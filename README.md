

# <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/main-title.jpg">
This repository is a part of our research work entitled 
  <p align="center"> <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/title.png"></p>
and describes how to identify MC-MitM attack signatures in terms of pattern of network traffic. Kindly refer to our above research paper for more details of MC-MitM attacks and their variants.

## <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/sub-title-1.jpg">
In MC-MitM base variant attacks, the legitimate channel is 1 since the AP operates on channel while the rogue channel is 13. The dataset or PCAP files can be [downloaded here](https://drive.google.com/drive/folders/1nsOLzfiosLP9e9lcIs7AVPWij9BBNs1C?usp=share_link). These PCAP files can also be viewed online at Cloudshark also. The following is a description of the dataset or PCAP file.
1. "Network-traffc-flow-real-channel" is the captured traffic on legitimate channel, which can be [viewed online on cloudshark](https://www.cloudshark.org/captures/2799fd9a88d6).
2. "Network-traffc-flow-rogue-channel" is the captured traffic on rogue channel, which can be [viewed online on cloudshark](https://www.cloudshark.org/captures/0487998f9748).  
3. Access the above cloudshark files and apply the following filters to see respective frames.

### A. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/filters-stage1.png">

 
#### 1. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/const-jamming.png">
It is difficult to identify constant jamming behavior with above cloudshark files.Therefore, below we provide a wireshark capture screenshot of such constant jamming behavior. Please see the yellow box in the above wireshark capture screenshot. Here, the arrival time between first and second beacon frame is around 82 ms, which shows that there was a constant jamming on the channel of the AP. When such jamming occurs, it can drastically affect the standard deviation of frame inter-arrival time If we observe this behavior for a specific time (e.g., 60 seconds). In normal conditions, the frame inter-arrival time would be 0.2 or 0.3ms if the AP transmits  beacons  every 100ms. This way, we calculate the frame inter-arrival time and frame delivery ratio to identify potential constant jamming attacks. 
<p align="center">
  <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/const-jam-example.png">
</p>


#### 2. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/reactive%20jamming.png">
```
(_ws.malformed) and (wlan.bssid == c0:4a:00:33:3b:62) and (wlan.fc.type_subtype ==8 or wlan.fc.type_subtype ==5)

```
### B. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/filters-stage2.png">

Here, victims MAC addresses are 8c:f5:a3:08:16:63 and e4:02:9b:cd:3b:92 and APś MAC address is c0:4a:00:33:3b:62
#### 1. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-beacon-traffic.png">
##### Filter for legitimate channel
```
 (wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==1)&& (wlan.fc.type_subtype==8)
```
##### Filter for rogue channel
```
 (wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==13)&& (wlan.fc.type_subtype==8)
```
#### 2. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-probe-traffic.png">
##### Filter for legitimate channel
```
(wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==1 )&& (wlan.fc.type_subtype==5) and (wlan.addr == 8c:f5:a3:08:16:63 or wlan.addr == e4:02:9b:cd:3b:92)
```
##### Filter for rogue channel
```
(wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==13 )&& (wlan.fc.type_subtype==5) and (wlan.addr == 8c:f5:a3:08:16:63 or wlan.addr == e4:02:9b:cd:3b:92)
```

#### 3. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-auth-traffic.png">

##### Filter for legitimate channel
```
 (wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==1)&& (wlan.fc.type_subtype==11) and (wlan.addr == 8c:f5:a3:08:16:63 or wlan.addr == e4:02:9b:cd:3b:92)
```
##### Filter for rogue channel
```
 (wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==13)&& (wlan.fc.type_subtype==11) and (wlan.addr == 8c:f5:a3:08:16:63 or wlan.addr == e4:02:9b:cd:3b:92)
```
#### 4. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-asso-traffic.png">

##### Filter for legitimate channel
```
(wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==1)&& (wlan.fc.type_subtype==1) and (wlan.addr == 8c:f5:a3:08:16:63 or wlan.addr == e4:02:9b:cd:3b:92)
```
##### Filter for rogue channel
```
(wlan.bssid == c0:4a:00:33:3b:62 ) and  (wlan_radio.channel==13)&& (wlan.fc.type_subtype==1) and (wlan.addr == 8c:f5:a3:08:16:63 or wlan.addr == e4:02:9b:cd:3b:92)
```
#### 5. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-eapol-traffic.png">

##### Filter for legitimate channel
```
(eapol and not wlan.fc.type ==1) && wlan_radio.channel == 1 &&  (wlan.bssid == c0:4a:00:33:3b:62 ) && (wlan.addr== 8c:f5:a3:08:16:63 or wlan.addr== e4:02:9b:cd:3b:92)
```
##### Filter for rogue channel
```
(eapol and not wlan.fc.type ==1) && wlan_radio.channel == 13 &&  (wlan.bssid == c0:4a:00:33:3b:62 ) && (wlan.addr== 8c:f5:a3:08:16:63 or wlan.addr== e4:02:9b:cd:3b:92)
```
#### 6. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-data-traffic.png">

##### Filter for legitimate channel
```
(wlan.addr == c0:4a:00:33:3b:62)  and (wlan.addr == 8c:f5:a3:08:16:63)  && (wlan_radio.channel==1)&&  (wlan.fc.type_subtype==40) 
```
##### Filter for rogue channel
```
(wlan.addr == c0:4a:00:33:3b:62)  and (wlan.addr == 8c:f5:a3:08:16:63)  && (wlan_radio.channel==13)&&  (wlan.fc.type_subtype==40) 

```

## <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/sub-title-2.jpg">
In MC-MitM improved variant attacks, the legitimate channel is 1 since the AP operates on channel while the rogue channel is 13. The dataset (PCAP files) can be [downloaded here](https://drive.google.com/drive/folders/1qY6SyCaCrDWSZII4PmZt8Qn9E3V8VCTn?usp=share_link) These PCAP files can also be viewed online at Cloudshark. 
The following is a description of the dataset or PCAP file.
1. "Network-traffc-flow-real-channel" is the captured attack traffic on legitimate channel, which can be [viewed online on cloudshark](https://www.cloudshark.org/captures/2799fd9a88d6).
2. "Network-traffc-flow-rogue-channel" is the captured attack traffic on rogue channel, which can be [viewed online on cloudshark](https://www.cloudshark.org/captures/7efff27036ad).
3. Access the above cloudshark files and apply the following filters to see respective frames.

### A. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/filters-stage1.png">


#### 1. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/fake%20csa.png">
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==1 )&& wlan.csa.channel_switch_mode

```
### B. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/filters-stage2.png">
Here, victim MAC addresses is 00:72:63:f3:0a:15 and APś MAC address is 78:98:e8:50:d4:e4
#### 1. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-beacon-traffic.png">
##### Filter for legitimate chanel
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==1)&& (wlan.fc.type_subtype==8)
```
##### Filter for rogue channel
```
 (wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==11)&& (wlan.fc.type_subtype==8)
```
#### 2. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-probe-traffic.png">
##### Filter for legitimate channel
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==1)&& (wlan.fc.type_subtype==5)
```
##### Filter for rogue channel
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==11)&& (wlan.fc.type_subtype==5)
```

#### 3. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-auth-traffic.png">

##### Filter for legitimate channel
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==1)&& (wlan.fc.type_subtype==11) and (wlan.addr==00:72:63:f3:0a:15)
```
##### Filter for rogue channel
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==11)&& (wlan.fc.type_subtype==11) and (wlan.addr==00:72:63:f3:0a:15)
```
#### 4. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-asso-traffic.png">

##### Filter for legitimate channel
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==1)&& (wlan.fc.type_subtype==1) and (wlan.addr==00:72:63:f3:0a:15)
```
##### Filter for rogue channel
```
(wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==11)&& (wlan.fc.type_subtype==1) and (wlan.addr==00:72:63:f3:0a:15)
```
#### 5. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-eapol-traffic.png">
##### Filter for legitimate channel
```
(eapol and not wlan.fc.type ==1) && (wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==1)&& (wlan.addr == 00:72:63:f3:0a:15)
```
##### Filter for rogue channel
```
(eapol and not wlan.fc.type ==1) && (wlan.bssid == 78:98:e8:50:d4:e4 ) && (wlan_radio.channel==11)&& (wlan.addr == 00:72:63:f3:0a:15)
```
#### 6. <img src="https://github.com/maneshthankappan/MC-MitM-Attack-Dataset/blob/main/Labels/con-data-traffic.png">

##### Filter for legitimate channel
```
(wlan.bssid == 78:98:e8:50:d4:e4) && (wlan_radio.channel==11)&& (wlan.addr == 00:72:63:f3:0a:15) and (wlan.fc.type_subtype==32 or wlan.fc.type_subtype==40) 
```
##### Filter for rogue channel
```
(wlan.bssid == 78:98:e8:50:d4:e4) && (wlan_radio.channel==11)&& (wlan.addr == 00:72:63:f3:0a:15) and (wlan.fc.type_subtype==32 or wlan.fc.type_subtype==40) 

```

## Notes
  * Attack signatures are created for educational or research purpose only. 
  * All attacks were conducted within a private network of UOC research labs.
  * Network trace does not contain any sensitive data.
  * Visit the link [How to perfrom MC-MitM Base-Variant Attacks](https://github.com/maneshthankappan/Multi-Channel-Man-in-the-Middle-Attacks-Against-Protected-Wi-Fi-Networks-By-Base-Variant-), which explains how we setup attack environment.
  * Visit the link [How to perfrom MC-MitM Improved-Variant Attacks](https://github.com/maneshthankappan/Multi-Channel-Man-in-the-Middle-Attacks-Against-Protected-Wi-Fi-Networks-By-Improved-Variant), which explains how we setup attack environment.
 
## References
  * https://github.com/vanhoefm/modwifi
  * https://github.com/lucascouto/mitm-channel-based-package
  * https://www.krackattacks.com/
  * https://www.fragattacks.com/#tools
  * https://papers.mathyvanhoef.com/acsac2014.pdf
  * https://papers.mathyvanhoef.com/ccs2018.pdf





