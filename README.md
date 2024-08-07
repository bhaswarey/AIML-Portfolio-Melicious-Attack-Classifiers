

# Capstone Project : Cellular Device Originated Melicious Attack Classification

[Link to notebook:]  AIML-Portfolio-Melicious-Attack-Classifiers/prompt_IV_part1.ipynb at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/prompt_IV_part1.ipynb) 



## Context

The goal of this project is to define a self-adaptive secuirty mechanism in 4G/5G cellular networks to detect/prevent attacks launched by cellular devices. The mechanism includes data exploration and quality check of the network generated data and select the best model based on the performance of the classifiers (k-nearest neighbors, logistic regression, decision trees, and support vector machines). The dataset used is related to network intrusion detection generatde over 5G wireless network and comes from [kaggle](https://www.kaggle.com/datasets/humera11/5g-nidd-dataset). 



# 1 Business Understanding



## 1.1 Background



With a plethora of new connections, features, and services introduced, the 5th generation (5G) wireless technology reflects the development of mobile communication networks and is here to stay for the next decade. The multitude of services and technologies that 5G incorporates have made modern com- munication networks very complex and sophisticated in nature. This complexity along with the incorporation of Machine Learn- ing (ML) and Artificial Intelligence (AI) provides the opportunity for the attackers to launch intelligent attacks against the network and network devices. These attacks often traverse undetected due to the lack of intelligent security mechanisms to counter these threats. 

Therefore, the implementation of real-time, proactive, and self-adaptive security mechanisms throughout the network would be an integral part of 5G as well as future communication systems. Large amounts of data collected from real networks will play an important role in the training of AI/ML models to identify and detect malicious content in network traffic. This work presents %G Network Intrusion Detection Dataset (5G-NIDD), a fully labeled dataset built on a functional 5G test network that can be used by those who develop and test AI/ML solutions. The work further analyses the collected data using common ML models and shows the achieved accuracy levels.

The following approach will be taken as part of implementing the self-adaptive security mechanism:

- Level 1 classification - identify cellular device originated messages as 'benign' or 'melicious' taking the binary classification approach 
- Level 2 classification - identify melicious message 'attack type' taking the multi-class classification approach using one-versus-one strategy

The level 1 classification allows the system to detect a threat while level 2 allows the system to take specific steps to neutralize the threat.



## 1.2 Business Goals and KPI

The business objective is to find the best models to identify and detect malicious content in network traffic. This model will help cellular service provides provide secure and reliable services to thier customers, improving business outcomes.



# 2 Data Understanding

This section provides information about the data, its description and is its exploration to make sure it fits the business goals.



## 2.1 **Gathering and Describing Data**

This data comes from [UCI Machine Learning repository Links to an external site.](https://archive.ics.uci.edu/ml/datasets/bank+marketing). Here is a sample of the data:



| `Unnamed: 0` |    `Seq` | `Dur` |  `RunTime` |     `Mean` |      `Sum` |      `Min` |      `Max` |    `Proto` | `sTos` |  `dTos` |  `sDSb` | `dDSb` | `sTtl` |  `dTtl` | `sHops` | `dHops` | `Cause` | `TotPkts` | `SrcPkts` | `DstPkts` | `TotBytes` | `SrcBytes` | `DstBytes` | `Offset` | `sMeanPktSz` | `dMeanPktSz` |       `Load` |      `SrcLoad` |     `DstLoad` |         `Loss` | `SrcLoss` | `DstLoss` | `pLoss` | `SrcGap` | `DstGap` | `Rate` |   `SrcRate` |   `DstRate` |    `State` | `SrcWin` | `DstWin` |  `sVid` |  `dVid` | `SrcTCPBase` |   `DstTCPBase` |       `TcpRtt` | `SynAck` | `AckDat` | `Label` | `Attack Type` | `Attack Tool` |          |
| -----------: | -------: | ----: | ---------: | ---------: | ---------: | ---------: | ---------: | ---------: | -----: | ------: | ------: | -----: | -----: | ------: | ------: | ------: | ------: | --------: | --------: | --------: | ---------: | ---------: | ---------: | -------: | -----------: | -----------: | -----------: | -------------: | ------------: | -------------: | --------: | --------: | ------: | -------: | -------: | -----: | ----------: | ----------: | ---------: | -------: | -------: | ------: | ------: | -----------: | -------------: | -------------: | -------: | -------: | ------: | ------------: | ------------: | -------- |
|    `1215885` | `487569` |   `1` | `0.000000` | `0.000000` | `0.000000` | `0.000000` | `0.000000` | `0.000000` | `sctp` | `186.0` | `186.0` |   `ef` |   `ef` | `252.0` | `255.0` |   `4.0` |   `1.0` |  `Status` |       `2` |       `1` |        `1` |      `200` |      `102` |     `98` |     `190300` | `102.000000` |  `98.000000` |     `0.000000` |    `0.000000` |     `0.000000` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` |  `0.000000` |  `0.000000` | `0.000000` |    `CON` |    `NaN` |   `NaN` | `610.0` |        `NaN` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215886` | `487570` |   `3` | `0.235607` | `0.235607` | `0.235607` | `0.235607` | `0.235607` | `0.235607` | `sctp` | `186.0` |  `40.0` |   `ef` | `af11` | `255.0` | `250.0` |   `1.0` |   `6.0` |  `Status` |       `6` |       `3` |        `3` |     `3056` |      `290` |   `2766` |     `190392` |  `96.666664` | `922.000000` | `69199.984380` | `6587.240723` | `62612.742190` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` | `21.221781` |  `8.488712` | `8.488712` |    `CON` |    `NaN` |   `NaN` |   `NaN` |      `610.0` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215887` | `487571` | `764` | `0.099927` | `0.099927` | `0.099927` | `0.099927` | `0.099927` | `0.099927` |  `tcp` |   `0.0` |   `0.0` |  `cs0` |  `cs0` |  `64.0` | `114.0` |   `0.0` |  `14.0` |   `Start` |       `3` |       `2` |        `1` |      `252` |      `160` |     `92` |     `190496` |  `80.000000` |  `92.000000` |  `6404.675293` | `6404.675293` |     `0.000000` |       `0` |       `0` |     `0` |    `0.0` |    `0.0` |  `0.0` | `20.014610` | `10.007305` | `0.000000` |    `CON` |  `213.0` | `273.0` |   `NaN` |        `NaN` | `2.237373e+09` | `1.983280e+09` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215888` | `487572` |   `3` | `1.307852` | `1.307852` | `1.307852` | `1.307852` | `1.307852` | `1.307852` | `sctp` | `186.0` |  `40.0` |   `ef` | `af11` | `255.0` | `250.0` |   `1.0` |   `6.0` |  `Status` |       `6` |       `3` |        `3` |      `596` |      `306` |    `290` |     `190704` | `102.000000` |  `96.666664` |  `2434.526123` | `1247.847534` |  `1186.678589` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` |  `3.823062` |  `1.529225` | `1.529225` |    `CON` |    `NaN` |   `NaN` |   `NaN` |      `610.0` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215889` | `487573` |   `1` | `0.476803` | `0.476803` | `0.476803` | `0.476803` | `0.476803` | `0.476803` | `sctp` | `186.0` | `186.0` |   `ef` |   `ef` | `252.0` | `255.0` |   `4.0` |   `1.0` |  `Status` |       `4` |       `2` |        `2` |      `392` |      `200` |    `192` |     `190808` | `100.000000` |  `96.000000` |  `3288.569824` | `1677.841797` |  `1610.728149` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` |  `6.291907` |  `2.097302` | `2.097302` |    `CON` |    `NaN` |   `NaN` | `610.0` |        `NaN` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |



Following features of the provided sample data above:

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1215890 entries, 0 to 1215889
Data columns (total 52 columns):
 #   Column       Non-Null Count    Dtype  
---  ------       --------------    -----  
 0   Unnamed: 0   1215890 non-null  int64  
 1   Seq          1215890 non-null  int64  
 2   Dur          1215890 non-null  float64
 3   RunTime      1215890 non-null  float64
 4   Mean         1215890 non-null  float64
 5   Sum          1215890 non-null  float64
 6   Min          1215890 non-null  float64
 7   Max          1215890 non-null  float64
 8   Proto        1215890 non-null  object 
 9   sTos         1215676 non-null  float64
 10  dTos         272823 non-null   float64
 11  sDSb         1215676 non-null  object 
 12  dDSb         272823 non-null   object 
 13  sTtl         1215676 non-null  float64
 14  dTtl         272823 non-null   float64
 15  sHops        1215676 non-null  float64
 16  dHops        272823 non-null   float64
 17  Cause        1215890 non-null  object 
 18  TotPkts      1215890 non-null  int64  
 19  SrcPkts      1215890 non-null  int64  
 20  DstPkts      1215890 non-null  int64  
 21  TotBytes     1215890 non-null  int64  
 22  SrcBytes     1215890 non-null  int64  
 23  DstBytes     1215890 non-null  int64  
 24  Offset       1215890 non-null  int64  
 25  sMeanPktSz   1215890 non-null  float64
 26  dMeanPktSz   1215890 non-null  float64
 27  Load         1215890 non-null  float64
 28  SrcLoad      1215890 non-null  float64
 29  DstLoad      1215890 non-null  float64
 30  Loss         1215890 non-null  int64  
 31  SrcLoss      1215890 non-null  int64  
 32  DstLoss      1215890 non-null  int64  
 33  pLoss        1215890 non-null  float64
 34  SrcGap       278671 non-null   float64
 35  DstGap       278671 non-null   float64
 36  Rate         1215890 non-null  float64
 37  SrcRate      1215890 non-null  float64
 38  DstRate      1215890 non-null  float64
 39  State        1215890 non-null  object 
 40  SrcWin       242420 non-null   float64
 41  DstWin       177078 non-null   float64
 42  sVid         114571 non-null   float64
 43  dVid         2009 non-null     float64
 44  SrcTCPBase   278671 non-null   float64
 45  DstTCPBase   230047 non-null   float64
 46  TcpRtt       1215890 non-null  float64
 47  SynAck       1215890 non-null  float64
 48  AckDat       1215890 non-null  float64
 49  Label        1215890 non-null  object 
 50  Attack Type  1215890 non-null  object 
 51  Attack Tool  1215890 non-null  object 
dtypes: float64(32), int64(12), object(8)
memory usage: 482.4+ MB
```



The description of the data is as follows:

Understanding the Features

Data description:

```
Input variables:

1 - Seq (numeric) - argus sequence number.
2 - Dur (numeric) - record total duration. 
3 - RunTime (numeric) - total active flow run time. This value is generated through aggregation, and is the sum
of the records duration.
4 - Mean (numeric) - average duration of aggregated records.
5 - Sum (numeric) - total accumulated durations of aggregated records.
6 - Min (numeric) - minimum duration of aggregated records.
7 - Max (numeric) - maximum duration of aggregated records.
8 - Proto (Categorical) - transaction protocol.
9 - sTos (numeric) - source TOS byte value.
10 - dTos (numeric) - destination TOS byte value.
11 - sDSb (categorical) - source diff serve byte value.
12 - dDSb (categorical) - destination diff serve byte value.
13 - sTtl (numeric) - src -> dst TTL value.
14 - dTtl (numeric) - dst -> src TTL value.
15 - sHops (numeric) - estimate of number of IP hops from src to this point.
16 - dHops (numeric) - estimate of number of IP hops from dst to this point.
17 - Cause (categorical) - Argus record cause code. Valid values are Start, Status, Stop, Close, Error.
18 - TotPkts (numeric) - total transaction packet count.
19 - SrcPkts (numeric) - src -> dst packet count.
20 - DstPkts (numeric) - dst -> src packet count.
21 - TotBytes (numeric) - total transaction bytes.
22 - SrcBytes (numeric) - src -> dst transaction bytes.
23 - DstBytes (numeric) - dst -> src transaction bytes.
24 - Offset (numeric) - record byte offset in file or stream.
25 - sMeanPktSz (numeric) - Mean of the flow packet size transmitted by the src (initiator).
26 - dMeanPktSz (numeric) - Mean of the flow packet size transmitted by the dst (target).
27 - Load (numeric) - bits per second.
28 - SrcLoad (numeric) - source bits per second.
29 - DstLoad (numeric) - destination bits per second.
30 - Loss (numeric) - pkts retransmitted or dropped.
31 - SrcLoss (numeric) - source pkts retransmitted or dropped.
32 - DstLoss (numeric) - destination pkts retransmitted or dropped.
33 - pLoss (numeric) - percent pkts retransmitted or dropped.
34 - SrcGap (numeric) - source bytes missing in the data stream.
35 - DstGap (numeric) - destination bytes missing in the data stream.
36 - Rate (numeric) - pkts per second.
37 - SrcRate (numeric) - source pkts per second.
38 - DstRate (numeric) - destination pkts per second.
39 - State (categorical) - transaction state.
40 - SrcWin (numeric) - source TCP window advertisement.
42 - DstWin (numeric) - destination TCP window advertisement.
43 - sVid (numeric) - source VLAN identifier.
44 - dVid (numeric) - destination VLAN identifier.
45 - SrcTCPBase (numeric) - source TCP base sequence number.
46 - DstTCPBase (numeric) - destination TCP base sequence number.
47 - TcpRtt (numeric) - TCP connection setup round-trip time, the sum of ’synack’ and ’ackdat’.
48 - SynAck (numeric) - TCP connection setup time, the time between the SYN and the SYN_ACK packets.
49 - AckDat (numeric) - TCP connection setup time, the time between the SYN_ACK and the ACK packets.
50 - Attack Tool (categorical) - Type of source that launched the attack.

Target Labels:
51 - Label (categorical) - Benign or Melicious.
52 - Attack Type (categorical) - Type of attack.
```





Categories per feature and their frequency:

```
_________________________________________

Feature: Proto
    category  freq in %
0        udp      74.28
1        tcp      22.92
2       icmp       2.44
3       sctp       0.36
4  ipv6-icmp       0.00
_________________________________________

Feature: sDSb
   category  freq in %
0       cs0      99.47
1        ef       0.29
2      af11       0.06
3       cs6       0.05
4       cs7       0.04
5      af41       0.04
6        52       0.01
7      af12       0.01
8       cs4       0.01
9         4       0.01
10       39       0.00
11       54       0.00
_________________________________________

Feature: Cause
   category  freq in %
0    Status      59.92
1     Start      40.02
2  Shutdown       0.06
_________________________________________

Feature: State
   category  freq in %
0       REQ      48.46
1       INT      27.04
2       CON      10.87
3       RST       6.22
4       FIN       4.87
5       ECO       2.37
6       ACC       0.09
7       URP       0.06
8       RSP       0.01
9       TST       0.00
10      NRS       0.00
_________________________________________

Feature: Label
    category  freq in %
0  Malicious      60.72
1     Benign      39.28
_________________________________________

Feature: Attack Type
         category  freq in %
0          Benign      39.28
1        UDPFlood      37.62
2       HTTPFlood      11.58
3     SlowrateDoS       6.02
4  TCPConnectScan       1.65
5         SYNScan       1.65
6         UDPScan       1.31
7        SYNFlood       0.80
8       ICMPFlood       0.10
_________________________________________

Feature: Attack Tool
     category  freq in %
0      Benign      39.28
1      Hping3      38.51
2   Goldeneye      11.58
3  Torshammer       4.92
4        Nmap       4.61
5   Slowloris       1.09
_________________________________________
```

The above provides the categorical features and the category per feature with the frequency of occurrence. 



***Here are some additional details on target columns - <u>'Label' and 'Attack Type'</u>:***

**1 - *DoS Attacks* Types -** A DoS attack is one of the most common attacks that can occur in a network. The aim of this attack is to slow down or completely shut down a target making it inaccessible to legitimate users. Flooding techniques and malicious content injection are some of the common methods to lunch a DoS attack. The network or a node will eventually undergo resource exhaustion and deny the nonmalicious users’ access as a result of a DoS attack. Due to the heterogeneous nature of the 5G networks, DoS attacks impose a vital threat in 5G which may target the network nodes, devices, and applications.

​	**a) *Benign Traffic:*** The benign traffic profile includes protocols such as HTTP, HTTPS, SSH, and Secure File Transfer Protocol (SFTP). 

​	**b) *ICMP Flood:*** Internet Control Message Protocol (ICMP) flood attacks use ICMP echo requests to flood a target at a very high frequency. Ideally, an ICMP echo reply follows the echo request to the same Internet Protocol (IP) address. In this type of attack, the target will send back echo replies to massive amounts of ICMP echo requests. The higher frequency of echo requests also leads to a higher frequency in the rate of response which eventually overwhelms the network and makes the services unavailable for normal users.

​	**c) *UDP Flood:*** In a User Datagram Protocol (UDP) flood attack, attacker sends UDP packets at a higher rate. Since UDP is a connection-less protocol, it is possible to send a large amount of traffic. As the UDP packets arrive at the target destination, the reply is a “Destination Unreachable” packet if no associated application is found. Over time, as a higher amount of UDP packets are received and responded to, the system eventually becomes nonresponsive.

​	**d) *SYN Flood:*** SYN flood attack is a result of the exploitation of the TCP three way handshake. In a typical TCP communication between two nodes, the source nodes sends a SYN packet to the desired node for the initiation of the connection. The destination node replies with a SYN ACK to acknowledge the SYN packet. Finally, the source sends another ACK to acknowledge receiving the SYN ACK, completing the three way handshake. In a SYN flood attack, the attacker does not perform the final step of the TCP handshake, therefore leaving the connection half open. The transmission of SYN packets at a higher frequency will leave large amounts of ports half open for a certain period and eventually the receiver will be exhausted once all ports are occupied preventing access for legitimate users.

​	**e) *HTTP Flood:*** HTTP flood attacks target the application layer. It is a popular method for DoS/DDoS attacks due to its proven effectiveness in mimicking normal human behavior and thereby staying undetected. We used Python based Goldeneye tool to conduct the HTTP flood attacks. To perform the application layer attacks, we deployed a web server at the victim Multi-access Edge Computing (MEC) instance. The target was an Apache2 web server deployed in MEC.

​	**f) *Slowrate DoS:*** Another exploitation of the application layer to conduct DoS attacks is the use of slow rate attacks. In terms of the speed and the number of packets directed at the target, it is comparatively different from other forms of DoS attacks. This slow nature of the traffic makes it harder to detect. In this exercise, we conducted two different forms of slow rate DoS attacks. As the first one, we performed slowloris attack through a python script. The attack establishes several connections with the targeted web server and maintain them for a longer period. We performed this by sending HTTP partial headers continuously to keep the connections open without completion. The web server waits for the connections to complete which might never occur. The opening of a large number of such connections will eventually lead to resource exhaustion. 

​	In another case, the attacker sends slow POST requests to a web server. The POST requests comprises packets that specify a larger packet size in the header field, but the actual packet has a lesser size. The server then waits for the completion of the whole packet size specified in the header field.



**2 - *Port Scans*** - A port scan usually precedes an actual attack to identify opportunities for attacks via open ports. Typically, port scans send requests to a targeted range of ports in a targeted host and observe the response. The response is sufficient to determine the status of a specific port in most cases. In some instances, deeper knowledge such as the operating system of the target may also be discovered. Port scan is an efficient way to determine exploitable hosts in a network before the execution of attacks. The dataset contains attack data from different port scans such as the SYN scan, TCP Connect scan, and UDP scan.

​	**a) *SYN Scan:*** The SYN scan uses part of the three way handshake in TCP connection establishment to discover open ports. The attacker sets the SYN flag in a TCP packet and sends to the target. If the targeted port/s is ready for a TCP connection, it returns a response packet with SYN and ACK flags set. This means the scan indicates an *open* port to the attacker. Ports that are not ready to establish a TCP connection send a RST packet indicating a *closed* port. As the attacker determines the state of the port from two packet flows, attacker cease the execution of the next step of the three way handshake. However, to terminate the connection the attacker may send an RST packet to the target once the information on the status of the port is collected. If not, the target will keep sending packets with SYN and ACK flags set until a response is seen from the attacker. Other than *open* or *closed* ports, a *filtered* port may imply that a firewall is blocking the packets or the host is not reachable.

​	The incomplete three way handshake in SYN scan makes the scanning process quite fast in comparison to other available techniques. The SYN scan is one of the most popular scanning techniques.

​	**b) *TCP Connect Scan:*** Similar to SYN scan, the TCP connect scan exploits the TCP handshake to perform the scanning process. However, the three way handshake is fully completed therefore, the time taken to scan the ports is higher compared with SYN Scan. Conversely, attackers may not need the same level of privileges to execute a TCP connect scan as they require for SYN scan.

​	The execution of the TCP connect scan is similar to SYN scan with the addition of the completion step in the three way handshake. This means that the two initial packet flows (SYN flag set packet and SYN ACK flags set packet) take place for an *open* port. Subsequently, the target replies with a packet set with ACK flag to complete the three way handshake. Although the opening of a TCP connection also offers the potential for data exchange, the attacking operating system makes sure the connection is terminated as soon as it detects that one has been made. In the event of a *closed* port, target sends a RST packet to the host similar to the SYN scan. *Filtered* ports may also exist in this scenario.

​	**c) *UDP Scan:*** UDP scan transmits UDP datagrams to the targeted ports of the targeted host. The attacker sends the UDP packets with a missing payload to ports that are not UDP. For UDP ports, a protocol-specific payload will exist. In UDP scan, the status of a port is defined based on the response of the target or the unresponsiveness of the target. As nonUDP ports receive a UDP datagram without a payload, the probability of getting a proper response is minimum. An *open|filtered* state is likely from such ports which indicates either a firewall is blocking the packets or packets are simply been forwarded from TCP/IP stack towards a listening application and discards them as invalid. Because of this, it might be challenging to precisely identify whether a port is open for nonUDP ports. In the case of UDP ports, a response may be recognized as a clear indicator of an *open* port. A port is judged to be closed if the response is an ICMP port unreachable error.





## 1.2 Early Data **Exploration** and Data Quality Check

Next step is to check the quality of the data. For example, due to the presence of categorical features,  the summary of the data is checked for the types in each category. By doing this, the step needed for data cleaning or to be transformed is identified. For example, checking for missing/empty values.

Following is the list of missing values in percentage:

```
Unnamed: 0      0.00
Seq             0.00
Dur             0.00
RunTime         0.00
Mean            0.00
Sum             0.00
Min             0.00
Max             0.00
Proto           0.00
sTos            0.02
dTos           77.56
sDSb            0.02
dDSb           77.56
sTtl            0.02
dTtl           77.56
sHops           0.02
dHops          77.56
Cause           0.00
TotPkts         0.00
SrcPkts         0.00
DstPkts         0.00
TotBytes        0.00
SrcBytes        0.00
DstBytes        0.00
Offset          0.00
sMeanPktSz      0.00
dMeanPktSz      0.00
Load            0.00
SrcLoad         0.00
DstLoad         0.00
Loss            0.00
SrcLoss         0.00
DstLoss         0.00
pLoss           0.00
SrcGap         77.08
DstGap         77.08
Rate            0.00
SrcRate         0.00
DstRate         0.00
State           0.00
SrcWin         80.06
DstWin         85.44
sVid           90.58
dVid           99.83
SrcTCPBase     77.08
DstTCPBase     81.08
TcpRtt          0.00
SynAck          0.00
AckDat          0.00
Label           0.00
Attack Type     0.00
Attack Tool     0.00
dtype: float64
```





Figure 1 is the result of an attempt to preserve features that have over 80% of missing data by removing rows with null data. This approach resulted in the dataset to be be reduced from 1.2M to ~300K rows and caused the data to be imbalanced (for target column 'Label')   

![AIML-Portfolio-Melicious-Attack-Classifiers/images/pie_benign_malicious_before_cleaning_data.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pie_benign_malicious_before_cleaning_data.png) 

**Figure 1 - Benign vs Malicious Result - Before Dropping Features with >= 77% Missing Data**

Given the result in Figure 1, the approach taken was to drop features with missing data above 77%., followed by removing duplicates. Figure 2 provides the 'Label' discribution after removing null and duplicate data.

![AIML-Portfolio-Melicious-Attack-Classifiers/images/pie_benign_malicious_after_cleaning_data.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pie_benign_malicious_after_cleaning_data.png) 

**Figure 2 - Benign vs Malicious Result - Post Dropping Features with >= 77% Missing Data**



Shape pre & post treating duplicate data:

```
(1215676, 39)
Duplicates : 21
Shape post treating duplicates: (1215655, 39)
```









# 2 Data Preparation

This section provides information on data preparation and cleaning, to allow for analysis as part of this case study and the future case studies covering predictions.  



## 2.1 Data Transformation

Following categorical features were transformed:

**a) [Binary Classification Approach] (Level 1) Target Feature - 'Label' -** Ordinal encoding method used

{'Benign': 0, 'Malicious': 1}.

**b) [Multi-class Classification Approach] (Level 2) Target Feature - 'Attack Type' -** Ordinal encoding method used

{'Benign': 0, 'UDPFlood': 1, 'HTTPFlood': 2, 'SlowrateDoS': 3, 'TCPConnectScan': 4, 'SYNScan': 5, 'UDPScan': 6, 'SYNFlood': 7, 'ICMPFlood': 8}.

**b) Remaining -** 

For the rest of the catagorical data, One-Hot-Encoding method was used.



## 2.2 Data Cleansing

In this step, the data is handled based on the problem found during the data understanding phase. Based on the finding, the following steps are executed:

a) Dropped columns that had over 77% of missing values. 

b) After step (a), removed rows with NULL values.

c) Duplicate data was found and removed.



## 2.2 Final Data (post cleaning and transformation)

The shape data after cleaning : (1215655, 39)

![AIML-Portfolio-Melicious-Attack-Classifiers/images/pie_benign_malicious_after_cleaning_data.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pie_benign_malicious_after_cleaning_data.png) 

**Figure 3 - Level 1 Target Feature Post Data Cleaning**

In Figure 3, the disbribution of  'Label' distribution between 'benign' or 'melicious' (binary classification).



![AIML-Portfolio-Melicious-Attack-Classifiers/images/benign_malicious_attacktype.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/benign_malicious_attacktype.png) 

**Figure 4 - Level 2 Target Feature Post Data Cleaning**

In Figure 4, the disbribution of  'Attack Type' distribution (multi-class classification).

Clearly imbalances in the Attack Type categories (classification of malicious attacks). The most noticeable are:

- UDPFlood
- UDPScan
- TCPConnectScan
- SYNScan
- SYNFlood
- ICMPFlood

 

# 3 Data Understanding - Deep Analysis

This section provides information about deeper exploration and analysis of the data conducted, in preparation for future machine learning model.



## 3.1 Exploratory Data Analysis (EDA)

In this section, the results of exploring and visualizing insight from the data is captured.



### 3.1.1 Categorical Data 

Figure 4 provides a view of the categorical features and the category distribution per feature in percentage.

![AIML-Portfolio-Melicious-Attack-Classifiers/images/bar_categories.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/bar_categories.png) 

**Figure 4 - Categorical Features**

In Figure 4, the disbribution of the feature categories is presented, providing a hint as to which feature and associated categories may influence 'Label' outcome as 'benign' or 'melicious' (level 1 classification). 

Figure 3 provides 'Label' breakdown into 'Attack Type', providing a drill down view of messages that are classified as melicious (via binary classification) into the type of melicious attack categories (via multi-class classification) 



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/proto_benign_malicious.png) 

**Figure 5 - Distribution of Benign and Malicious messages across Proto categories**

Figure 5 provides a view of the message Proto categories and their association to 'Label' classification. Fore example, 'icmp' protocol based messages have a very high likelihood of being benign. Where as 'tcp' protocol based messages are highly likelihood of being malicious.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/proto_benign_malicious.png) 

**Figure 6 - Malicious Vs Benign distribution per Proto category**



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/Proto_benign_malicious_distribution.png) 

**Figure 7 - Comparitive view - Malicious Vs Benign distribution per Proto category**



Figure 6/7 provides a view of the message protocol categories and their association to 'Label' classification. For example, 'icmp' protocol based messages have a very high likelihood of being benign. Where as 'tcp' protocol based messages are highly likely to be of malicious type.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/State_benign_malicious_distribution.png) 

**Figure 8 - Malicious Vs Benign distribution per State category**

Figure 8 provides a view of the session state categories and their association to 'Label' classification. For example, 'RST', 'FIN' states have a very high likelihood of being malicious. Where as 'ECO' protocol based messages are highly likely to be of benign type.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/Cause_benign_malicious_distribution.png) 

**Figure 9 - Malicious Vs Benign distribution per Cause category**

Figure 9 provides a view of the cause categories and their association to 'Label' classification. Shutdown cause is associated with messsages that are benign. Messages associated with Status cause has roughly 2/3 chance of being malicious.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/sDSb_benign_malicious_distribution.png) 

**Figure 10 - Malicious Vs Benign distribution per sDSb category**

Figure 10 provides a view of the sDSb categories and their association to 'Label' classification. With the exception of 'cs0', all sDSb types are associated with messsages that are benign. Messages associated with 'cs0' has little less than 2/3 chance of being malicious.



From the distribution presented above, it is clear the following features influence the 'y' (Label) outcome:

a) From a Label (as 'Y') prespective, the cleaned data is not as imbalanced.

b) From a Attack Type (as 'Y') prespective, the cleaned data is imbalanced. 

b) Over half of the malicious messages are of type 'UDPFlood'.

c) From the 'Proto' feature perspective, message of category type 'tcp' have roughly higher than 95% chance of being malicious. Message of category type 'dup' have roughly higher than 50% chance of being malicious

d) Messages not associated with feature category of type sDSb ''cs0' are benign.





### 3.1.2 Addressing Business Questions

Following were some of the business questions answered based on the analysis of the data.

**1) In the case of Malicious messages, what is the protocol the business should focus on to prevent majority of the malicious attacks?**

Figure 11 Malicious messages distribution across all Proto feature categories. 



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/attack_type_dist.png) 

**Figure 11 - Malicious message distrubution across Proto category types**



Over 70% of the malicious message are based on protocol of type 'udp' . The next to protocols use are 'HTTPFlood' and 'SlowrateDoS', which are less than 10% of the overall malicious messages.  



**2) Identify assets to detect/prevent majority of the attacks? **

Lets identify malicious message protocol/network features that standout. 



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/proto_attacktypes.png) 

**Figure 12 - Breakdown of malicious message across Attack Type per network protocol**



From Figure 12, it is clear that:

A)  Majority of the attacks are of UDP protocal based UDPFlood attack method

B) In the case of malicious messages using TCP protocol, the messages utilize HTTPFlood and SlowrateDoS attack methods.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/sdsb_attacktypes.png) 

**Figure 13 - Breakdown of malicious message across Attack Type per destination diff serve byte value (sDSb)**



From Figure 13, it is clear that:

A)  Majority of the attacks are of sDSb cs0 attacks utilizing SlowrateDoS

B) Remaining malicious messages utilize SYNScan, TCPConnectiotScan, UDPScan, HTTPFlood, and SlowrateDoS.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/cause_attacktypes.png) 

**Figure 14 - Breakdown of malicious message across Attack Type per cause code**



From Figure 14 provides the following information:

A)  Majority of the malicious message associated with casue code Status using UDPFlood, HTTPFlood, and SlowrateDoS attack methods 

B) Remaining malicious messages are associated with cause code Start using SYNCScan, TCPCommectScan, UDPScan, UDPFlood, SYNCFlood, HTTPFlood, and SlowrateDoS.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/cause_attacktypes.png) 

**Figure 15 - Breakdown of malicious message across Attack Type per connection state**



From Figure 15 provides the following information:

A)  Majority of the malicious message associated with state REQ & INT use UDPFlood attack methods. 

B) Remaining fewer malicious messages are associated with SYNCScan, TCPConnectScan, UDPScan, SYNCFlood, HTTPFlood, and SlowrateDoS.



NOTE: 

1. Please refer to section 2.1 for details description of malicious categories.
2. Please refer to section 2.1 for description of the attack methods.



### 4.1.3 Numerical Features Evaluation 

The numerical features were evaluated via correlation matrix and features with > 80% correlation were dropped. 

```
Features Dropped: ['RunTime', 'Mean', 'Sum', 'Min', 'Max', 'SrcPkts', 'TotBytes', 'SrcBytes', 'DstBytes', 'Offset', 'sMeanPktSz', 'DstLoad', 'Rate', 'SrcRate', 'DstRate']
```

Following are the results after dropping the identified features. 



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pairplot_numeric_features_label.png) 

**Figure 16 - Pair-plot of features aganist 'Label'**

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pairplot_numeric_features_attack_type.png) 

**Figure 17 - Pair-plot of features aganist 'Attack Type'**

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/heatmap_numeric_features_encoded.png) 

**Figure 18 - Heatmap of features aganist 'Label' and Attack Type'**



### 4.1.3 Observation 

Insights derived from the Initial analysis are: 

a) The most used attack method is UDPFlood followed by HTTPFlood

b) Network protocols per the attach method used are UDP and TCP.

Per the distribution of sDSb Attack Type category, the destination diff serve byte value may help with easily separating messages between benign versus malicious.



### 5.0   Modeling  

The goal of the modeling phase is to identify the best model to be used for identify the key features that dynamically help identify malicious messages. The classification will be executed at two levels:

1. Level 1 - Binary classification where the 'Y' (target feature) is 'Label'

2. Level 2 - Multi-class classification where the 'Y' (target fetaure) is 'Attack Type'.

   

This phase will have four tasks:

**a) Select modeling technique**: Determine which classicication algorithms to try (e.g. KNN,
DT).

**b) Generate test design**: Pending the modeling approach, split the data into training, test, and validation sets.
**c) Build model**: Build and executing the selected models.
**d) Assess model**: Interpret the model results based on the pre-defined success criteria, and the test design.



### 5.1   Model Selection 

The modeling technique is as follows:

### 5.1.1   Pre-process 

The pre-process is defined to transform the categorical features to numerical values,  retaining the original information. As a result, "Ordinal Encoder" was executed against the 'Label' and 'Attack Type' feature since the categorical values had inherent order to it.

For the rest of the features, "OneHotEncoder" was used because the categorical values did not have inherent order or ranking.

### 5.1.2   Modeling Technique 

The models that will be evaluated are:

-  Logistic Regression
- KNN
- Decision Tree
- SVM (Note: Due to time constraints, this model requires a very long runtime due to the very large size of data in terems of rows and thefore will not be used)

Following steps were taken to deterime the best model using default hyper parameters:

a) Use of GridSerachCV to help identify the best hyperparameters for each model.

b) Evaluate the accuracy and perfromance of each model. 

The model that performs the best will be selected to identify the important features that contribute to identifying malicious messages and the attack type. 

Becasue the data is imbalanced in the case where 'Y' is the Attack Type, the F1-sore was used.

### 5.1.3   Testing Technique 

The pre-processed data will be split, of which 70% will be randomly allocated for taining and 30% will be allocated for testing.

### 5.1.4   Model assessment using hyperparameter

GridSearchCV will be used for each model to find the optimal hyper parameters.



### 5.1.5   Refining Data

Per the results presented in Figure 18, following features were further identified to have correlation above 80% were dropped:

```
Features to Drop: ['Proto_udp', 'sDSb_cs0', 'sDSb_ef', 'Cause_Status', 'State_ECO', 'State_NRS', 'State_URP']
```



### 5.2   Binary Classification 

### 5.2.1 Summary of Assessment Results 

The dataset was split as follows:

```
Xbin_train shape = (850958, 41)
 Xbin_test shape = (364697, 41)
ybin_train shape = (850958,)
 ybin_test shape = (364697,)
```

Following is a sample view of the normal data:

|      |       Seq |       Dur |      sTos |      sTtl |     sHops |   TotPkts |   DstPkts | dMeanPktSz |      Load |   SrcLoad |      Loss |   SrcLoss |  DstLoss |    pLoss |    TcpRtt |    SynAck |    AckDat | Proto_icmp | Proto_ipv6-icmp | Proto_sctp | Proto_tcp |   sDSb_39 |    sDSb_4 |   sDSb_52 |   sDSb_54 | sDSb_af11 | sDSb_af12 | sDSb_af41 |  sDSb_cs4 |  sDSb_cs6 |  sDSb_cs7 | Cause_Shutdown | Cause_Start | State_ACC | State_CON | State_FIN | State_INT | State_REQ | State_RSP | State_RST | State_TST |
| ---: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | ---------: | --------: | --------: | --------: | --------: | -------: | -------: | --------: | --------: | --------: | ---------: | --------------: | ---------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | -------------: | ----------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: |
|    0 |  2.070873 | -0.807021 | -0.069237 | -0.329345 | -0.352366 | -0.165054 | -0.111893 |  -0.287842 | -0.008214 | -0.010969 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 |  1.031632 | -0.007511 | -0.257647 | -0.004336 |
|    1 | -0.619749 |  0.715383 | -0.069237 | -0.329345 | -0.352366 | -0.125414 | -0.111893 |  -0.287842 | -0.008214 | -0.010957 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 |  1.031632 | -0.007511 | -0.257647 | -0.004336 |
|    2 | -0.781195 | -0.807021 | -0.069237 | -0.329345 | -0.352366 | -0.165054 | -0.034843 |   0.018933 | -0.008214 | -0.010969 | -0.091038 | -0.074202 | -0.06135 | -0.09457 |  5.078216 |  0.081540 |  8.386164 |   -0.15843 |       -0.001533 |  -0.060035 |  1.834878 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 | -0.969338 | -0.007511 |  3.881275 | -0.004336 |
|    3 | -0.967806 |  0.720621 | -0.069237 | -0.329345 | -0.352366 | -0.125414 | -0.111893 |  -0.287842 | -0.008214 | -0.010958 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 |  1.031632 | -0.007511 | -0.257647 | -0.004336 |
|    4 |  0.583671 |  0.715967 | -0.069237 | -0.329345 | -0.352366 | -0.125414 | -0.111893 |  -0.287842 | -0.008214 | -0.010957 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |                |             |           |           |           |           |           |           |           |           |



### 5.2.2   Binary Classification - Model Comparison 



Following is the comparison between the 3 models:

```
                   Model  Train Accuracy  Test Accuracy
0  Logistic Regression        0.990149       0.990104
1                  KNN        0.999700       0.999548
2        Decision Tree        0.999766       0.999619
```

| algorithm | params |                                        mean_score | std_score | cv_result |                                                   |
| --------: | -----: | ------------------------------------------------: | --------: | --------: | ------------------------------------------------- |
|         0 |     LR | {'C': 4.281332398719396, 'max_iter': 2500, 'mu... |  0.990146 |  0.000150 | {'mean_fit_time': [1.467014233271281, 1.580855... |
|         1 |    KNN | {'metric': 'manhattan', 'n_neighbors': 5, 'wei... |  0.999521 |  0.000026 | {'mean_fit_time': [1.7499810059865315, 2.31384... |
|         2 |     DT | {'criterion': 'entropy', 'max_depth': 10, 'min... |  0.999706 |  0.000014 | {'mean_fit_time': [1.6299346288045247, 1.79270... |



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/confusion_matrix_binary.png) 

**Figure 18 - Binary Classification - Confusion Matrix**



Figure 18 provides th confusion matrix fo the three models with the following additional information per model:

```
Model = LogisticRegression(C=4.281332398719396, max_iter=2500,
                   multi_class='multinomial', solver='sag') AUC = 0.99

Model = KNeighborsClassifier(metric='manhattan') AUC = 1.0

Model = DecisionTreeClassifier(criterion='entropy', max_depth=10, min_samples_leaf=5) AUC = 1.0
```



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/test_best_model_binary_confusion_matrix.png) 

**Figure 19 - Best Model DecisionTreeClassifier Confusion Matrix with ROC Plot**



### 5.2.3   Feature engineering and exploration 

 Figure 20 provides the important features there were the top selected feaures by the Decision Tree model.

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/bin_permutation_importance.png) 

**Figure 20 - Important features selected by the best model**

Base on the results presented in Figure 20, following are the important features identified by the model:

a) Seq - 

b) sTtl

c) sHops

d) Cause_Start

e) Proto_icmp

f) Dur

g) sTos

h) pLoss

i) State_RST

j) SyncAck



These features are identified as important features based on binary classification algorithm and accordingly needs to be analyzed further. Using this results of the analysis, the data can be optimzed to improve the execution of the models.



### 5.3.   Multi-class Classification

### 

### 5.3.1 Summary of Assessment Results 

The dataset was split as follows:

```
Xbin_train shape = (850958, 41)
 Xbin_test shape = (364697, 41)
ybin_train shape = (850958,)
 ybin_test shape = (364697,)
```

Following is a sample view of the normal data:

|      |       Seq |       Dur |      sTos |      sTtl |     sHops |   TotPkts |   DstPkts | dMeanPktSz |      Load |   SrcLoad |      Loss |   SrcLoss |  DstLoss |    pLoss |    TcpRtt |    SynAck |    AckDat | Proto_icmp | Proto_ipv6-icmp | Proto_sctp | Proto_tcp |   sDSb_39 |    sDSb_4 |   sDSb_52 |   sDSb_54 | sDSb_af11 | sDSb_af12 | sDSb_af41 |  sDSb_cs4 |  sDSb_cs6 |  sDSb_cs7 | Cause_Shutdown | Cause_Start | State_ACC | State_CON | State_FIN | State_INT | State_REQ | State_RSP | State_RST | State_TST |
| ---: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | ---------: | --------: | --------: | --------: | --------: | -------: | -------: | --------: | --------: | --------: | ---------: | --------------: | ---------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | -------------: | ----------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: |
|    0 |  2.070873 | -0.807021 | -0.069237 | -0.329345 | -0.352366 | -0.165054 | -0.111893 |  -0.287842 | -0.008214 | -0.010969 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 |  1.031632 | -0.007511 | -0.257647 | -0.004336 |
|    1 | -0.619749 |  0.715383 | -0.069237 | -0.329345 | -0.352366 | -0.125414 | -0.111893 |  -0.287842 | -0.008214 | -0.010957 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 |  1.031632 | -0.007511 | -0.257647 | -0.004336 |
|    2 | -0.781195 | -0.807021 | -0.069237 | -0.329345 | -0.352366 | -0.165054 | -0.034843 |   0.018933 | -0.008214 | -0.010969 | -0.091038 | -0.074202 | -0.06135 | -0.09457 |  5.078216 |  0.081540 |  8.386164 |   -0.15843 |       -0.001533 |  -0.060035 |  1.834878 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 | -0.969338 | -0.007511 |  3.881275 | -0.004336 |
|    3 | -0.967806 |  0.720621 | -0.069237 | -0.329345 | -0.352366 | -0.125414 | -0.111893 |  -0.287842 | -0.008214 | -0.010958 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |      -0.024247 |   -0.816894 | -0.030114 | -0.349244 | -0.226162 | -0.608926 |  1.031632 | -0.007511 | -0.257647 | -0.004336 |
|    4 |  0.583671 |  0.715967 | -0.069237 | -0.329345 | -0.352366 | -0.125414 | -0.111893 |  -0.287842 | -0.008214 | -0.010957 | -0.091038 | -0.074202 | -0.06135 | -0.09457 | -0.265714 | -0.044344 | -0.388247 |   -0.15843 |       -0.001533 |  -0.060035 | -0.544995 | -0.001084 | -0.007817 | -0.010342 | -0.001084 | -0.025616 | -0.010455 |   -0.0204 | -0.009199 | -0.023307 | -0.020687 |                |             |           |           |           |           |           |           |           |           |



### 5.3.2   Multi-class Classification Model Comparison

TDB - pending completion of program execution - becasue of the size of the data, the program has been running for over a week now and is partially complete, i.e., binary classification is done but the multi-class classification part is still executing and that is why these sections are marked as TBD



### 5.3.3   Feature engineering and exploration 

TDB - pending completion of program execution - becasue of the size of the data, the program has been running for over a week now and is partially complete, i.e., binary classification is done but the multi-class classification part is still executing and that is why these sections are marked as TBD





### 6.0   Deployment

- becasue of the size of the data, the program has been running for over a week now and is partially complete, i.e., binary classification is done but the multi-class classification part is still executing and that is why these sections are marked as TBD

### 6.0.1   Summary

TDB - pending completion of program execution 



### 6.0.2   Recommendation

TDB - pending completion of program execution 



### 7.0   Next Steps

TDB - pending completion of program execution 
