# Install supabase on Oracle oci

# First steps:
```
# Get the code
git clone --depth 1 https://github.com/supabase/supabase

# Go to the docker folder
cd supabase/docker

# Copy the fake env vars
cp .env.example .env

# Pull the latest images
docker compose pull

# Start the services (in detached mode)
docker compose up -d
```

# Verify that everything worked

```
docker compose ps
```

# Change default username and password editing .env within your Docker directory!!

Change these as well as the default secrets:
```
Username: supabase
Password: this_password_is_insecure_and_should_be_updated
```
#Nginx Setup

```
cd /etc/nginx/sites-available/
sudo nano supabase.conf
```

```
server {
    server_name <domain name>;
    listen 80;

    location / {
        proxy_pass http://localhost:5678;
        proxy_set_header Connection '';
        proxy_http_version 1.1;
        chunked_transfer_encoding off;
        proxy_buffering off;
        proxy_cache off;
    }
}
```
#Link and Test Nginx Configs
```
sudo ln -s /etc/nginx/sites-available/n8n.conf /etc/nginx/sites-enabled/
sudo nginx -t
```

#Apply all changes
```
# Stop and remove the containers
docker compose down

# Recreate and start the containers
docker compose up -d
```


