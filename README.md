# dahdi
******************************
Step 1:  Uninstall the old dahdi drivers
******************************
ssh the server via putty 
First check the dahdi modules installed by running below command
'''lsmod | grep dahdi

you will get the below output 




Now uninstall all the modules which shown in above pic

'''modprobe -r wctc4xxp wctdm24xxp wcte12xp xpp dahdi_transcode wcb4xxp
'''modprobe -r wctdm wcfxo wctdm24xxp wcte11xp wct1xxp wcte12xp
'''modprobe -r dahdi_voicebus wct4xxp wctdm24xxp dahdi



******************************
Step 2:  Downloading the latest dahdi driver
******************************
```console
wget http://downloads.asterisk.org/pub/telephony/dahdi-linux-complete/dahdi-linux-complete-current.tar.gz
tar -xvzf dahdi-linux-complete-current.tar.gz
cd dahdi-linux-complete-2.10.1+2.10
make clean
make all
make install
make config
```

******************************
Step 3:  Configuring the dadhi
******************************
```console
dahdi_genconf -v
dahdi_cfg -v
/etc/init.d/dahdi restart
```

if you are using any digium card follow the below link

```console
http://striker24x7.blogspot.in/2013/12/how-to-configure-digium-te133-and-te134.html
http://striker24x7.blogspot.in/2014/08/configuring-digium-te235-and-te435-card.html
```

******************************
Step 4:  Troubleshoot
******************************
If still  dahdi version show old version after running dahdi_cfg -v
then follow the below steps


Then run the below commands to remove the old version
```console
rpm -qa | grep "dahdi"
```

check the outputs , below is the one i got frommy server
```console
rpm -qa | grep "dahdi"
  dahdi-linux-devel-2.4.1-70.el5
 dahdi-tools-2.4.1-68.el5
 dahdi-linux-2.4.1-70.el5
 dahdi-linux-kmdl-2.6.18-238.9.1.el5.goPAE-2.4.1-70.RHL5
```

run the below command for the each package outputs

```console
rpm -e --nodeps "dahdi-linux-devel-2.4.1-70.el5"
rpm -e --nodeps "dahdi-tools-2.4.1-68.el5"
rpm -e --nodeps "dahdi-linux-2.4.1-70.el5"
rpm -e --nodeps "dahdi-linux-kmdl-2.6.18-238.9.1.el5.goPAE-2.4.1-70.RHL5"
```


once done again follow the above steps to reinstall the dahdi latest

**************************
