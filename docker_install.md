# Update Linux Installation


```
sudo apt update && sudo apt upgrade
```

# Install docker and Docker-compose

## Install Pre-requisites

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

## Add docker repository key

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

```
sudo apt update
```

### To Make sure it uses docker repository

```
apt-cache policy docker-ce
```

## Install Docker

```
sudo apt install docker-ce
```

## Check Docker status

```
systemctl status docker
```

## Add current user to Docker group

```
sudo usermod -aG docker ${USER}
```

### Log back in

```
su - ${USER}
```

### Check user

```
id -nG
```
### To add another user to Docker group

```
sudo usermod -aG docker username
```

## Install Docker-compose

Check the [current release](https://github.com/docker/compose/releases)
and replace the command

```
sudo curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

### Set the permissions to the executable

```
sudo chmod +x /usr/local/bin/docker-compose
```

### Check the installation

```
docker-compose --version
```