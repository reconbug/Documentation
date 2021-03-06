# Initialize and Start the Vagrant Box

After you've chosen a box, initialize the Vagrant box. Each one is slightly different, but here's how to do it for the example we're doing:

```
vagrant init hashicorp/precise64
```

This will also create a Vagrant file for you. Now, boot the box with Vagrant by doing (it will need to download if it's the first time using the it):

```
vagrant up
```

# SSH into the Box and Customize It

We'll now SSH into the box and start customizing it. If you don't know anything about servers, you can always just use Scotch Box since all of this is already done for you. Here's how to SSH into the box:

```
vagrant ssh
```

Now, we need to setup our server by installing whatever we want on it. This example will install a basic LAMP stack, but you can do whatever you like (Ruby, Nginx, etc.). The point of this article isn't to teach you how to setup a server, but instead how to turn your virtual environment into a Vagrant Box. So this step might be more involved than what is actually shown:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install vim
sudo apt-get install apache2
sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql
sudo mysql_install_db
sudo /usr/bin/mysql_secure_installation
sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
sudo apt-get install php5-cgi php5-cli php5-curl php5-common php5-gd php5-mysql
sudo service apache2 restart
```

# Make the Box as Small as possible

We're now going to clean up disk space on the VM so when we package it into a new Vagrant box, it's as clean as possible. First, remove APT cache

```
sudo apt-get clean
```

## Then, "zero out" the drive (this is for Ubuntu):

```
sudo dd if=/dev/zero of=/EMPTY bs=1M
```
```
sudo rm -f /EMPTY
```

## Lastly, let's clear the Bash History and exit the VM:

```
cat /dev/null > ~/.bash_history && history -c && exit
```

# Repackage the VM into a New Vagrant Box

We're now going to repackage the server we just created into a new Vagrant Base Box. It's very easy with Vagrant:

```
vagrant package --output mynew.box
```

# Add the Box into Your Vagrant Install

The previous command will have created a "mynew.box" file. You can technically put this wherever you want on your computer. Now, let's add this new Vagrant Box into Vagrant:

```
vagrant box add mynewbox mynew.box
```

This now will "download" the box into your Vagrant install allowing to initiate this from any folder, but before we do this, let's delete and remove the Vagrant file we built this box from.

```
vagrant destroy
```
```
rm Vagrantfile
```

## Initialize Your New Vagrant Box

We need to now initialize a Vagrant environment from our brand new box using the same command from earlier but referencing the new Box.

```
vagrant init mynewbox
```

## Customize Your New Vagrantfile

When you initialize the Vagrant environment, it creates a Vagrantfile for you (just like from before). Open the Vagrantfile and delete everything. You can use what was in there as a reference or just use Vagrant's Official Docs

# Create new box using existing setup

## Clean the app-get
```
sudo apt-get clean
```

## Clean the history and exit the box
```
cat /dev/null > ~/.bash_history && history -c && exit
```

## Create the box with Vagrantfile

```
vagrant package --vagrantfile Vagrantfile --output hyper.box
```
### Upload the box to the Vagrant Cloud

A [Manual](https://www.vagrantup.com/docs/cli/cloud.html) describes how we can achive this using `cli`

# Create Vagrant Box using .ova file

Sometimes distribution providers (such as UCS) only give you VirtualBox .ova files to test their software. Here is how you can easily and non-interactively import a .ova file into a .box for use with Vagrant.

```
$ VBoxManage import ./UCS-Virtualbox-Demo-Image.ova --vsys 0 --eula accept                                                                                                                                   
0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Interpreting /home/crohr/dev/ucs/./UCS-Virtualbox-Demo-Image.ova...                                                                                                                       
OK.                                                                                                                                                                                                        
Disks:  vmdisk1 53687091200     -1      http://www.vmware.com/interfaces/specifications/vmdk.html#streamOptimized       UCS-Demo-Image-virtualbox-disk1.vmdk    -1      -1                                 
...
0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Successfully imported the appliance.                           
```
## Then list your VMs to find the VM ID:

```
$ VBoxManage list vms
"UCS 4.1" {acef4c0a-35be-4640-a214-be135417f04d}
```
## You can now package that VM as a Vagrant box:

```
$ vagrant package --base acef4c0a-35be-4640-a214-be135417f04d --output UCS.box                                                                                                                             
==> acef4c0a-35be-4640-a214-be135417f04d: Exporting VM...                                                                                                                                                
==> acef4c0a-35be-4640-a214-be135417f04d: Compressing package to: /home/crohr/dev/ucs/UCS.box                                                                                           
```
## And add it to the list of your local Vagrant boxes:

```
$ vagrant box add UCS.box --name UCS
```

## Finally, you can create a Vagrantfile to use this box:
```
Vagrant.configure("2") do |config|
  config.vm.box = "UCS"
  # ...
end
```

And vagrant up!


# More resources

[1. CheatSheet and description](https://elatov.github.io/2014/06/upload-vagrant-box-to-the-vagrant-cloud/)

[2. Vagrant Snapshots](https://www.vagrantup.com/docs/cli/snapshot.html)

[3. Creating Base boxes](https://www.vagrantup.com/docs/virtualbox/boxes.html)

[4. CheatSheet from Linux Academy](https://linuxacademy.com/blog/linux/vagrant-cheat-sheet-get-started-with-vagrant/)
