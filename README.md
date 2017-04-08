
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link rel="stylesheet" href="https://stackedit.io/res-min/themes/base.css" />

</head>
<body><div class="container"><h1 id="setting-up-iquidus-explorer">Setting up Iquidus Explorer</h1>

<p><div class="toc">
<ul>
<li><a href="#setting-up-iquidus-explorer">Setting up Iquidus Explorer</a></li>
<li><a href="#requirements">Requirements</a></li>
<li><a href="#1-set-up-your-server-1">1. Set up your Server</a><ul>
<li><a href="#11-ensure-you-have-a-suitable-ssh-client">1.1. Ensure you have a suitable SSH client</a></li>
<li><a href="#12-buy-a-5-per-month-instancedroplet">1.2. Buy a $5 per month Instance/Droplet</a></li>
<li><a href="#13-ssh-into-your-server-space">1.3. SSH into your server space</a></li>
</ul>
</li>
<li><a href="#2-inside-the-vps">2. Inside the VPS</a><ul>
<li><a href="#21-set-up-swap">2.1. Set up Swap</a></li>
<li><a href="#22-set-up-nodejs">2.2. Set up Nodejs</a></li>
<li><a href="#23-set-up-mongod-database">2.3. Set up Mongod (database)</a></li>
</ul>
</li>
<li><a href="#3-compile-dependencies-for-bdsm-fetish">3. Compile Dependencies for BDSM-FETISH</a><ul>
<li><a href="#31-git-clone-bdsm-fetish">3.1. Git Clone BDSM-FETISH</a></li>
</ul>
</li>
<li><a href="#4-mongo">4. Mongo </a></li>
<li><a href="#5-iquidus-eplorer">5. Iquidus Eplorer</a><ul>
<li><a href="#51-settingsjson">5.1 settings.json</a></li>
<li><a href="#52-favicon-and-logo">5.2. Favicon and Logo</a></li>
</ul>
</li>
<li><a href="#6-starting-the-explorer">6. Starting the Explorer</a><ul>
<li><a href="#61-crontab">6.1 Crontab</a></li>
<li><a href="#7-links">7. Links</a></li>
</ul>
</li>
</ul>
</div>
<hr>

<p>These are plain instructions, and intended for someone with basic knowledge of using a server and Linux (specifically Ubuntu 14 x, 64 bit). </p>

<p><strong>Each command starts on a separate line. </strong></p>

<p><strong>Press Enter after you have pasted into your client.</strong></p>

<hr>

<h1 id="requirements">Requirements</h1>

<p>Server <br>
Ubuntu <strong>14</strong>.0x 64 bit Package <br>
Nodejs <br>
Mongodb <br>
BDSM-FETISHd daemon</p>

<hr>

<h1 id="1-set-up-your-server">1. Set up your Server</h1>

<p>You can go the cheap way with an unmanaged plan. This is not recommended if you are not familiar with setting them up.</p>

<p>Your choice is <a href="https://www.vultr.com">Vultr</a> or <a href="https://www.digitalocean.com">Digital Ocean</a></p>

<p>Make sure you take up their new-user offers.</p>

<p>I will assume you go with Vultr, as they give you double the memory.</p>

<hr>

<h2 id="11-ensure-you-have-a-suitable-ssh-client">1.1. Ensure you have a suitable SSH client</h2>

<p>This is not a problem if you use a Linux OS. Windows users can use Putty, but there are other clients out there equally as good.</p>

<hr>

<h2 id="12-buy-a-5-per-month-instancedroplet">1.2. Buy a $5 per month Instance/Droplet</h2>

<blockquote>
  
</blockquote>

<ul>
<li>Ensure you enable IPv6 during this procedure</li>
<li>Choose Ubuntu 14 x 64 bit at $5</li>
<li>Pay by Paypal</li>
</ul>

