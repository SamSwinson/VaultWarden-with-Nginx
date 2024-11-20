# VaultWarden-with-Nginx
This repository is the required docker-compose and configuration files to self host Vault Warden with Nginx acting as a reverse proxy.

## Blog Post
If you want a more detailed walk through of this then head over to my blog post about it. [Self Hosted Password Manager Using Docker](https://knowledgeaddict.co.uk/2024/11/20/self-hosted-password-manager-using-docker/)

## Notes
In my case I want to make the Vault Warden database accessible on my host system along with my Nginx configuration file and certificate. You can just as easily set up a persistent volume for the containers rather than creating mount points to the host system.

You will also need some form of web certificate. This can be self-signed locally on the box you are using or if you have a home certificate authority. If you go this route you need to make sure the CA certificate is installed on any devices you want to connect to the Vault Warden server because the mobile BitWarden application and some web bowers will not allow you to connect if you have an untrusted certificate. Alternatively, you can get a certificate signed by a 3rd party certificate authority that is already trusted on your devices.

## How to
1. Install docker compose
2. Create the docker network - `docker network create vaultwarden_network`
3. Create a temporary Vault Warden server to get the admin password hash - `docker run --rm -it vaultwarden/server /vaultwarden hash`
4. Manipulate the hash output and save it for later to put in the docker compose file - `echo 'your-authentication-token-here' | sed 's#\$#\$\$#g'`
5. Create the docker compose file
6. Create the Nginx configuration file and make sure it is in the same location as referenced in the docker compose file
7. Place the Nginx certificates in the same place as referenced in the docker compose file

## Start Containers
Enter the directory your docker compose file is in.
`docker-compose up -d`

## Stop Containers
Enter the directory your docker compose file is in.
`docker-compose down`
