# Topology

```


                   +--+
            +------+s2+------+
            |      +--+      |
+--+      +-++              ++-+       +--+--+
|h1+------+s1|              |s4+-------+h2/h3|
+--+      +-++              ++-+       +--+--+
            |                |
            |      +--+      |
            +------+s3+------+
                   +--+


```

Start a Virtulabox in headless fashion:

VBoxManage startvm p4-learning --type headless


ssh to Virtualbox :

ssh -p 22 p4@127.0.0.1 (see the port number as per your VBox settings

For switch tables:

cmd: simple_switch_CLI --thrift-port 9091

output:

RuntimeCmd: table_dump MyIngress.ipv4_lpm
==========
TABLE ENTRIES
**********
Dumping entry 0x0
Match key:
* ipv4.dstAddr        : LPM       0a000100/24
Action entry: MyIngress.ipv4_forward - 0a000102, 01
**********
Dumping entry 0x1
Match key:
* ipv4.dstAddr        : LPM       0a000000/8
Action entry: MyIngress.ipv4_forward - 0a000102, 02
==========
Dumping default entry
Action entry: MyIngress.drop - 
==========

Note: Traffic 10.0.2.2 is the traffic from s1-s2-s4

Traffic 10.250.250.2 is also from s1-s2-s4

send packets via iperf script: iperfs.sh

fail_and_reroute() API in controller.py during populate works with different delays which fails a link and reroutes the packets and simulates control plane convergence

So just run with this in controller and you are good instead of manually failing the link via mininet by using: mininet> link s1 s2 down

For Shortcut, there is no delay and the traffic rightaway takes the S1-S3 path instead of S1-S2-S1-S3 with loops (for existing FRRs)

## How to run

Run the topology in mininet:

```
sudo p4run
```

Runs controller and populates 2000 entries:
```
sudo python controller populate 2000
```

Note: once topology is set try to ping from one host to another:

```
mininet> h1 ping h2
```

data values:

Median throughput for us: 52.4, 51.4, 43, 40.9, 33.05, 0, 15.7, 13.6, 52.4, 48.2, 66.1, 47.2, 64, 46.1, 47.2, 64, 46.1, 55

Median throughput for controller: 35.7, 51.4, 53.5, 37.7, 18.9, 0, 0, 0, 0, 0, 0, 0, 50.3, 46.1

Median Throughput new for us= 49.8, 40.5, 36.2, 0, 13, 52.45, 55, 57.5, 51.1, 54.3, 54.5, 55

Median for Control Plane Convergence = 49.9, 40.4, 36.1, 0, 0, 0, 0, 0, 0, 0, 43.1, 53.7

For FRR: one can follow: https://frrouting.org/ 

For P4: one can follow: https://github.com/nsg-ethz/p4-learning



