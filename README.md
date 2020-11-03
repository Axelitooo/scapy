# scapy

Generation of UDP-Notif packages via scapy (python)

1) make sure you have scapy and python installed (with matching versions)

2) place simulation.py in the same directory as run_scapy

3) place message.json file in parent directory

4) open terminal in said parent directory, and execute run.sh script as root, with the appropriate arguments

SYNTAX :

sudo ./run.sh IPV4 source (w.x.y.z), IPV4 destination (w.x.y.z), INT source port (1000 < x < 10 000), INT destination port (1000 < y < 10 000, y != x), INT packet amount, (x > 0), INT MTU (x > 16 if segmentation, x > 12 if single-packet message), FLOAT sleep time, (x >= 0), STR message type (x = ints or x = json), FLOAT packet loss probability (0 <= x <= 1)

EXAMPLES :

sudo ./run.sh 192.0.2.4 192.0.2.2 9340 9341 1 1500 1 ints 0.001

Sends 1 notification message made of 10 * 2 ** 10 integers. The message is made of 10240 integers, and the segmented header size is 16, which implies a payload size of 1484. Therefore, the expected outcome is 7 segments.

sudo ./run.sh 192.0.2.4 192.0.2.2 9340 9341 2 9000 1 json 0.001

Sends 2 notification messages made from a json file, with a bigger MTU, Depending on the json's size, we can expect several segments, or a single packet.

sudo ./run.sh 192.0.2.4 192.0.2.2 9340 9341 4 1500 1 rand 0.001

Sends 4 notification messages made of 10 * 2 ** x integers (6 <= x <= 12). The message is made of 640 to 40960 integers, and the segmented header size is 16, which implies a payload size of 1484. Therefore, the expected outcome is 1 packet or up to 28 segments.

For each call, source is 192.0.2.4 on port 9340 and destination is 192.0.2.2 on port 9341, there is a 1-second sleeptime between messages and a 0.001 dropping probability for each packet / segment.