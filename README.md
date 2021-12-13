# Installation

This project is run via docker and docker-compose.
Make sure both are installed.

First, the environment needs to be set. You can do this 
by creating a file called `.env` in the root project directory.
Use the following template:

```
PATH_SSL_CERT=/path/to/ssl-certs/fullchain.pem
PATH_SSL_KEY=/path/to/ssl-certs/privkey.pem
PATH_SSL_DIR=/path/to/ssl-certs

SMTP_HOST=mail.example.org
SMTP_PORT=587
SMTP_FROM=user@example.org
SMTP_SSL=true
SMTP_USERNAME=user@example.org
SMTP_PASSWORD=secret_password

SSMTP_HOSTNAME=example.org

URL_BASE=https://vaultwarden.example.org
FQDN=vaultwarden.example.org

# comma separated list of email domains, 
# which are allowed to sign up for an account
SIGNUPS_DOMAINS_WHITELIST=example.org

# if the ADMIN_TOKEN is set (also in the docker-compose file)
# the admin panel of vaultwarden gets enabled
# use a strong passphrase!
# ADMIN_TOKEN=

```

You can change the fail2ban configuration in the file `./fail2ban/conf/jail.d/vaultwarden.local`.
You should change the `maxretry` and `ignoreip` directives.

You can run it via `docker-compose up -d`.

# fail2ban

## unban an ip address

First get the container ID with `docker ps`.
Then, execute this command.

```
docker exec -t <CONTAINER> fail2ban-client set <JAIL> unbanip <IP>
```

E.g. 

```
docker exec -t d83 fail2ban-client set vaultwarden unbanip 149.20.4.15
```
