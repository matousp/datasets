<h3>IEC 104 datasets</h3>

The following files represent various attacks on IEC 104 communication created using IEC virtual testbed developed by Peter Grofcik at Brno University of Technology, see MATOUŠEK Petr and GROFČÍK Peter. ICS Virtual Testbed. FIT-TR-2021-02, Brno: Faculty of Information Technology BUT, 2021 at https://www.fit.vut.cz/research/publication/12527/.en. The dataset below were captured at the HMI side in the topology. 

The files containe data in CSV format extracted by the IPFIX probe. Each line contains a list of headers of interest extracted from the IEC 104 packet. The fields are as follows: 
   * Timestamp (absolute time)
   * Relative time (in sec, from the start of capturing)
   * Source IP address
   * Destination IP address
   * Source port
   * Destination port
   * IP length (from IP header)
   * APDU lengt (from IEC 104 header)
   * APDU format type (i-format:0x0, s-format:0x1, u-format:0x3), 
   * u-format type (start data transfer:0x01, stop data transfer:0x02, test frame activation: 0x10, test frame confirmation: 0x20, stop data transfer action: 0x04, stop data transfer confirmation: 0x08)
   * ASDU type identification (e.g., single point information M_SP_NA_1:1, interrogation command: C_IC_NA_1:100, etc.), see MATOUŠEK Petr. Description and analysis of IEC 104 Protocol. FIT-TR-2017-12, Brno: Faculty of Information Technology BUT, 2017 at https://www.fit.vut.cz/research/publication/11570/.en.
   * Number of Information objects within a ASDU packet
   * Cause of Transmission (e.g., periodic:1, spontaneous:3, activation:6, confirmation activation:7, etc). 
   * Originator address
   * ASDU address field

Note: Since IEC 104 packet may include multiple APDUs and ASDUs, the IPFIX probe separates these packets into so called virtual IEC 104 packets that are used for further analysis. 

HMI-MITM.csv
------------
 * dataset duration: 16.6.2021, 10:29:12,38 -> 19.6.2021, 13:53:07,15
 * total virtual packets: 557.215
 * Attack 1: command Act (ASDU typeID=100, CoT=6) changed to Spont (ASDU typeID=100, CoT=3). The HMI responses with <100.45> -> unknown cause.
       * The attack starts at 16.6.2021, 20:23:04 and ends at 21:31:34.
 * Attack 2: an attacker changes the value of the object IOA=1 transmitted in ASDU with typeID=1 (SIG) and CoT=20 (interrogation) from value 0x00 to value 0x11. 
       * The attack starts at 17.6.2021, 5:29:45 and ends at 6:52:15. 
 * Attack 3: The attacker changes the value of Activation command (ASDU TypeID=46, double command, CoT=6 Act) from DCO value 0x01 to value 0x11. 
       * The attack starts at 18.6.2021, 22:15:19,53 and ends at 19.6.2021, 02:38:09,93.

HMI-standard.csv
----------------
  * dataset duration: 29.6.2021, 07:08:31,25 -> 01.07.2021, 10:02:26,45  
  * total virtual packets: 381.666
  * no attacks - applied for training normal communication

report-block-HMI.csv
--------------------
  * dataset duration: 26.11.2021, 13:20:48,89 -> 27.11.2021, 13:58:04,38
  * total virtual packets: 84.334
  * Attacker blocks M_SP_NA_1 (ASDU type=1, CoT=20) information (single point) from reaching HMI. Instead, packet (ASDU=3, CoT 20) is received twice. 
    * The attack starts on 26.11.2021 at 23:35:52,75) and ends on 27.11.2021 at 01:47:32,98.

reply-HMI.csv
-------------
  * dataset duration: 25.11.2021, 07:59:50,43 -> 26.11.2021, 13:13:41,88
  * total virtual packets: 248.394
    * attack 1: replaying HMI -> RTU packet -> replay for C_IC_NA_1 Act (ASDU type = 100, CoT 7) 
        * the attack starts at 20:16:31,906 and ends at 22:35:52,1 
    * attack 2:  replaying RTU -> HMI packet -> replay for interrog response for C_IC_NA_1 (ASDU type = 100)            - missing packets <100,6>,<100,7>
        * the attack starts on 26.11.2021 at 07:38:53,03) and ends on 26.11.2021 at 08:49:53,17 

value-change-HMI.csv
--------------------
  * dataset duration: 23.11.2021, 21:01:30,02 -> 25.11.2021, 07:57:14,31
  * total virtual packets: 261.967
  * two attacks: 1 for HMI and 1 for RTU
    * attack 1:  change of HMI -> RTU packet -> change of C_DC_NA_1 (ASDU type=46) request value for IOA 1
        * tha attack starts on 24.11.2021 at 07:22:21,59) and ends on 24.11.2021 at 09:03:01,59.
        * duplicated packets <100,6>,<100,7> -> <100,6>,<100,7>,<100,7> visible on HMI
    * attack 2: visible on HMI: change of RTU -> HMI packet -> change of C_IC_NA_1 (ASDU=100, CoT=6) response for M_SP_NA_1 (single point, ASDU=1, CoT=20)
        * that attack starts on 24.11.2021 at  20:56:23,16 and ends on 24.11.2021 at 22:57:13,48.
        * visible on RTU from 21:09:23.83: additional <100.6> packets until 22:44:33,84
        * not visible on HMI

masquerating-HMI.csv
-------------------- 
  * dataset duration: 27.11.2021, 14:00:44,54 -> 28.11.2021, 12:00:08, 06
  * total virtual packets: 164.760
    * an attacker connected as correct HMI device to a RTU device and generates C_IC_NA_1 (ASDU=100, interrogation) cyclic requests 
    * an attack starts at 14:15:14.73 and continues until 19:11:15.28. 
    * duplicated packets <100,7><100,7> instead of <100,7>

