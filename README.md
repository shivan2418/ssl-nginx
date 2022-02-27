# ssl-nginx
Dockerfile for getting a letsecrypt certificate. Tested and working.

This docker-files uses nginx and certbot to request a certificate that can then be mounted by another 
project.


### How to 
To avoid any conficts with other docker-compose files and nginx.conf you should clone this project
on the safe level as the root folder of the project you want SSL for. Like so.

![image](https://user-images.githubusercontent.com/40603805/155863263-1c166b82-be84-40a8-9810-fe8108632415.png)

### Steps
1. Turns off your website, nginx etc. This project needs to be able to listen on port 80 and 443.
  Edit the command for the certbot service in `docker-compose.yml` file. Fil in the proper domain and email.
  You can require more certificates by adding multiple `-d <domain>`. You can optionally add `--dry-run` to test if it works before you go live. Keep in mind certbot/letsencrypt has a rate limit.
2. Run the script using `docker-compose up`
3. There should now be certifates in in the a folder called `certbot` in the same folder as this project.
4. (optional) Mount the certificates in your other proejct using under volumes.
```  
../nginx-ssl/certbot/conf:/etc/nginx/ssl
../nginx-ssl/certbot/data:/var/www/certbot
```
 