<p>You will get a Public IP 4 address and password (Vultr will give you a password (management), Digi Ocean will email you one, which you have to change when you log on.</p>

<hr>

<h2 id="13-ssh-into-your-server-space">1.3. SSH into your server space</h2>

<p>For example</p>

<blockquote>
  <p>ssh root@45.46.47.48 <br>
  Copy paste your password (paste is a simple right-click with my SSH client)</p>
</blockquote>

<hr>

<h1 id="2-inside-the-vps">2. Inside the VPS</h1>

<p>i. First command:</p>

<blockquote>
  <p>sudo apt get-update</p>
</blockquote>

<p><strong>Remember to press “Enter” after each command</strong></p>

<hr>

<h2 id="21-set-up-swap">2.1. Set up Swap</h2>

<blockquote>
  <p>dd if=/dev/zero of=/mnt/myswap.swap bs=1M count=2000 <br><br>
  mkswap /mnt/myswap.swap <br><br>
  swapon /mnt/myswap.swap</p>
</blockquote>

<p>Add the settings to <strong>fstab</strong> using “nano” (<em>sudo apt-get install nano</em>) if it is not installed already.</p>

<blockquote>
  <p>nano /etc/fstab</p>
</blockquote>

<p>Paste the following line at the end of the file.</p>

<blockquote>
  <p>/mnt/myswap.swap none swap sw 0 0</p>
</blockquote>

<p>Press Ctrl and X together, just answer yes to saving the file.</p>

<hr>

<h2 id="22-set-up-nodejs">2.2. Set up Nodejs</h2>

<p>This is an old way, depreciated, but still works. It is simple:</p>

<blockquote>
  <p>curl -sL <a href="https://deb.nodesource.com/setup">https://deb.nodesource.com/setup</a> | sudo bash -</p>
  
  <p>sudo apt-get install nodejs</p>
  
  <p>sudo apt-get install build-essential</p>
</blockquote>

<p>(remember “enter” after each command)</p>

<p><strong>If “curl” is not installed</strong>:</p>

<blockquote>
  <p>sudo apt-get install curl</p>
</blockquote>

<h2 id="23-set-up-mongod-database">2.3. Set up Mongod (database)</h2>

<p><a href="https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/">Tutorial</a></p>

<p>Basically, you paste these commands:</p>

<blockquote>
  <p>sudo apt-key adv –keyserver hkp://keyserver.ubuntu.com:80 –recv 0C49F3730359A14518585931BC711F9BA15703C6</p>
  
  <p>echo “deb [ arch=amd64 ] <a href="http://repo.mongodb.org/apt/ubuntu">http://repo.mongodb.org/apt/ubuntu</a> trusty/mongodb-org/3.4 multiverse” | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list</p>
  
  <p>sudo apt-get update</p>
  
  <p>sudo apt-get install -y mongodb-org</p>
</blockquote>

 <p>Now just leave Mongod alone, you will start it up later.</p>

<hr>

<h1 id="3-compile-dependencies-for-bdsm-fetish">3. Compile Dependencies for BDSM-FETISH</h1>

<p>There are various you can use, but try this command:</p>

<blockquote>
  <p> sudo apt-get install git build-essential libssl-dev libboost-all-dev libqrencode-dev libdb++-dev libminiupnpc-dev qt-sdk -y</p>
</blockquote>

<p>It will take a few minutes to unpack</p>

<blockquote>
  <p>sudo apt-get update</p>
</blockquote>

<hr>

<h2 id="31-git-clone-bdsm-fetish">3.1. Git Clone BDSM-FETISH</h2>

<blockquote>
  <p>git clone <a href="https://github.com/bdsmc/bdsm-fetish-PoS-master.git">https://github.com/bdsmc/bdsm-fetish-PoS-master.git</a></p>
</blockquote>

<p>Shorten the directory name</p>

<blockquote>
  <p>mv bdsm-fetish-PoS-master bdsm</p>
</blockquote>

<p>cd into src</p>

<blockquote>
  <p>cd bdsm/src</p>
</blockquote>

<p>Compile</p>

<blockquote>
  <p>make -f makefile.unix</p>
</blockquote>

<p>Wait till finished, and strip the daemon (d), then start it.</p>

<blockquote>
  <p>strip BDSM-FETISHd</p>
  
  <p>./BDSM-FETISHd</p>
</blockquote>

<p>It will spit out a password and username and tell you to use /root/.BDSM-FETISH/BDSM-FETISH.conf</p>

<p>copy paste the password and username, make a note of them</p>

<blockquote>
  <p>nano /root/.BDSM-FETISH/BDSM-FETISH.conf</p>
</blockquote>

<p>paste the rpcusername and password into the empty document and add the rest of the .conf details</p>

<p>Use something like this:</p>

<blockquote>
  <p>daemon=1 <br>
  server=1 <br>
  txindex=1 <br>
  rpcusername=BDSM-FETISHrpc <br>
  rpcpassword=XXXXXXXXXXXXXXXXXXX <br>
  rpcallowip=127.0.0.1 <br>
  rpcport=8746</p>
</blockquote>

<p>Ctrl X, answer “yes” to save</p>

<blockquote>
  <p>cd <br>
  cd/src <br>
  ./BDSM-FETISHd</p>
</blockquote>

<p>The daemon starts, and index all the transactions, so will be slow. Just let it get on with it. It may take a few hours.</p>

<hr>

<h1 id="4-mongo">4. Mongo </h1>

<p>Start using Mongod. Simple commands:</p>

<blockquote>
  <p>cd <br>
  Mongo</p>
</blockquote>

<p>Mongo will respond, and you will give it two commands:</p>

<blockquote>
  <p>use explorerdb <br>
  db.createUser( { user: “iquidus”, pwd: “3xp!0reR”, roles: [ “readWrite” ] } )</p>
</blockquote>

<p>You can replace the “user” and “pwd” with whatever you want; e.g. “Yourname” and “SecretPassword.” <strong>Or you can leave it as it is seeing as this is your first go.</strong></p>

<p>You will have noticed Mongo has given you the symbol &gt; as a command prompt. You want to get rid of that now.</p>

<p>Just press at the same time:</p>

<blockquote>
  <p>Ctrl  C </p>
</blockquote>

<p>Mongo will say “Goodbye”</p>

<hr>

<h1 id="5-iquidus-eplorer">5. Iquidus Eplorer</h1>

<p>You need to clone the repository and install some node modules, as such:</p>

<blockquote>
  <p>git clone <a href="https://github.com/iquidus/explorer">https://github.com/iquidus/explorer</a> explorer</p>
  
  <p>cd explorer &amp;&amp; npm install –production</p>
</blockquote>

<p>Don’t worry about all the errors npm tells you about, it should just finish anyway unless you made a mistake somewhere else.</p>

<hr>



<h2 id="51-settingsjson">5.1 settings.json</h2>

<p>Now you need to set up the settings.json file. I have prepared one for you.</p>

<blockquote>
  <p>cd <br>
  cd explorer <br>
  wget <a href="https://github.com/bdsmc/logo/blob/master/settings.json">https://github.com/bdsmc/logo/blob/master/settings.json</a></p>
</blockquote>

<p>Make sure it is saved as settings.json</p>

<blockquote>
  <p>dir</p>
</blockquote>

<p>if it is called something else: </p>

<blockquote>
  <p>mv whateverfile settings.json <br>
  dir</p>
</blockquote>

<p>It should now be called settings.json</p>

<p><strong>The only changes you need to make are to (1). the rpc password (I assume you used BDSM-FETISHrpc as the username; and (2) If you changed the db settings from “user: “iquidus”, pwd: “3xp!0reR” to your own, replace the ones in the .json file</strong></p>

<blockquote>
  <p>Ctrl  X</p>
</blockquote>

<p>Answer “yes” to saving file as settings.json</p>

<h2 id="52-favicon-and-logo">5.2. Favicon and Logo</h2>

<blockquote>
  <p>cd <br>
  cd explorer/public <br>
  rm -r favicon.ico <br>
  wget <a href="https://github.com/bdsmc/logo/blob/master/favicon.ico">https://github.com/bdsmc/logo/blob/master/favicon.ico</a> <br>
  mv filename.icon favicon.ico</p>
  
  <p>cd images <br>
  rm -r logo.png <br>
  wget <a href="https://github.com/bdsmc/logo/blob/master/logo.png">https://github.com/bdsmc/logo/blob/master/logo.png</a> <br>
  mv filename.png logo.png</p>
  
  <p>cd</p>
</blockquote>

<p>You should have “Screen” already installed. But you can test whether it is there easily:</p>

<blockquote>
  <p>sudo apt-get install screen</p>
</blockquote>

<p>It will either install it, or tell you that you have the latest version.</p>

<hr>

<h1 id="6-starting-the-explorer">6. Starting the Explorer</h1>

<p>The daemon should be running already (with txindex=1), and Mongo should also be running in the background.</p>

<blockquote>
  <p>cd <br>
  cd explorer <br>
  screen -S explorer <br>
  npm start</p>
</blockquote>

<p>Let it start and then remove yourself from the running process with by pressing the following keys together:</p>

<blockquote>
  <p>Ctrl  A  D  </p>
</blockquote>

<hr>

<h2 id="61-crontab">6.1 Crontab</h2>

<p>You need to set up a Cron, which is simple:</p>

<blockquote>
  <p>crontab -e</p>
</blockquote>

<p>(enter)</p>

<p>You may be asked which editor you want to use, so just choose “nano”</p>

<p>At the bottom of the page, paste:</p>

<blockquote>
  <p><em>/1 </em> * * * cd /root/explorer &amp;&amp; /usr/bin/nodejs scripts/sync.js index update &gt; /dev/null 2&gt;&amp;1 <br>
  <em>/5 </em> * * * cd /root/explorer &amp;&amp; /usr/bin/nodejs scripts/peers.js &gt; /dev/null 2&gt;&amp;1</p>
</blockquote>

<p>We are missing out this cron because of Cryptopia, so we cannot link to an exchange. <strong>Do not insert it.</strong></p>

<blockquote>
  <p><em>*/2 </em> * * * cd /root/explorer &amp;&amp; /usr/bin/nodejs scripts/sync.js market &gt; /dev/null 2&gt;&amp;1*</p>
</blockquote>

<p>It can be used if and when you pay 0.10 BTC to Yobit. You would also change the settings.json file with the new information.</p>

<p>If you followed the instructions, the explorer will be synching, and it will take some time.</p>

<p>You should see it at your server url. For example:</p>

<p>45.46.47.48:3001</p>

<p>Some hours later it will be synched, just don’t interfere with the process.</p>

<p>Exit your server</p>

<blockquote>
  <p>cd <br>
  exit</p>
</blockquote>



<h2 id="7-links">7. Links</h2>

<p>It is recommended you read up at both these, but they will confuse you if you do it while following this guide. Check them later.</p>

<p><a href="https://github.com/iquidus/explorer">Iquidus Github</a></p>

<p><a href="https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/">Mongodb Community Edition 3.4</a></p></div></body>
</html>
