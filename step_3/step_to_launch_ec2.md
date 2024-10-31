# Step-by-Step Guide to Upload and Deploy `step_2.zip` to an EC2 Instance

## Step 1: Launch an EC2 Instance

### 1. Log in to AWS Console:

- Sign in to the AWS Management Console.

### 2. Navigate to EC2:

- In the AWS Management Console, search for EC2 and open the EC2 Dashboard.

### 3. Launch a New Instance

- Click the **Launch Instance** button.
- Choose **Amazon Linux 2** or **Ubuntu** as the AMI (Amazon Machine Image).
- Select **t2.micro** (which is free-tier eligible).

### 4: Configure Security Group

### Create a New Key Pair:

1. On the left-hand menu, click **Key Pairs** under **Network & Security**.
2. Click the **Create key pair** button.

### Specify Key Pair Details:

- **Name**: Enter a name for your key pair (e.g., `chocfactory-key`).
- **Key pair type**: Select **RSA**.
- **Private key file format**: Choose `.pem` (for Linux/Mac) or `.ppk` (for Windows using PuTTY).

### Download the Key Pair:

- After clicking **Create key pair**, AWS automatically downloads the private key file (.pem for Linux/Mac or .ppk for Windows).
- Keep this file safe. You’ll need it to SSH into your EC2 instance.

## Configuring the Network Settings

### 1. Choose Network (VPC):

- If you already have a VPC (Virtual Private Cloud) set up, select it from the dropdown.
- If not, you can use the default VPC, which AWS creates automatically. The default VPC should be sufficient for simple deployments like your ChocFactory website.

### 2. Select Subnet:

- Choose a subnet within your VPC where your EC2 instance will reside. The default subnet is typically selected for you, and you can leave this unchanged unless you have a specific need to choose a different subnet.

### 3. Enable Auto-Assign Public IP:

- Make sure that **Auto-assign public IP** is set to **Enabled**. This ensures that your EC2 instance gets a public IP address, which is necessary for accessing the server over the internet.

### 4. Security Group Configuration:

- Under **Firewall (security groups)**, create a new security group or select an existing one that allows inbound traffic for HTTP, HTTPS, and SSH.

If you’re creating a new security group:

- **Name**: Enter a security group name (e.g., `chocfactory-sg`).
- **Description**: Describe the security group (e.g., "Security group for ChocFactory EC2").

Then configure the following inbound rules:

| Type  | Protocol | Port Range | Source                     | Description                                                                                                                          |
| ----- | -------- | ---------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| HTTP  | TCP      | 80         | Anywhere (0.0.0.0/0, ::/0) | Allows public access to the web server.                                                                                              |
| SSH   | TCP      | 22         | Your IP                    | Allows you to SSH into your instance. (Restrict this to your own IP for security purposes, but you can select Anywhere for testing.) |
| HTTPS | TCP      | 443        | Anywhere (0.0.0.0/0, ::/0) | If you plan to use SSL/TLS in the future.                                                                                            |

### Review:

- Review the settings to ensure the security group is correctly configured for HTTP and SSH access.
- Once satisfied, proceed to the next step by clicking **Launch Instance**.

---

## Step 2: uploading zip

### 1. connect EC2 using Putty:

- connect using putty remember the .ppk file.

### 2. download Putty SCP (PSCP)

- download the pscp.exe file from the putty website remember what folder you store it in

### 3. open command terminal

- win (key) + R (key) then type cmd to open command terminal

### 4. be in the right folder 

```bash
 cd c:\Users\downloads
 
```

### 5. uploading zip to ec2

```bash
 pscp -i path_to_your_ppk_file step_2.zip ec2-user@your-ec2-public-ip:/home/ec2-user/
```

- Replace `path_to_your_ppk_file` with the path to your `.ppk` file.
- Replace `your-ec2-public-ip` with the public IP address of your EC2 instance.
  
This will copy `step_2.zip` to the `/home/ec2-user/` directory of your EC2 instance.

---

## Step 3: Unzip the File

### 1. SSH into EC2

- Use PuTTY to SSH into your EC2 instance

### 2. Install Unzip (if necessary):

- If unzip is not installed on your EC2 instance, install it with the following command

```bash
sudo yum install unzip
```

### 3. Unzip the File

- Navigate to the directory where you uploaded `step_2.zip`

```bash
cd /home/ec2-user/
```

- unzip the file

```bash
unzip step_2.zip
```

---

## Step 4: Deploy the Files

### 1. Move the Unzipped Files to the Web Server Directory

- Depending on how you're hosting the site, you’ll need to move the files to the appropriate directory (e.g., `/var/www/html/` for Apache on Amazon Linux/Ubuntu):

```bash
sudo mv step_2/* /var/www/html/
```

### 1.1. creating Directory

- Create /var/www/html: Run the following command to create the directory:

```bash
sudo mkdir -p /var/www/html
```

### 1.2. Move Files to the Directory

- Move the Files: Now that the directory is created, you can move your files from the `step_2` directory into `/var/www/html/`

```bash
sudo mv step_2/* /var/www/html/
```

### 2. Restart the Web Server

- After moving the files, restart your web server to ensure it recognizes the changes. ( have Appache web server(httpd installed))

```bash
sudo systemctl restart httpd
```

### 2.1 Install Apache if you do not

```bash
sudo yum install httpd -y
```
### 2.2 Start the Apache Service: After installation, start the Apache service

```bash
sudo systemctl start httpd
```

### 2.3 Enable Apache to Start on Boot (optional): To ensure Apache starts automatically on system boot, run

```bash
sudo systemctl enable httpd
```

### 2.4 Verify Apache is Running

```bash
sudo systemctl status httpd  # for Amazon Linux
```

### step2. Navigate to the directory where you uploaded `step_2.zip`

```bash
cd /home/ec2-user/
```


### imprtant note - If unable to see website check the address. make sure it is http not https


