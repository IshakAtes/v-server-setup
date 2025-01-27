# v-server-setup  
Guide:  
[Download the PDF Checklist](https://github.com/IshakAtes/v-server-setup/blob/main/Git%20%2B%20VServer%20Checkliste.pdf)


Walkthrough: Setting Up a Server with SSH and Nginx  

This guide walks you through setting up a virtual server, configuring SSH keys, disabling password authentication, and installing a web server (Nginx).  

---

## Table of Contents  

0. [**Introduction**](#v-server-setup)
   - Overview of the guide  

1. [**Step 1: Generate an SSH Key Pair**](#step-1-generate-an-ssh-key)
   - Create a secure SSH key  

2. [**Step 2: Specify the Key's Path**](#step-2-specify-the-keys-path)  
   - Define where the key will be stored  

3. [**Step 3: View the Keys**](#step-3-view-the-keys)  
   - Verify existing keys  

4. [**Step 4: Connect to the Server**](#step-4-connect-to-the-server)  
   - Establish an initial SSH connection

5. [**Step 5: Copy the Key to the Server**](#step-5-copy-the-key-to-the-server)
   - Transfer the public key to the server  

6. [**Step 6: Test the Connection with the New Key**](#step-6-test-the-connection-with-the-new-key)
   - Verify the connection with the new key  

7. [**Step 7: Disable Password Authentication**](#step-7-disable-password-authentication)
   - Secure the server by disabling password login  

8. [**Step 8: Restart the SSH Service**](#step-8-restart-the-ssh-service)
    - Apply the changes and restart SSH  

9. [**Step 9: Verify the Setup**](#step-9-verify-the-setup)
    - Test the updated SSH configuration  

10. [**Step 10: Update the System**](#step-10-update-the-system)
    - Update the server’s packages  

11. [**Step 11: Install Nginx**](#step-11-install-nginx)
    - Install the Nginx web server  

12. [**Step 12: Check the Nginx Status**](#step-12-check-the-nginx-status)
    - Verify that Nginx is running  

13. [**Step 13: Create an Alternative HTML Page**](#step-13-create-an-alternative-html-page)
    - Set up a custom HTML page  

14. [**Step 14: Configure Nginx**](#step-14-configure-nginx)
    - Create and configure a new Nginx site  

15. [**Step 15: Restart Nginx**](#step-15-restart-nginx)
    - Restart Nginx to apply changes  

16. [**Step 16: Test the Alternative Page**](#step-16-test-the-alternative-page)
    - View the custom page in your browser  

    [**Conclusion**](#Conclusion)
    - congratulations, you have set up a server

---


## Setup SSH

## Step 1: Generate an SSH Key

Run the following command to create a new SSH key pair for the server:
```bash
ssh-keygen -t ed25519 -f C:/Users/user-directory/.ssh/demo-server -C "demo-server key"  
```



## Step 3: View the Keys

List your existing keys using this command:
```bash
ls ~/.ssh/da/  
```
> [!Note]
> The `~` symbol represents your home directory, e.g., `C:/Users/user-directory` .



## Step 4: Connect to the Server

Use the following command to connect to your server:
```bash
ssh username@ip-address  
```



## Step 5: Copy the Key to the Server

Copy the public key to your server:
```bash
type C:\Users\user-directory\.ssh\demo-server.pub | ssh username@ip-address "cat >> .ssh/authorized_keys"  
```



## Step 6: Test the Connection with the New Key

Connect to the server using the new SSH key:
```bash
ssh -i C:/Users/user-directory/.ssh/demo-server username@ip-address  
```



## Step 7: Disable Password Authentication

Edit the SSH configuration file:
```bash
sudo nano /etc/ssh/sshd_config  
```

Set the following parameter:
```bash
PasswordAuthentication no  
```
#### Save the file with `Ctrl + O` and exit with `Ctrl + X`.



## Step 8: Restart the SSH Service

Restart the SSH service to apply changes:
```bash
sudo systemctl restart ssh.service  
```

and logout:
```bash
logout
```



## Step 9: Verify the Setup

Test logging in with the SSH key:
```bash
ssh -i ~/.ssh/demo-server username@ip-address  
```



## Step 10: Update the System

Run the following command to update your server:
```bash
sudo apt update  
```




## Setup Nginx

## Step 11: Install Nginx

Install the Nginx web server:
```bash
sudo apt install nginx -y  
```



## Step 12: Check the Nginx Status

Verify that Nginx is running:
```bash
systemctl status nginx.service  
```
#### If we now enter our IP address `http://<ip_address>/` in the browser, we will be greeted by the Nginx default HTML page.



## Step 13: Create an Alternative HTML Page

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



## Step 14: Configure Nginx

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



## Step 15: Restart Nginx

After making changes to the configuration or HTML files, restart the Nginx service to apply the updates:

```bash
sudo service nginx restart  
```
#### Check the status of the Nginx service to verify when it was last restarted:
#### The output will show the service's current state and the timestamp of the last update or restart.
#### `systemctl status nginx.service`



## Step 16: Test the Alternative Page

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