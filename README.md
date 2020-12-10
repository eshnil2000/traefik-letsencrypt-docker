### Traefik Letsencrypt Docker Setup refer to 
https://www.digitalocean.com/community/tutorials/how-to-use-traefik-v2-as-a-reverse-proxy-for-docker-containers-on-ubuntu-20-04

###

```sh
sudo apt-get install apache2-utils
htpasswd -nb admin secure_password
git clone this repo
touch acme.json
chmod 600 acme.json

```
### htpasswd , use in traefik.toml
```
Output
admin:$apr1sdasdadasdasdasd/asdasdad
```
###

### Configure DNS entries
``` 
A record : *.yourdomain.com IP address
A record : monitor.yourdomain.com IP address
A record : @ IP address
```
 
### Start the container
docker run -d \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $PWD/traefik.toml:/traefik.toml \
  -v $PWD/traefik_dynamic.toml:/traefik_dynamic.toml \
  -v $PWD/acme.json:/acme.json \
  -p 80:80 \
  -p 443:443 \
  --network web \
  --name traefik \
  traefik:v2.3


### go to traefik dashboard
https://monitor.yourdomain.com
### test containers reverse proxy Setup 
```sh
cd wordpress
docker-compose up -d

cd ../whoami
docker-compose up -d
```
### to tear down
``` 
docker-compose down
```

### Bare metal setup
```
sudo apt update
sudo snap install docker
sudo snap start docker
sudo ufw default allow routed
sudo ufw allow http
sudo ufw allow ssh
sudo ufw allow 8080
sudo ufw allow 443
sudo apt-İet install fail2ban
ssh-keygen
chmod 0400 pemfile.pem

sudo ufw status
sudo ufw show added
sudo ufw status verbose

sudo nano /etc/hosts
and then add:

cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

sudo apt install bash-completion
```

```sh
./bash_profile
alias kubectl="microk8s kubectl"
alias helm="microk8s helm3"

[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion
source /etc/profile.d/bash_completion.sh

source <(kubectl completion bash)

```

### SSL,DNS checker
https://www.sslshopper.com/ssl-checker.html#hostname=https://monitor.codenovator.com/
https://dnschecker.org/#A/monitor.yourdomain.com

