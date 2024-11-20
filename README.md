# VaultWarden-with-Nginx
This repository is the required docker-compose and configuration files to self host Vault Warden with Nginx acting as a reverse proxy.

## Notes
In my case I want to make the Vault Warden database accessible on my host system along with my Nginx configuration file and certificate. You can just as easily set up a persistent volume for the conatiners rather than creating mount points to the host system.

## How to
1. Install docker compose
2. Create the docker network - `docker network create vaultwarden_network`
3. Create a temporary Vault Warden server to get the admin password hash - `docker run --rm -it vaultwarden/server /vaultwarden hash`
4. Manipulate the hash output and save it for later to put in the docker compose file - `echo 'your-authentication-token-here' | sed 's#\$#\$\$#g'`
5. Create the docker compose file
6. 
