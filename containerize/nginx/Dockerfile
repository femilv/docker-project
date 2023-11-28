# Use nginx base image
FROM nginx:alpine

# Copy SSL certs
COPY ./files/localhost.crt /etc/nginx/ssl/
COPY ./files/localhost.key /etc/nginx/ssl/

# Copy the Nginx global configuration file
COPY nginx.conf /etc/nginx/nginx.conf

# Expose ports
EXPOSE 80 443
