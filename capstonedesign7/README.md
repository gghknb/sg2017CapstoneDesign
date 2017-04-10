1. Introduction
     This project measure temperatures by temperature sensor and arduino send temperature dats to
     my web server with http call and thing speak. 
     I can read temperatures by thing speak channel and web server([Web server Ip address:3000]/dump)

2. Install tools on Ubuntu
  (1) Install node.js
      sudo apt-get install build-essential checkinstall
      sudo apt-get install libssl-dev
      sudo apt-get install curl
      curl -o- https://raw.githubusercontent.com/crea…/…/v0.31.0/install.sh | bash
      relogin
      nvm install 7.8.0
      nvm use 7.8.0
      nvm alias default node
      
      or following manual : http://www.hostingadvice.com/how-to/install-nodejs-ubuntu-14-04/#node-version-manager
  (2) Install express framework
      mkdir myapp
      cd myapp
      npm init
      npm install express --save
      npm install express
      
      or following manual : https://expressjs.com/en/starter/installing.html
  (3) Install mysql
      sudo apt-get update
      sudo apt-get install mysql-server
      sudo mysql_secure_installation
      sudo mysql_install_db
      mysql --version
  (4) Make sensor table
      mysql -u root -p       //login mysql
      create database data;
      use data;
        create table sensors (
        id int not null auto_increment primary key,
        seq int(10) unsigned,
        device decimal(4,0) unsigned,
        unit decimal(2,0) unsigned,
        type char(1),
        value decimal(10,4),
        ip char(15),
        time TIMESTAMP DEFAULT CURRENT_TIMESTAMP);
        CREATE USER 'sensor'@'localhost' IDENTIFIED BY 'sensor.data';
        GRANT ALL PRIVILEGES ON data.* TO 'sensor'@'localhost';
        FLUSH PRIVILEGES;
        SET PASSWORD FOR 'sensor'@'localhost' = PASSWORD('mypassword');     // setting your password to 'mypassword'

3. Execute
Upload capstonedesign7.ino to your nodemcu using Arduino sketch.
Type following command in your ubuntu server.
  node cap7.js 
If console print Done insert then this temperature data send to your web server successly.
If you refresh your web server then print 'dump complete' on your Ubuntu console.
Type fllowing command in your ubuntu server then you can see your temperature data
  tail -f   LOG.txt   
