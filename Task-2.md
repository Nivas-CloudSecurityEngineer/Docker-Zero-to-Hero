```
# Use Ubuntu as the base image
FROM ubuntu:latest

# Update package lists and install Nginx
RUN apt-get update && apt-get install -y nginx

# Remove the default Nginx index.html file
RUN rm /var/www/html/index.nginx-debian.html

# Copy the custom index.html to the Nginx web directory
COPY index.html /var/www/html/

# Expose port 80
EXPOSE 80

# Start Nginx service
CMD ["nginx", "-g", "daemon off;"]

```
