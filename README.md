# osinttw

Phishing OSINT MODULE    


Authors: (@networkseg1) - seguridadxredes[at]gmail.com
Version 1.0.0


DESCRIPTION


Python script to feed a Database with information related to phishing. 



** osint-tw.py: Python script to connect to Twitter Streamming API, downloading english or spanish phishing tweets and store them into a MariaDB in real time.

** database_osint.py: module to setup your Database parameters. This module is used inosint-tw.py.

** DBosint_tw.sql: a sql file to create the OSINT database and all the tables needs.

** twd.sh: Bash script to run osint-tw.py as a daemon. This script calls start_tw.sh script.



REQUIREMENTS
============================================

Debian -> Tested on Debian 9 64bits and python 3.4+


OSINT MODULE INSTALLATION


Step 1: Run the script: setup.sh    (Installation Path: /opt/twosint/)
______________________________________________________________________________________         

This script installs and setup:
--> All the needs debian and python packages.
--> A virtual version 3 python environment under /opt/twosint folder.
--> The MariaDB Database and create the osint DB and its tables. 
--> A crontab to improve our phishing collecting.

Besides:
--> Copy all python scripts  under the /opt/twosint folder.
--> Copy the traphuman-twd.sh daemon to /usr/sbin/


Step 2: SETUP YOUR OWN TWITTER API
____________________________________

GET your token Tweeter API keys from: https://apps.twitter.com/ - Create New App and fill the
information.

Open the App page and click in Keys and Access Token.
You will need:
consumer_key
consumer_secret
access_token
access_secret

-->  Edit /opt/twosint/osint-tw.py and set your own API Keys parameters.


Step 3: Setup your own Database parameters
___________________________________________

--> Edit /opt/twosint/lib/python/site-package/database_osint.py and set you own Database information. 
The default parameters will work but we suggest you to use another user/pass data.



Step 4: START osint-tw
______________________
 
/usr/sbin/twd.sh start

The script will start to collecting phishing tweets.
During the installation a crontab is setup. Review the crontab if you wish adjust it.


Step 5: Check the Logfile
_________________________

/var/log/twd.log

Now, you could check your logfile: /var/log/twd.log for some issue, if everything is ok, you will see a line like this one:
     https://stream.twitter.com:443 "POST /1.1/statuses/filter.json?delimited=length HTTP/1.1" 200 None


OTHER INFORMATION
=================

Module installation path
________________________

/opt/twosint/


Crontab installed
_________________

05 02 osint-twd.sh stop
05 07 osint-twd.sh start

