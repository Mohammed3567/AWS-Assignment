# AWS-Assignment

This repo is for my AWS DevOps assignment. The task was to launch an EC2 instance, install Nginx, and host a simple HTML webpage on it.

## What I did

1. Launched an Ubuntu EC2 instance on AWS.
2. Created a security group and allowed port 22 (SSH) and port 80 (HTTP).
3. Connected to the instance using SSH.
4. Updated packages and installed Nginx.
5. Created an index.html and style.css file with my details.
6. Copied the files to the EC2 instance and moved them into the Nginx folder.
7. Restarted Nginx and checked the website using the EC2 public IP.
8. Pushed the code to this GitHub repo.

## EC2 Setup Steps

- Went to AWS Console > EC2 > Launch Instance.
- Chose Ubuntu as the OS.
- Proceeded with the default instance (free tier).
- Created a new key pair (.pem file) and downloaded it.
- Created a new security group with inbound rules:
  - SSH (port 22) from Anywhere
  - HTTP (port 80) from Anywhere
- Launched the instance
- Opened WSL ubuntu
- Copied the pem file from its location into the Linux environment:
```
cp /mnt/c/Users/HP/Downloads/website.pem ~/
```
- Changed the permission of the pem file:
```
chmod 400 ~/website.pem
```
- Finally connected using SSH from local terminal:

```
ssh -i ~/website.pem ubuntu@43.205.217.231
```

## Nginx Installation Steps

Ran these commands after connecting to the instance:

```
sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y
sudo systemctl status nginx
sudo systemctl restart nginx
sudo systemctl status nginx
```

Checked disk usage, memory usage, and running processes:

```
df -h
free -h
top
```

## Hosting the Website

- Wrote index.html and style.css on my laptop using VS Code.
- Copied both files from my laptop to the EC2 instance using SCP:

```
scp -i ~/website.pem /mnt/c/Users/HP/Desktop/aws-assignment/index.html ubuntu@43.205.217.231:/home/ubuntu/
```

- Logged into the EC2 instance and moved the files into the Nginx web root:

```
sudo cp index.html style.css /var/www/html/
sudo systemctl restart nginx
```

- Opened the browser and went to http://43.205.217.231 to confirm the website was live.
