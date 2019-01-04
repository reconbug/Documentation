# Install GO language on Linux

## Install prerequisites

```
sudo apt install wget git
```

## Install GO using GO Installer

```
wget -q https://storage.googleapis.com/golang/getgo/installer_linux
```

### Set the permissions

```
chmod +x installer_linux
```
### Install GO

```
./installer_linux
```

Open a new Shell or execute the bash_profile file

### Verify the installation

```
go version
```

### Execute the hello-World

```
go get github.com/golang/example/hello
```
```
hello
```

