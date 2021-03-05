<link rel="stylesheet" type="text/css" media="all" href="../style/main.css" />

# installation

## Windows
https://nodejs.org/zh-tw/download/

> LTS 64-bit or Docker Image
> reboot

    node --version
    npm --version

## Linux
https://github.com/nodesource/distributions

### Ubuntu 20.04 (Focal Fossa)

    curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
    sudo apt-get install -y nodejs
    
    sudo reboot
    node --version
    npm --version

or

    wget https://deb.nodesource.com/setup_lts.x | sudo -E bash -
    sudo apt-get install -y nodejs

    sudo reboot
    node --version
    npm --version

# Basic Operating

## Initial Project

    npm init -y

## Find Installed Package

    npm ls
    npm ls -g

## Some Useful Package
<font class="--red">**[WARNING!]**</font> Please Select Package what you used!!

    npm i express
    npm i express session
    npm i mysql2
    npm i ejs
    npm i multer
