# VPS Command Reference
Commands I use for routine VPS maintenance, Docker management, monitoring, and troubleshooting.

# Update Server
sudo apt update
sudo apt full-upgrade -y
sudo apt autoremove -y
sudo reboot

## Check Upgradable 
apt list --upgradable

## Prune Docker Images
docker image prune -af

## UFW Status
sudo ufw status verbose

## Fail2Ban Status
sudo systemctl status fail2ban

sudo fail2ban-client status
sudo fail2ban-client status sshd

## Tailscale Status
tailscale status

## Unbound Status
sudo systemctl status unbound

## dnscrypt Status
sudo systemctl status dnscrypt-proxy



## Pi-hole Status 
sudo pihole status
sudo pihole -up

### Pi-Hole Gravity
sudo pihole -g

## DNS Health Check
dig @127.0.0.1 -p 5335 1.1.1.1
dig @127.0.0.1 -p 5335 google.com

# Permissions 
sudo chown -R 1000:1000 /PATH
sudo chmod -R 775 /PATH

# Storage Check
df -h

# Memory Check
free -h


# Docker Status
docker ps

## Docker Restart
sudo systemctl restart docker

## Docker Compose
docker compose up -d
docker compose down
docker compose restart
docker compose config

## Container Logs
docker logs <container> --tail 50
docker logs -f <container>

# Github Push
git add .
git commit -m "[PUSH NAME]"
git push origin main



# Deploy new Gluetun container
  ## Add new port to Glutetun Compose, Save + Restart 
  - [TailscaleIP]:[PORT:PORT]

  ## Stop + Remove + Prune Existing Containers using Gluetun
  docker stop [gluteun containers]
  docker rm [gluteun containers]
  docker container prune -f


  ## Start Containers
  cd /ContainerPath && docker compose up -d
 

  ## Verify Container IP
  docker exec <container> curl -s https://ipinfo.io/ip

    

