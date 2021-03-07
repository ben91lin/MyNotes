# installation

## Windows
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/

https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#configure-a-windows-service-for-mongodb-community-edition

> Download .msi installer.\
> Choose the version you wanted.\
> \>\> Custom \>\> ~~Disable Install MongoDB Compass~~ \> Install

~~ps. The MongoDB Compass GUI have some JS error, I don't know if they fixed it or not.~~

### Configure Service
If you install MongoDB 4.4 and choose "Mongo Service", the servce will started default.\
If you want to change the db/log destination, try this.

> Configure Dest: \<install directory\>\bin\mongod.cfg\
> database path \> dbPath\
> log path \> path

Save it and restart the service.

## Ubuntu
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/

    wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list 
    # [Attention!] this command line used in Ubuntu 20.04
    sudo apt-get update
    sudo apt-get install -y mongodb-org
    sudo systemctl start mongod
    sudo systemctl status mongod
    mongo

# Use

## with Node.js
https://www.npmjs.com/package/mongodb
https://mongodb.github.io/node-mongodb-native/driver-articles/mongoclient.html