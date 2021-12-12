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

10.0.2.2 is the traffic from s1-s2-s4

10.250.250.2 is also from s1-s2-s4

send packets via iperf script: iperfs.sh

fail_and_reroute() API in controller.py during populate works with different delays which fails a link and reroutes the packets

So just run with this in controller and you are good instead of maulally failing the link via mininet by using: mininet> link s1 s2 down

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

For FRR: one can follow: https://frrouting.org/ 

For P4: one can follow: https://github.com/nsg-ethz/p4-learning
