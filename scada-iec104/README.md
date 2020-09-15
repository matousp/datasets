<h3>This directory contains datasets described in the paper submitted to IM 2020 conference.</h3>
<br>
(c) Petr Matoušek, Faculty of Information Technology, Brno University of Technology, Czech Republic
<br>
Contact: matousp@fit.vutbr.cz
<br>
The CSV files below were obtained from the IPFIX flow probe with IEC 104 support. Original PCAP files 
were captured at the research lab of the Faculty of Electrical Engineering and Communication, Brno University of Technology.

* iec104-traffic/ - contains IEC 104 flows in CSV format 
   * iec104-ioa.csv - 2:25 min of the traffic, 64x IEC 104 packets
   * mega104-17-12-18-ioa.csv - 2 days and 19:55:08 hours of the traffic, 58.929x IEC 104 packets
   * mega104-14-12-18-ioa.csv - 15:38:01 hours of the traffic, 14.342x IEC 104 packets
   * 13122018-mega104-iao.csv - 2 days and 23:17:39 hours of the traffic, 874.697x IEC 104 packets
   * 10122018-104Mega-ioa.csv - 04:53:21 hours of the traffic, 62.676x IEC 104 packets

* attacks/ - contains cyber attacks on IEC 104 communication
          - the attacks were emulated using normal traffic obtained from mega104-17-12-18-ioa.csv file.
          - see Readme.txt for details about the attacks 
   * injection-attack.csv
   * raw-device.csv
   * dos-attack.csv
   * scanning-attack.csv
   * switching-attack.csv
   * connection-loss.csv
   * normal-traffic.csv
 
