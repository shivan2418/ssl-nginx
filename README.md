# ssl-nginx
Dockerfile for getting a letsEncrypt certificate. Tested and working.

This docker-files uses nginx and certbot to request a certificate that can then be mounted by another 
project.


### How to 
To avoid any conflicts with other docker-compose files and nginx.conf you should clone this project
on the safe level as the root folder of the project you want SSL for. Like so.

![image](https://user-images.githubusercontent.com/40603805/155863263-1c166b82-be84-40a8-9810-fe8108632415.png)

### Steps to get/renew certificate
1. Edit the command for the certbot service in `docker-compose.yml` file. Fill in your domain and email.
2. Turns off any other services using port 80 and 443. This ssl-nginx needs to be able to listen on port 80 and 443 to get the certificate.
  You can request multiple certificates by adding multiple `-d <domain>`. You can optionally add `--dry-run` to test if it works before you go live. Keep in mind certbot/letsencrypt has a rate limit.
3. Run the script using `docker-compose up`
4. There should now be certificates in a folder called `certbot` in the same folder as this project.
5. (optional) Mount the certificates in your other project using under volumes.
  4.1 Under nginx can should mount them as
    ```  
      ../ssl-nginx/certbot/conf:/etc/nginx/ssl
      ../ssl-nginx/certbot/data:/var/www/certbot
    ```
    and then reference them by their full path in the containers in your nginx.conf file
    ```
        ssl_certificate /etc/nginx/ssl/live/example.comz/fullchain.pem;
        ssl_certificate_key /etc/nginx/ssl/live/example.com/privkey.pem;
    ```


 
