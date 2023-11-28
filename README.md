
The containerize directory contains the following structure:

app folder: This includes:

.dockerignore: A file to specify what to ignore during Docker build.
src folder: Presumably contains the source code of the Python web application.
Dockerfile: For building the app's Docker image.
nginx folder: This includes:

.dockerignore: Similar to the one in the app folder.
files folder: Likely contains the SSL keypair and other necessary files for nginx.
Dockerfile: For building the nginx Docker image.
nginx.conf: The nginx configuration file.
Other files:

README.md: contains instructions or information about the project.
validate.sh: A shell script for validation purposes.
docker-compose.yml: For defining and running multi-container Docker applications.
Given this structure, let's proceed with the tasks as per your requirements. We'll start by addressing Part One, which involves completing the nginx.conf file. ​​

The current nginx.conf file has a basic configuration with placeholders for your modifications. Here's what needs to be added to meet the requirements of Part One:

Server Directives for Ports 80 and 443: We need to configure Nginx to listen on both HTTP (port 80) and HTTPS (port 443).

Redirect HTTP to HTTPS: Any HTTP request should be permanently redirected to HTTPS.

SSL Configuration: Set up SSL using the provided localhost.crt and localhost.key files. These files should be made available to Nginx but not included in the Docker image.

Modern and Secure Protocols and Ciphers: The SSL configuration should enforce the use of modern and secure protocols and ciphers.

Upstream Directive for Proxying Requests: Nginx should proxy requests to the upstream Python application.

Passing Necessary Headers: Include X-Forwarded-For, X-Real-IP, and X-Forwarded-Proto headers with appropriate values in the requests to the upstream application.

nginx.conf: 
This configuration meets the specified requirements:

Ports 80 and 443: It listens on both HTTP and HTTPS.
HTTP to HTTPS Redirect: All HTTP traffic is permanently redirected to HTTPS.
SSL Configuration: Uses the provided SSL certificate and key.
Modern Protocols and Ciphers: TLSv1.2 and TLSv1.3 with strong ciphers.
Upstream Proxy: Requests are proxied to the app server running on port 8000.
Headers: X-Forwarded-For, X-Real-IP, and X-Forwarded-Proto headers are passed.


Part Two Requirements Recap:
App Dockerfile: Securely build, install, and configure the Python application into a container.
Nginx Dockerfile: Build an nginx container configured with the updated nginx.conf.
Docker-Compose:
Start the app in development mode with hot code reload.
Start nginx configured from Part One.
Ensure the app service is not directly accessible from the host.
Drafting the Dockerfiles and docker-compose.yml:
App Dockerfile
Use a lightweight Python base image.
Copy the application source code.
Install necessary dependencies.
Set the command to run the application with a production-quality server like Gunicorn.
Nginx Dockerfile
Use an nginx base image.
Copy the SSL certificate and key.
Copy the updated nginx.conf.
Expose ports 80 and 443.
Docker-Compose
Define services for app and nginx.
Mount the app's source code for hot code reload.
Configure nginx to proxy requests to the app service.
