# Wireshark-TCP-HTTP-log-report

## Type of attack that may have caused this network interruption

#### One potential explanation for the website's connection timeout error message is: 
An HTTP/1.1 504 Gateway Time-out (text/html) error message.

#### The logs show that: 
An [RST, ACK] packet was sent to the requesting visitor after the [SYN, ACK] packet was not received by the web server. Then, the visitor received a timeout error message in their browser, and the connection attempt was dropped.

#### This event could be: 
This is a direct DoS SYN flood attack.

## How the attack is causing the website to malfunction
When website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol.
1) The [SYN] packet is the initial request from an employee visitor trying to connect to a web page hosted on the web server.
2) The [SYN, ACK] packet is the web server’s response to the visitor’s request, agreeing to the connection.
3) The [ACK] packet is the visitor’s machine acknowledging the permission to connect.

### Explanation
Initially, the attacker’s SYN request is answered normally by the web server (log items 52-54). However, the attacker keeps sending more SYN requests, which is abnormal. At this point, the web server is still able to respond to normal visitor traffic, which is highlighted and labeled as green. An employee visitor with the IP address of 198.51.100.14 successfully completes a SYN/ACK connection handshake with the web server (log item nos. 55, 56, 58). Then, the employee’s browser requests the sales.html webpage with the GET command and the web server responds (log item no. 60 and 62).In the next 20 rows, the log begins to reflect the struggle the web server is having to keep up with the abnormal number of SYN requests coming
in at a rapid pace. The attacker is sending several SYN requests every second. The rows highlighted and labeled yellow are failed communications between legitimate employee website visitors and the web server.
As you scroll through the rest of the log, you will notice the web server stops responding to legitimate employee visitor traffic. The visitors receive more error messages indicating that they cannot establish or maintain a connection to the web server. From log item number 125 on, the web server stops responding. The only items logged at that point are from the attack. As there is only one IP address attacking the web server, you can assume this is a direct DoS SYN flood attack.

Ref 1: link to document - [Wireshark TCP/HTTP log](https://docs.google.com/spreadsheets/d/1gQHCYDbsO7Kb2GJKIvwKKyC0d2d33UIdhpQVp5SYItQ/edit?gid=218501934#gid=218501934)
