## how to setup ssl for your domain.

### Use
- NGINX, ZEROSSL, DOCKER, VIM, UBUNTU 20.x

### Knowledge 
1. Know about RSA: mechanism, usage(public key, signature, CA authorities) 
2. Know about nginx: how to setup, public http domain

### Steps
#### step1: setup domain run successfully with http  
Using this script to install `nginx`
```
#!/bin/bash

echo "Updating package lists..."
sudo apt update

echo "Installing Nginx..."
sudo apt install -y nginx

echo "Starting Nginx service..."
sudo systemctl start nginx

echo "Enabling Nginx to start on boot..."
sudo systemctl enable nginx

echo "Nginx installation complete!"
echo "Nginx status:"
sudo systemctl status nginx
```

Then, setup `nginx` to point to our services. let config our proxy server like this: 
```
# /etc/nginx/conf.d/your_domain.com.conf
server {
    listen 80;
    server_name your_domain www.your_domain.com;

    location / {
        proxy_pass http://127.0.0.1:3000; # exam: 3000 is the target port
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    access_log /var/log/nginx/your_domain.access.log;
    error_log /var/log/nginx/your_domain.error.log;
}
```
#### step2: ask the certificate from SSL issuers: letencrypt | zerossl,..
Go to the console/ dashboard of the issuer, setup your domain information, and generate the certificate for this domain. Then CA authorities(Issuer) want to verify that `"you own this domain"`.  

At the time I documented, ZeroSSL have 3 ways to verify `HTTP-01 challenge` `DNS-01 challenge` `Email verification`.   

- **HTTP-01 challenge** 

Pros:  
It’s easy to automate without extra knowledge about a domain’s configuration.
It allows hosting providers to issue certificates for domains CNAMEd to them.
It works with off-the-shelf web servers.  

Cons:  
It doesn’t work if your ISP blocks port 80 (this is rare, but some residential ISPs do this).
Let’s Encrypt doesn’t let you use this challenge to issue wildcard certificates.
If you have multiple web servers, you have to make sure the file is available on all of them.  

- **DNS-01 challenge**  

The Issuer will generate a CNAME record, then you access into your domain's dashboard to config a new record. then put the verify button on zerossl's dashboard.  
- **Email verification**     

They send code via email, then you access to your email, put the code the verify `"you own this domain"`  


after this step, you will have some type of certificate files: `certificate.crt`, `ca_bundle.crt`, `private.key`.

put it `/etc/ssl/your_domain`

#### step3: install the certificate into your server 

With NGINX, you have to merge the certificate. 
```shell
$ cat certificate.crt ca_bundle.crt >> certificate.crt
```

change nginx configuration like this 
```
server {
    listen 443 ssl;
    server_name your_domain.com www.your_domain.com;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location ^~ /.well-known/pki-validation/ {
        alias /var/www/html/.well-known/pki-validation/;
        allow all;
    }

    
    ssl_certificate /etc/ssl/your_domain.com/certificate.crt;
    ssl_certificate_key /etc/ssl/your_domain.com/private.key;

    access_log /var/log/nginx/your_domain.com.access.log;
    error_log /var/log/nginx/your_domain.com.error.log;
}

# Redirect HTTP to HTTPS
server {
    listen 80;
    server_name your_domain.com www.your_domain.com;

    # Redirect all traffic to HTTPS
    location / {
        return 301 https://$host$request_uri;
    }
}
```


after all, restart your nginx: 
```
$ sudo systemctl restart nginx
```

Thanks