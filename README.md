# HTTPS
This tutorial will show you how to get https running on your node.js project.

Create a "server.js" file with the following content
```
var express = require('express');
var https = require('https');
var http = require('http');
var fs = require('fs');
var app = express();
var options = {
    host: '127.0.0.1',
    key: fs.readFileSync('ssl/server.key'),
    cert: fs.readFileSync('ssl/server.crt')
  };
http.createServer(app).listen(80);
https.createServer(options, app).listen(443);
app.get('/', function(req, res){
  res.send('Hello from Express');
});
```
You will need to create ssl server keys and put them into a ssl directory in order to make this work.
You can generate the keys with the following commands 
```
openssl genrsa -out server.pem 2048
openssl req -new -key server.pem -out server.csr
openssl x509 -req -days 365 -in server.csr -signkey server.pem -out server.crt
```
After this command completes, copy all of the server files into the ssl directory and move the server.pem file to server.key with the following commands:
```
mkdir ssl
cp server.* ssl
cd ssl
mv server.pem server.key
```
Your ssl directory should now contain the following files
server.crt server.csr server.key

Now run the server in "server.js".  You need to stop the httpd web server that is currently running on port 80.  You will need to use sudo to start your server since it will be running on port 80 and 443.
```
sodo service httpd stop
sudo node server.js
```
And make sure that port 80 and port 443 are open on your ec2 node.

What response do you get when you access the page https://yourIP/ through your browser? *If you're using Chrome you might get a warning about an unknown certificate... you can likely ignore it in this case.
