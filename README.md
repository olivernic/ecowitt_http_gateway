# ecowitt_http_gateway
<i>Simple HTTP gateway that receives data from <b>GW1000 with Ecowitt protocol</b> and resend data to Meteotemplate or csv, json, ecc.</i><br><br>
<b><i>Install this gateway if you have a web server at home, like a Raspberry or something where you want to store weather data</b></i>
  
The GW1000 allows sending data both to Ecowitt.net and Wunderground, even to an external site as long as you select one
of the two previous protocols. <br>
We know the Wunderground protocol and we know that it don't send UV and PM2.5 data, nor ground temperature or
other additional sensors, so you need to select the Ecowitt protocol.

Now to permit this script to work, we need a web server to which the GW1000 need to send data.

<b>REQUIREMENTS</B>

The web server must have these possibilities:
- to create a directory named <b>/data/report</b> (es. /var/www/html/data/report )
- in this directory will be put the <b>index.php</b> file 

So, the web site will look like: http://192.168.1.4/data/report/index.php<br>
In the GW1000 configuration it will be necessary writing only the IP address, es. 192.168.1.4 and specify the update rate.

I recommend having this web server on a raspberry, in the same network of the GW1000, so the script can also be used to store data without losing them in case of Internet connection failure<br> 
When the GW1000 will contact the web site, the index.php will do these functions:

1) creates a .JSON file in /var/log/ecowitt ( overwrited every update, contains only last data )<br>
2) creates a .CSV file in /var/log/ecowitt ( appended every update, contains all data )<br>
3) converts in metric all data a resend to a Meteotemplate web site on Internet<br>

<b>SIMPLE INSTALL GUIDE</b>:
- Install Apache
- Install PHP
- Install jq ( for JSON query )
- Create directory Es. /var/www/html/data/report/
- Create /var/log/ecowitt with chmod 777
- Put file: index.php 
- Configure index.php
- Configure GW1000 to send data to you server

Look in /var/log/ecowitt to read fields using 'jq'

jq -r '.tempc' weather_XXXXXXXXXXXXXXXX.json

<b>NEXT STEPS of IMPROVEMENTS</b>:
- improve the writing of .CSV file
- send the .JSON file on an FTP server
- create a connection to weewx

# ecowitt Meteotemplate plugin
<i>Simple plugin for [Meteotemplate](http://www.meteotemplate.com/), wonderful template developed by Jachym.</i><br><br>
<b><i>Install this plugin if you don't want to install the previous gateway, or you only need to update your Meteotemplate web site. You will not store any data locally in your network</b></i>

- Download it from the repository
- Install it in the plugin directory of your template website, just like another plugin
- Go in the Plugin setup page, via Admin Panel of Meteotemplate
- Configure it
- Configure the GW1000 with the setup you read in the Plugin page

