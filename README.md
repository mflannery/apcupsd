# Installing and configuring apcupsd on fedora 35

From - http://www.apcupsd.org/

Install apcupsd:

```
  $ sudo dnf install apcupsd
```

Start apcupsd:

```
  $ sudo systemctl enable --now apcupsd.service
```

Verify apcupsd is running with:

```
  $ sudo systemctl status apcupsd.service
```

You should see output similar to the following:

```
  $ sudo systemctl status apcupsd.service 
```  
```
  ● apcupsd.service - APC UPS Power Control Daemon for Linux
     Loaded: loaded (/usr/lib/systemd/system/apcupsd.service; enabled; vendor p>
     Active: active (running) since Sun 2022-01-23 13:51:56 EST; 7min ago
    Process: 1415535 ExecStartPre=/bin/rm -f /etc/apcupsd/powerfail (code=exite>
   Main PID: 1415536 (apcupsd)
      Tasks: 3 (limit: 38340)
     Memory: 664.0K
        CPU: 40ms
     CGroup: /system.slice/apcupsd.service
             └─1415536 /sbin/apcupsd -b -f /etc/apcupsd/apcupsd.conf
```

Now that apcupsd is running check the status:

```
    $ apcaccess status
```
```
    APC      : 001,036,0879
    DATE     : 2022-01-23 14:01:48 -0500  
    HOSTNAME : fedora
    VERSION  : 3.14.14 (31 May 2016) redhat
    UPSNAME  : fedora
    CABLE    : USB Cable
    DRIVER   : USB UPS Driver
    UPSMODE  : Stand Alone
    STARTTIME: 2022-01-23 13:51:56 -0500  
    MODEL    : Back-UPS NS 1500M2 
    STATUS   : ONLINE 
    LINEV    : 122.0 Volts
    LOADPCT  : 5.0 Percent
    BCHARGE  : 100.0 Percent
    TIMELEFT : 131.3 Minutes
    MBATTCHG : 5 Percent
    MINTIMEL : 3 Minutes
    MAXTIME  : 0 Seconds
    SENSE    : Medium
    LOTRANS  : 88.0 Volts
    HITRANS  : 142.0 Volts
    ALARMDEL : No alarm
    BATTV    : 27.4 Volts
    LASTXFER : No transfers since turnon
    NUMXFERS : 0
    TONBATT  : 0 Seconds
    CUMONBATT: 0 Seconds
    XOFFBATT : N/A
    SELFTEST : NO
    STATFLAG : 0x05000008
    SERIALNO : 3B1827X30213  
    BATTDATE : 2018-07-06
    NOMINV   : 120 Volts
    NOMBATTV : 24.0 Volts
    NOMPOWER : 900 Watts
    FIRMWARE : 957.e3 .D USB FW:e3
    END APC  : 2022-01-23 14:01:52 -0500
```
This server will now shutdown if the batter power level goes below 5% or 3 minutes of run time.  
I have added a doshutdown script that will turn off my synology server as well as my fedora server in the event the battery runs out of power. Copy doshutdown to /etc/apcpusd and edit as appropriate.  
