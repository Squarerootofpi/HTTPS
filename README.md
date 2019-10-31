# HTTPS
This tutorial will show you how to get https running on your node.js project.

Implement the express_http_https.js server from the  code from github
You will need to create ssl server keys and put them into a ssl directory in order to make this work.
You can generate the keys with the following commands 

openssl genrsa -out server.pem 2048
openssl req -new -key server.pem -out server.csr
openssl x509 -req -days 365 -in server.csr -signkey server.pem -out server.crt
After this command completes, copy all of the server files into the ssl directory and move the server.pem file to server.key with the following commands:
mkdir ssl
cp server.* ssl
cd ssl
mv server.pem server.key
Your ssl directory should now contain the following files
server.crt server.csr server.key

Now enter the code from github (Links to an external site.) into a file, and run the file with node (using sudo node [filename] since you want it to run on port 80).
You will need to run as superuser 
sudo node [filename]
And make sure that port 80 and port 443 are open on your ec2 node.

What response do you get when you access the page https://yourIP/ through your browser? *If you're using Chrome you might get a warning about an unknown certificate... you can likely ignore it in this case.
