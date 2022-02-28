<h3>MMS Datasets</h3>
(c) Petr Matoušek, Faculty of Information Technology, Brno University of Technology, Czech Republic
<br>
Contact: matousp@fit.vutbr.cz
<br>

The following datasets contain a set of cyber security attacks on MMS communication that were created manually on the real life communication provided by the G-ICS labs, University of Grenoble Alps, France, see http://lig-g-ics.imag.fr. 

The files include data of interest in CSV format extracted by the IPFIX probe. Each line contains a list of MMS fiels obtained from MMS packets. The fields are as follows: 
   * Timestamp (absolute time)
   * Relative time (in sec, from the start of capturing)
   * Source IP address
   * Destination IP address
   * Source port
   * Destination port
   * IP length (from IP header)
   * MMS type - e.g., 8: initiate request, 9: initiate response, 0: confirmed-request, 1: confirmed response, 3: unconfirmed PDU, see MATOUŠEK Petr. Description of IEC 61850 Communication. FIT-TR-2018-01, Brno: Faculty of Information Technology BUT, 2018 at https://www.fit.vut.cz/research/publication/11832/.en for details.
   * MMS service - for confirmed-requests/responses only, e.g., 0: status, 1: getNameList, 2: identify, 4: read, 5: write, 6: getVariableAccessAttributes, 12: getNamedVariableListAttributes, etc.
   * Confirmed Request Invoked ID
   * Domain ID - only for GetVariableAccessAttributes Request
   * Item ID - only for GetVariableAccessAttributes Request
   * Object Class - only for GetNameList
 
gics-normal.csv
---------------
  communication between 10.10.20.10:102 and 10.10.3.19:50225
  normal communication -> for training
  First packet: 07:08:31.22
  Last packet: 08:43:01.46
  MMS packets: 2707

gics-lost-connection.csv: 
-------------------------
  * two lost connections: 2x
  * missing packets: from 07:20:11.38 to 07:22:01,45 (58 packets)
  * missing packets: from 07:27:41.46 to 07:29:51,53 (63 packets)

gics-modified.csv:
------------------
  1) An attacker modified packets to write requests (0,5), (1,5).
       packets: with Domain ID _Fundamental: 7:26:31.45 (2x), 7:27:11,45 (2x)
  2) An attacker sends cancel requests/error (5,1),(7,1) instead of conf req/resp (0,1), (1,1).
       from 08:10:51,44 to 08:13:51,44 (48x modified packets)

gics-scanning.csv:
------------------
  * The attacker scans resources by (0,1),(1,1), (0,12),(1,12) etc., packets with Invoke Id from 1 to 34.
  * The attack was launched at 7:50:41,51 and ends at 07:53:01:51 (73 packets).

gics-interrupt.csv:
-------------------
  * The attacker tries to interrupt MMS services by spoofed initiate-ErrorPDU (MMS type=10) and conclude-RequestsPDU (MMS type=11)
    * initiate-ErrorPDU: 6x between 07:28:01,46 - 08:02:11.55
    * concludeRequestPDU: 9x between 07:16:51,29 - 08:19:41,44
    