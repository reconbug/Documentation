# Installation instructions

## Node.js v11.x:

## Using ubuntu
```
cd ~
```
```
curl -sL https://deb.nodesource.com/setup_11.x -o nodesource_setup.sh
```
```
chmod 764 nodesource_setup.sh 
```
```
sudo bash nodesource_setup.sh 
```
```
sudo apt-get install -y nodejs
```

## Node.js v10.x:
```
cd ~
```
```
curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh
```
```
chmod 764 nodesource_setup.sh 
```
```
sudo bash nodesource_setup.sh 
```
```
sudo apt-get install -y nodejs

```

## Commands will be shown in the Output of above
```
# Run `sudo apt-get install -y nodejs` to install Node.js 10.x and npm
## You may also need development tools to build native addons:
     sudo apt-get install gcc g++ make
## To install the Yarn package manager, run:
     curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
     echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
     sudo apt-get update && sudo apt-get install yarn

```

# Optional: install build tools

To compile and install native addons from npm you may also need to install build tools:

# use `sudo` on Ubuntu
```
sudo apt-get install -y build-essential
```
