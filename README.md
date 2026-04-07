# DPDK Testing

This repo holds the Containerfiles to create container images to run `pktgen` and `testpmd` to perform traffic tests between two pods in a Kubernetes cluster. It also includes the pod definitions and the commands required to emulate traffic for testing and troubleshooting.

## Run testpmd

```bash
dpdk-testpmd -l 4,6,8,10,12 -n 8 -a 0000:22:09.3 -a 0000:22:19.2 --socket-mem=1024,0 --log-level=10 -- --socket-num=0 --port-numa-config=0,0,1,0 --nb-cores=4 --mbcache=512 --rxq=4 --txq=4 --rxd=8192 --txd=8192 --burst=64 --forward-mode=mac --eth-peer=0,da:1e:b6:ec:0f:f6 --eth-peer=1,16:bd:de:d9:cb:18 -a -i

```

## Run pktgen

```bash
pktgen -v -l "4,6,8,10,12" -a 0000:22:09.2 -a 0000:22:19.1 -n 8 --socket-mem=1024,0 --in-memory -- -m [6,8].0 -m [10,12].1
 
 
set 0 dst mac 82:29:9f:c0:9d:62
set 1 dst mac 7a:7d:7f:8d:24:c9
set 0,1 proto udp
set 0,1 rate 30
set 0,1 size 1500
set all burst 64
start 0,1
stop 0,1

```
