# Blynk server
Blynk Server is an Open Source [Netty](https://github.com/netty/netty)-based Java server, responsible for forwarding 
messages between Blynk mobile application and various microcontroller boards (i.e. Arduino, Raspberry Pi. etc).

Download latest server build:

[Download Blynk Server >](https://github.com/blynkkk/blynk-server/releases)

## Requirements
Java 8 required. (OpenJDK, Oracle). 

[How to install Java](http://docs.blynk.cc/#blynk-server-how-to-run-local-blynk-server-install-java-on-ubuntu).

## How to run local Blynk Server
By default, mobile application use 8443 port and is based on SSL/TLS sockets. Default hardware port is 8442 and 
is based on plain TCP/IP sockets.

### Quick Local Server launch

1. Make sure you are using Java 8

	```
	java -version
	Output: java version "1.8.0_40"
	```
2. Navigate to the folder where ```.jar``` file is. For example:
	
	```
	cd Users/User/Blynk/Server 
	```


3. Launch Blynk server.

	```
	java -jar server-0.9.1.jar -dataFolder /path
	```
	
	By default server uses these ports:
	- Hardware: 8442 
	- Blynk App: 8443 (SSL port)
        
<span style="color:#24C48C" >**That's it!**</span>
 
You won't see any output, because all the logging is done within same folder in ```./logs/blynk.log``` file.

### Launch Blynk Server on Raspberry Pi

1. Login to Raspberry Pi via ssh;
2. Install Java 8: 
        
		sudo apt-get install oracle-java8-jdk
        
3. Make sure you are using Java 8:

        java -version
        Output: java version "1.8.0_40"
        
4. Download Blynk server .jar file (or manually copy it to raspberry via ssh and scp command): 
   
        wget "https://github.com/blynkkk/blynk-server/releases/download/v0.9.1/server-0.9.1.jar"

5. Run the server on default ```hardware port 8442``` and default ```application port 8443``` (SSL port)

        java -jar server-0.9.1.jar -dataFolder /home/pi/Blynk        
        
That's it! You won't see any output because all the logging is done within same folder in ```./logs/blynk.log file.```
        
+ To enable server auto-restart, find /etc/init.d/rc.local file and add a line:

        java -jar /home/pi/server-0.9.1.jar -dataFolder /home/pi/Blynk &

                
### App and sketch changes

To connect Blynk App to your local server you need to set up a custom server during login. Set up IP address and PORT (should be 8443 by default)

<img src="images/login.png" style="width: 200px;"/>  <img src="images/custom.png" style="width: 200px;"/>

+ If you are using Ethernet connection, in the Ethernet example sketch change:

	```
	Blynk.begin(auth);
	```
 
	to
	
	```
	Blynk.begin(auth, "your_host"); //or
	Blynk.begin(auth, IPAddress(xxx,xxx,xxx,xxx));
	```
	


        
+ If you are connecting over WiFi, make edits in the WiFi example sketch. Change

   ```     
	Blynk.begin(auth, SSID, pass));
	```
	to
	
	```
	Blynk.begin(auth, SSID, pass, "your_host"); //or
	Blynk.begin(auth, SSID, pass, IPAddress(XXX,XXX,XXX,XXX));
	```
	
	
        
+ If you are connected over USB when running ```blynk-ser.sh``` provide ```-s``` option with address of your local server:

	```
	./blynk-ser.sh -s you_host_or_IP
	```     

## Advanced local server setup
If you need more flexibility, you can extend server with more options by creating server.properties file in same folder as server.jar. 
Example could be found [here](https://github.com/blynkkk/blynk-server/blob/master/server/tcp-server/src/main/resources/server.properties).
server.properties options:

+ Application port

        app.ssl.port=8443
        
+ For simplicity Blynk already provides server jar with build-in SSL certificates, so you have working server 
out of the box via SSL/TLS sockets. But as certificate and it's private key is in public, this is very unsecure. 
In order to fix that, you will need to provide your own certificates and change properties with path to your 
certificates, private key and it's password. 

	See how to generate self-signed certificates [here](http://docs.blynk.cc/#blynk-server-how-to-run-local-blynk-server-generate-ssl-certificates)

	Points to certificate and key that placed in same folder as running jar:
	
    ```    
    server.ssl.cert=./server_embedded.crt
    server.ssl.key=./server_embedded.pem
    server.ssl.key.pass=pupkin123
    ```

+ Hardware port

        hardware.default.port=8442

+ User profiles folder. Folder in which all users profiles will be stored. By default System.getProperty("java.io.tmpdir")/blynk used. Will be created if not exists

	data.folder=/tmp/blynk

+ Folder for all application logs. Will be created if it doesn't exist

        logs.folder=./logs

+ Log debug level. Possible values: trace|debug|info|error. Defines how precise logging will be. From left to right -> maximum logging to minimum

        log.level=trace

+ Maximum allowed number of user dashboards.

        user.dashboard.max.limit=10

+ 100 Req/sec rate limit per user.

        user.message.quota.limit=100

+ In case user exceeds quota limit - response error returned only once in specified period (in Millis).

        user.message.quota.limit.exceeded.warning.period=60000

+ Maximum allowed user profile size. In Kb's.

        user.profile.max.size=128

+ Maximum allowed number of notification queue. Queue responsible for processing email, pushes, twits sending. Because of performance issue - those queue is processed in separate thread, this is required due to blocking nature of all above operations. Usually limit shouldn't be reached
        
        notifications.queue.limit=10000

+ Period for flushing all user DB to disk. In millis

        profile.save.worker.period=60000

+ Specifies maximum period of time when application socket could be idle. After which socket will be closed due to non activity. In seconds. Leave it empty for infinity timeout

        app.socket.idle.timeout=600

+ Specifies maximum period of time when hardware socket could be idle. After which socket will be closed due to non activity. In seconds. Leave it empty for infinity timeout

        hard.socket.idle.timeout=15
        
+ Mostly required for local servers setup in case user want to log raw data in CSV format. See [raw data](http://docs.blynk.cc/#blynk-server-how-to-run-local-blynk-server-raw-data-storage) section for more info.
        
        enable.raw.data.store=true
        
+ Comma separated list of users allowed to create accounts. Leave it empty if no restriction required.
        
        allowed.users.list=allowed1@gmail.com,allowed2@gmail.com
        
### Enabling mail on Local server
In order to enable mail notifications on Local server you need to provide own mail credentials. To do that you need to create file "mail.properties" within same folder where server.jar is.
Mail properties:

```
mail.smtp.auth=true
mail.smtp.starttls.enable=true
mail.smtp.host=smtp.gmail.com
mail.smtp.port=587
mail.smtp.username=YOUR_EMAIL_HERE
mail.smtp.password=YOUR_EMAIL_PASS_HERE
```
        
See example [here](https://github.com/blynkkk/blynk-server/blob/master/server/notifications/mail-notifications/src/main/resources/mail.properties).

NOTE: you'll need to setup Gmail to allow less secured applications. Go [here](https://www.google.com/settings/security/lesssecureapps) and then click "Allow less secure apps".


### Raw data storage
By default, raw data storage is enabled. Every 'write' ```Blynk.virtualWrite()``` command will be stored on disk. 
The default path is "data" folder within [data.folder](http://docs.blynk.cc/#blynk-server-how-to-run-local-blynk-server-advanced-local-server-setup) property of server properties.

File name format is: 
        
    dashBoardId_pin.csv

Example:
 
    data/1_v5.csv
        
It means that raw data from Virtual Pin 5 of dashboard with ID 1 is stored
in 1_v5.csv

Data format is:

    value,timestamp
        
Example:

    10,1438022081332
        
Where 10 - pin value, and 1438022081332 - difference(in milliseconds) between current time and midnight, January 1, 1970 UTC 

Raw data files are rotated every day and gzipped.

**WARNING**: It will be changed soon. 

### Generate SSL certificates

+ Create key
        
        openssl genrsa -out server.key 2048
        
+ Create new cert request
        
        openssl req -new -out server.csr -key server.key

+ Generate self-signed request

        openssl x509 -req -days 1825 -in server.csr -signkey server.key -out server.crt
        
+ Convert server.key to PKCS#8 private key file in PEM format

        openssl pkcs8 -topk8 -inform PEM -outform PEM -in server.key -out server.pem
        
WARNING: in case you connect hardware via [USB script](https://github.com/blynkkk/blynk-library/tree/master/scripts) you have to provide an option '-s' pointing to "common name" (hostname) you did specified during certificate generation.
        
As output you'll retrieve server.crt and server.pem files that you need to provide for server.ssl properties.

### Install Java on Ubuntu

    sudo apt-add-repository ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get install oracle-java8-installer

### Behind WiFi router
If you want to run Blynk server behind WiFi-router and want it to be accessible from the Internet, you have to add port-forwarding rule on your router. This is required in order to forward all of the requests that come to the router within the local network to Blynk server.
