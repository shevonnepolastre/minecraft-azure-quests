# Copying the World Folder Over 

I decided to use AzCopy so I had to install it.  I SSHed into my Azure VM and installed it using WGet
```
wget https://aka.ms/downloadazcopy-v10-linux -O azcopy.tar.gz
tar -xvf azcopy.tar.gz
sudo cp ./azcopy_linux_amd64*/azcopy /usr/bin/
azcopy --version

```

I then used the AzCopy command: 

```powershell

azcopy copy azurevmdirectory blobstorageappendedwithSAS

```

I got the following output:

```
mcadmin@minecraft-vm:~$ azcopy copy "/home/mcadmin/world/*" "https://storageaccount.blob.core.windows.net/worldstorageSAS" --recursive=true
INFO: Scanning...
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support

Job a1afd194-60e7-db4f-79d3-17a4b97a65a1 has started
Log file is located at: /home/mcadmin/.azcopy/a1afd194-60e7-db4f-79d3-17a4b97a65a1.log


100.0 %, 51 Done, 0 Failed, 0 Pending, 0 Skipped, 51 Total, 2-sec Throughput (Mb/s): 219.6323


Job a1afd194-60e7-db4f-79d3-17a4b97a65a1 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 51
Number of Folder Property Transfers: 0
Number of Symlink Transfers: 0
Total Number of Transfers: 51
Number of File Transfers Completed: 51
Number of Folder Transfers Completed: 0
Number of File Transfers Failed: 0
Number of Folder Transfers Failed: 0
Number of File Transfers Skipped: 0
Number of Folder Transfers Skipped: 0
Total Number of Bytes Transferred: 55028831
Final Job Status: Completed
```


Used grep to search for "success" and got the following:

```

mcadmin@minecraft-vm:~$ grep -i success /home/mcadmin/.azcopy/8e6fd446-8a25-f24a-6201-d52b644a87d2.log
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.410184ms, OpTime=21.550536ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/7.514217ms, OpTime=22.197845ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/39.9µs, OpTime=21.827739ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/24.8µs, OpTime=22.707953ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/12.936801ms, OpTime=22.731553ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/43.001µs, OpTime=23.564167ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/4.577671ms, OpTime=23.631068ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/2.058532ms, OpTime=24.606183ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.845391ms, OpTime=25.476596ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/16.620758ms, OpTime=25.374395ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/4.072563ms, OpTime=26.013105ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/4.374468ms, OpTime=25.860002ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/3.131549ms, OpTime=25.892303ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.049179ms, OpTime=26.902419ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/3.453654ms, OpTime=26.249608ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.596487ms, OpTime=26.621414ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.533486ms, OpTime=27.594729ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.844791ms, OpTime=27.462728ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/4.685773ms, OpTime=28.106038ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/6.657804ms, OpTime=28.581345ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/2.866545ms, OpTime=28.796649ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/2.805744ms, OpTime=27.840033ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/3.565055ms, OpTime=27.935534ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/2.284736ms, OpTime=28.278541ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/2.707243ms, OpTime=28.684647ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/4.133364ms, OpTime=30.269571ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/3.80976ms, OpTime=30.987883ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/3.348352ms, OpTime=9.372446ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/3.013647ms, OpTime=6.296598ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/3.738058ms, OpTime=10.27996ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/6.185996ms, OpTime=12.765699ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.351383ms, OpTime=8.191227ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/6.912107ms, OpTime=9.545048ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/4.807974ms, OpTime=9.68105ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/5.920292ms, OpTime=10.188059ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/9.713051ms, OpTime=13.191106ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/12.8455ms, OpTime=19.560004ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/12.19059ms, OpTime=18.397087ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/19.376802ms, OpTime=24.905688ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/75.914682ms, OpTime=75.915382ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/19.9µs, OpTime=76.896697ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/18.4µs, OpTime=77.72691ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/78.054215ms, OpTime=78.055815ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/19.701µs, OpTime=60.38344ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/7.5µs, OpTime=58.377909ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/67.201µs, OpTime=57.384694ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/30.1µs, OpTime=57.082688ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/59.069119ms, OpTime=59.06992ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/59.77383ms, OpTime=59.77473ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/8µs, OpTime=60.667044ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/7.8µs, OpTime=62.760977ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 ==> REQUEST/RESPONSE (Try=1/10.9µs, OpTime=93.627057ms) -- RESPONSE SUCCESSFULLY RECEIVED
2025/04/10 03:22:47 all parts of entire Job 8e6fd446-8a25-f24a-6201-d52b644a87d2 successfully completed, cancelled or paused
```

# Future updates - Using Cron

Learned about Cron today which automates tasks.  Will be adding that in the future to automatically backup the World folder. 
