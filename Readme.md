10 Today Navigation Menu Sign in Irefoh1 / EC2-deploysamples Public Code

Explain the process again Issues Pull requests Irefoh1/EC2-deploysamples Name Irefoh1 Irefoh1 3 weeks ago images 3 weeks ago README.md 3 weeks ago index.html 3 weeks ago Repository files navigation README Simple Website with Apache / Nginx on EC2 This repository is a simple documentation on how to launch EC2 instances in the cloud and host simple web applications in them.

Security Group Setup Assuming you are inside your AWS Management Console, go to the EC2 section. Before you launch the instance, go to security group. Ensure your security group has the following rules

Rule 1: SSH | Port 22 | Source: My IP Rule 2: HTTP | Port 80 | Source: 0.0.0.0/0 (Anywhere) Port 80 is the default for web servers. Sec-Group Image

Launch instance and install apache Now proceed to launch your instance. A t3 micro will do the job perfectly. You could choose Amazon Linux or Ubuntu as the Amazon Machine Image.

After your instance is successfully provisioned, ssh into it and intall apache using the following commands

sudo dnf update -y sudo dnf install -y httpd That's it. Apache starts automatically after installation. Open your browser and go to: http:// Use reference from image to copy your public ip Sec-Group Image You should see the default apache page

Replace with Your Own Website It's now time to replace what is showing in the default page with your own website. The default website files are stored in /var/www/html/ Use this command to edit the files sudo vim /var/www/html/index.html Place what is inside index.html of this repo in here Save and exit. Now, go back to your url and refresh, and you'll see your application working. This is how your webpage will look like Sec-Group Image

Useful Commands sudo systemctl status httpd sudo systemctl restart httpd sudo systemctl stop httpd sudo systemctl start httpd Launch using Nginx After ssh, run the following commands to install Nginx

sudo dnf update -y sudo dnf install -y nginx Start and enable nginx sudo systemctl start nginx sudo systemctl enable nginx Confirm that it works

Replace with your website Use this command sudo vim /usr/share/nginx/html/index.html to get to the index.html file and replace the default nginx page with the index.html file on this repo

Check your public ip and it has magically updated

Got it—here’s a clear, step-by-step explanation of the whole process so you can follow it without confusion.

🚀 EC2 Website Deployment (Simple Explanation) Create a Security Group (Firewall Rules) Before launching your server, you set rules for what traffic is allowed:

SSH (Port 22) → only your IP → lets you connect securely to the server

HTTP (Port 80) → from anywhere (0.0.0.0/0) → allows anyone to access your website

Launch an EC2 Instance Inside Amazon Web Services (AWS):

Go to EC2 → Launch Instance

Choose:

OS: Amazon Linux or Ubuntu

Instance type: t3.micro (cheap/free tier)

Attach the security group you created

Launch and download your key pair (.pem file)

Connect (SSH into the Server) From your terminal:

ssh -i your-key.pem ec2-user@your-public-ip Now you're inside your cloud server.

Install a Web Server Option A: Apache Run:

sudo dnf update -y sudo dnf install -y httpd Start it:

sudo systemctl start httpd sudo systemctl enable httpd 👉 Visit in browser:

http://your-public-ip You should see the default Apache page.

Option B: Nginx (alternative) Run:

sudo dnf update -y sudo dnf install -y nginx Start it:

sudo systemctl start nginx sudo systemctl enable nginx Upload Your Website For Apache: sudo vim /var/www/html/index.html For Nginx: sudo vim /usr/share/nginx/html/index.html Delete existing content

Paste your index.html from the repo

Save and exit (:wq in vim)

Create a Security Group: Allow SSH (Port 22) from your IP Allow HTTP (Port 80) from anywhere Launch EC2 Instance: Choose Amazon Linux or Ubuntu Use t3.micro instance Attach security group Connect via SSH: Use ssh -i your-key.pem ec2-user@your-public-ip Install Web Server: Apache: sudo dnf install -y httpd Nginx: sudo dnf install -y nginx Upload Website: Apache: edit /var/www/html/index.html Nginx: edit /usr/share/nginx/html/index.html Access Website: Visit http://your-public-ip