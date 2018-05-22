```fix
Pre-requisites:
1. new VPS Ubuntu 16.04 (DON'T TRY THIS SCRIPT WITH OTHER MASTERNODE COINS INSTALLED or accept unpredictable results)
2. VPS IP Address
3. follow the official setup guide to page 2 (https://crowdcoin.site/guides/QUICK_CROWDCOIN_MASTERNODE_SETUP.pdf)
to get the masternode private key and the TxID and TxIndex

Please copy and paste (or type) everything exactly as written behind "type:" to the end of the line.

Step 0) Type: apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && reboot
		if prompted "tools.conf (Y/I/N/O/D/Z) [default=N] ?" just press enter
Step 1) Type: git clone https://github.com/KingSlayerMN/vps.git && cd vps
Step 2) Type: ./install.sh -p crowd -c 1 -n 4 -s 
Step 3) Once install script has finished type: nano /etc/masternodes/crowd_n1.conf
Step 4) add your IP address here bind=[#NEW_IPv4_ADDRESS_FOR_MASTERNODE_NUMBER:::1]:12875 and place your 
		masternode private keys here masternodeprivkey=HERE_GOES_YOUR_MASTERNODE_KEY_FOR_MASTERNODE_crowd_1
Step 5) get current addnodes from https://www.cryptopia.co.nz/CoinInfo, type CRC in the search field and 
		click on "Connections" of Crowdcoin. 
		Select the addnodes show on the left into the clipboard, paste them with into the crowd_n1.conf, 
		save the conf-file
Step 6) To activate the masternode type: activate_masternodes_crowd
Step 7) To activate Sentinel 
		Type: export SENTINEL_CONFIG=/usr/share/sentinel/crowd1_sentinel.conf; /usr/share/sentinelenv/bin/python /usr/share/sentinel/bin/sentinel.py
Step 8) If it works without error, add that command as cronjob: 
		Type: crontab -e 
		and place the string below in one line at the bottom of the file:
		Type: * * * * * export SENTINEL_CONFIG=/usr/share/sentinel/crowd1_sentinel.conf; /usr/share/sentinelenv/bin/python /usr/share/sentinel/bin/sentinel.py 2>&1 >> /var/log/sentinel/sentinel-cron.log
Step 9) to make the command line interface (crowdcoin-cli) easier accessible add the string below to your .bashrc 
		type: echo "alias crc1='crowdcoin-cli -conf=/etc/masternodes/crowd_n1.conf $1'" >> ~/.bashrc
Step 10) to activate the alias added in step 9) type: . ~/.bashrc
Done!

Configuration files are in: /etc/masternodes
Data are in: /var/lib/masternodes

Instead of crowdcoin-cli masternode status you can now type 
crc1 masternode status, 
crc1 getinfo, 
crc1 mnsync status, 
crc1 getblockcount
If you wish the make use of watch you need to include the path to the conf-file together with crowdcoin-cli
eg. watch crowdcoin-cli -conf=/etc/masternodes/crowd_n1.conf mnsync status

Wait until "crc1 mnsync status" output is like 
{
  "AssetID": 999,
  "AssetName": "MASTERNODE_SYNC_FINISHED",
  "Attempt": 0,
  "IsBlockchainSynced": true,
  "IsMasternodeListSynced": true,
  "IsWinnersListSynced": true,
  "IsSynced": true,
  "IsFailed": false
}

Continue with the official setup guide at page 6 "STARTING YOUR MASTERNODE (Windows)"
Omit the chapter "Test and Troubleshooting" in the official setup guide.
```