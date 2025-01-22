# v-server-setup  
Guide:  
[Download the PDF checkliste](https://github.com/IshakAtes/v-server-setup/blob/main/Git%20%2B%20VServer%20Checkliste.pdf)


Walkthrough: Setting Up a Server with SSH and Nginx  

This guide walks you through setting up a virtual server, configuring SSH keys, disabling password authentication, and installing a web server (Nginx).  

---

## Table of Contents  

0. [**Introduction**](#v-server-setup)
   - Overview of the guide  

1. [**Step 1: Generate an SSH Key**](#step-1-generate-an-ssh-key)
   - Create a secure SSH key  

2. [**Step 2: Specify the Key's Path**](#step-2-specify-the-keys-path)  
   - Define where the key will be stored  

3. [**Step 3: View the Keys**](#step-3-view-the-keys)  
   - Verify existing keys  

4. [**Step 4: Connect to the Server**](#step-4-connect-to-the-server)  
   - Establish an initial SSH connection  

5. [**Step 5: Create a New Key Pair**](#step-5-create-a-new-key-pair)  
   - Generate a dedicated SSH key for the server  

6. [**Step 6: Copy the Key to the Server**](#step-6-copy-the-key-to-the-server)
   - Transfer the public key to the server  

7. [**Step 7: Test the Connection with the New Key**](#step-7-test-the-connection-with-the-new-key)
   - Verify the connection with the new key  

8. [**Step 8: Disable Password Authentication**](#step-8-disable-password-authentication)
   - Secure the server by disabling password login  

9. [**Step 9: Restart the SSH Service**](#step-9-restart-the-ssh-service)
    - Apply the changes and restart SSH  

10. [**Step 10: Verify the Setup**](#step-10-verify-the-setup)
    - Test the updated SSH configuration  

11. [**Step 11: Update the System**](#step-11-update-the-system)
    - Update the server’s packages  

12. [**Step 12: Install Nginx**](#step-12-install-nginx)
    - Install the Nginx web server  

13. [**Step 13: Check the Nginx Status**](#step-13-check-the-nginx-status)
    - Verify that Nginx is running  

14. [**Step 14: Create an Alternative HTML Page**](#step-14-create-an-alternative-html-page)
    - Set up a custom HTML page  

15. [**Step 15: Configure Nginx**](#step-15-configure-nginx)
    - Create and configure a new Nginx site  

16. [**Step 16: Restart Nginx**](#step-16-restart-nginx)
    - Restart Nginx to apply changes  

17. [**Step 17: Test the Alternative Page**](#step-17-test-the-alternative-page)
    - View the custom page in your browser  

---


## Setup SSH

## Step 1: Generate an SSH Key

Run the following command to create an SSH key:
```bash
ssh-keygen -t ed25519
```



## Step 2: Specify the Key's Path

During key creation, specify the path where the key should be stored, for example:
```bash
C:/Users/user-directory/.ssh/da/demo_ed25519
```



## Step 3: View the Keys

List your existing keys using this command:
```bash
ls ~/.ssh/da/  
```
> [!NOTE]: The `~` symbol represents your home directory, e.g., `C:/Users/user-directory` .



## Step 4: Connect to the Server

Use the following command to connect to your server:
```bash
ssh username@ip-address  
```


## Step 5: Create a New Key Pair

Generate a new SSH key pair for the server:
```bash
ssh-keygen -t ed25519 -f C:/Users/user-directory/.ssh/demo-server -C "demo-server key"  
```



## Step 6: Copy the Key to the Server

Copy the public key to your server:
```bash
type C:\Users\user-directory\.ssh\demo-server.pub | ssh username@ip-address "cat >> .ssh/authorized_keys"  
```



## Step 7: Test the Connection with the New Key

Connect to the server using the new SSH key:
```bash
ssh -i C:/Users/user-directory/.ssh/demo-server username@ip-address  
```



## Step 8: Disable Password Authentication

Edit the SSH configuration file:
```bash
sudo nano /etc/ssh/sshd_config  
```

Set the following parameter:
```bash
PasswordAuthentication no  
```
#### Save the file with `Ctrl + O` and exit with `Ctrl + X`.



## Step 9: Restart the SSH Service

Restart the SSH service to apply changes:
```bash
sudo systemctl restart ssh.service  
```

and logout:
```bash
logout
```



## Step 10: Verify the Setup

Test logging in with the SSH key:
```bash
ssh -i ~/.ssh/demo-server username@ip-address  
```



## Step 11: Update the System

Run the following command to update your server:
```bash
sudo apt update  
```




## Setup Nginx

## Step 12: Install Nginx

Install the Nginx web server:
```bash
sudo apt install nginx -y  
```



## Step 13: Check the Nginx Status

Verify that Nginx is running:
```bash
systemctl status nginx.service  
```
#### If we now enter our IP address `http://<ip_address>/` in the browser, we will be greeted by the Nginx default HTML page.



## Step 14: Create an Alternative HTML Page

Create a new directory for your alternative HTML page:
```bash
sudo mkdir /var/www/alternatives  
```

Create the HTML file:
```bash
sudo touch /var/www/alternatives/alternate-index.html  
```

Edit the file:
```bash
sudo nano /var/www/alternatives/alternate-index.html  
```

Example content:
```html
<!doctype html>
<html>  
  <head>
    <meta charset="utf-8">
    <title>Hello, Nginx!</title>  
  </head>  
  <body>
    <h1>Hello, Nginx!</h1>  
    <p>I have just configured our Nginx web server on Ubuntu Server!</p>  
  </body>  
</html>  
```
#### Save and exit the nano editor:
#### Press `Ctrl + O` to save the file. Press `Enter` to confirm the filename. Press `Ctrl + X` to exit.



## Step 15: Configure Nginx

Create a configuration file for the alternative page:
```bash
sudo nano /etc/nginx/sites-enabled/alternatives  
```

Example configuration:
```nginx
server {  
    listen 8081;  
    root /var/www/alternatives;  
    index alternate-index.html;  

    location / {  
        try_files $uri $uri/ =404;  
    }  
}  
```



## Step 16: Restart Nginx

After making changes to the configuration or HTML files, restart the Nginx service to apply the updates:

```bash
sudo service nginx restart  
```
#### Check the status of the Nginx service to verify when it was last restarted:
#### The output will show the service's current state and the timestamp of the last update or restart.
#### `systemctl status nginx.service`



## Step 17: Test the Alternative Page

Now we can see our alternative HTML page by entering our IP address followed by port `:8081` in the browser:
```bash
http://ip-address:8081/
```



## Conclusion
### Congratulations! 🎉 You have successfully set up your virtual server, configured SSH keys for secure access, disabled password authentication and installed and customized a web server with Nginx.

### By following this walkthrough, you’ve learned:

- How to create and use SSH keys for secure authentication.
- How to configure and manage the Nginx web server.
- How to serve custom web pages from your server.

#### Your server is now ready to be expanded further, whether for hosting websites, deploying applications, or exploring advanced configurations.

#### If you encounter any issues or want to share feedback, feel free to reach out or contribute improvements to this guide.

#### Happy coding! 🚀