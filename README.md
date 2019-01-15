# letsencrypt-glesys-hook (DNS-01 and the GleSYS API).
How to set up letsencrypt via DNS (glesys-dns01) Works for wildcard

## Dependencies
- curl
- xmlstarlet (debian: apt-get install curl xmlstarlet)
- GleSYS API credentials (DOMAIN permissions for list, add, remove records) 
  (in case you want to uppload the cert to load-balancer you will need permissions to the LB too)

## Instructions

- Create an API key for the GleSYS API in the control panel as it described above
- echo "export USER=CL12345" > /etc/ssl/private/glesys-credentials
- echo "export KEY=KEY_GOES_HERE" >> /etc/ssl/private/glesys-credentials
- echo "export LOADBALANSERID=lb1234567" >> /etc/ssl/private/glesys-credentials (in case you use load-balancer)
- chmod 600 /etc/ssl/private/glesys-credentials
- git clone https://github.com/abed19919/letsencrypt_glesys-dns01.git /etc/dehydrated/
- edit your /etc/dehydrated/config to include the hook you want to use
  * glesys-dns-01-hook.sh # if you don't have a load-balancer # Active be default
  * glesys-dns-01-lbl-hook.sh # to be upload the cert direct to the load-balancer
- echo "example.com *.example.com" > /etc/dehydrated/domains.txt # you domain here!

- cd /etc/dehydrated
- ./dehydrated --register --accept-terms
- ./dehydrated -c
