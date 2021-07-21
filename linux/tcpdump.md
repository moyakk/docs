## tcpdump

### Usage

```
$ tcpdump -h
tcpdump version 4.9.3
libpcap version 1.9.1 (with TPACKET_V3)
OpenSSL 1.1.1f  31 Mar 2020
Usage: tcpdump [-aAbdDefhHIJKlLnNOpqStuUvxX#] [ -B size ] [ -c count ]
                [ -C file_size ] [ -E algo:secret ] [ -F file ] [ -G seconds ]
                [ -i interface ] [ -j tstamptype ] [ -M secret ] [ --number ]
                [ -Q in|out|inout ]
                [ -r file ] [ -s snaplen ] [ --time-stamp-precision precision ]
                [ --immediate-mode ] [ -T type ] [ --version ] [ -V file ]
                [ -w file ] [ -W filecount ] [ -y datalinktype ] [ -z postrotate-command ]
                [ -Z user ] [ expression ]
```

### 자주 사용되는 옵션

- -i interface
  - 지정된 인터페이스로 들어오는 패킷만 출력한다.
  - 특별히 지정하지 않은 경우, 시스템의 인터페이스 목록에서 가장 낮은 숫자를 고른다.
  - any 라고 지정할 경우 모든 인터페이스의 패킷을 출력한다.
- -v, -vv, -vvv
  - 패킷의 내용을 조금 더 상세하게 출력한다.
- -x, -xx
  - 패킷을 16진수 형식으로 출력한다.
- -c count
  - 지정된 수의 패킷만 출력하고 종료한다.
- -w file, -r file
  - 패킷을 화면에 출력하는 대신 파일에 기록한다.
  - 기록된 파일은 -r 옵션을 통해 다시 읽을 수 있다.
- -C file_size
  - -w 옵션을 이용해 패킷을 파일에 기록하면서, 지정된 사이즈를 넘어서는 경우 파일을 분할한다.
- -n
  - 주소를 네임으로 변환하지 않고 숫자 그대로 출력한다.

### 필터

- Expression Type : host, net, port
- Directions : src, dst
- Protocols : tcp, udp, icmp, ...

다음과 같이 사용 될 수 있다.
- 출발지 또는 도착지의 주소가 192.168.0.10 인 패킷을 출력한다.
```
tcpdump host 192.168.0.10
```
- 출발지의 주소가 192.168.0.10 인 패킷을 출력한다.
```
tcpdump src 192.168.0.10
```
- 도착지의 주소가 192.168.0.10 인 패킷을 출력한다.
```
tcpdump dst 192.168.0.10
```
- 출발지 또는 도착지의 포트가 8080 인 패킷을 출력한다.
```
tcpdump port 8080
```
- 출발지의 포트가 8080 인 패킷을 출력한다.
```
tcpdump src port 8080
```
- 도착지의 포트가 8080 인 패킷을 출력한다.
```
tcpdump dst port 8080
```
- 포트 번호를 범위로 지정하는 경우
```
tcpdump portrange 1000-2000
```

필터 조건은 and, or, not 옵션으로 조합 할 수 있다.
- 출발지의 주소가 192.168.0.10 이면서 도착지의 포트가 8080 인 패킷을 출력한다.
```
tcpdump src 192.168.0.10 and dst port 8080
```
- 출발지의 주소가 192.168.0.10 이면서 도착지의 포트가 22 가 아닌 패킷을 출력한다.
```
tcpdump src 192.168.0.10 and src port not 22
```

## 네트워크 인터페이스 목록을 확인하는 방법

### ip

```
$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 0c:c4:7a:c4:90:e8 brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.248/24 brd 192.168.0.255 scope global noprefixroute eno1
       valid_lft forever preferred_lft forever
3: eno2: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast state DOWN group default qlen 1000
    link/ether 0c:c4:7a:c4:90:e9 brd ff:ff:ff:ff:ff:ff
```

조금 더 간략히 보려면

```
$ ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 0c:c4:7a:c4:90:e8 brd ff:ff:ff:ff:ff:ff
3: eno2: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast state DOWN mode DEFAULT group default qlen 1000
    link/ether 0c:c4:7a:c4:90:e9 brd ff:ff:ff:ff:ff:ff
```

### netstat

```
$ netstat -i
Kernel Interface table
Iface             MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
eno1             1500   447339      0      0 0        478545      0      0      0 BMRU
eno2             1500        0      0      0 0             0      0      0      0 BMU
lo              65536  2158838      0      0 0       2158838      0      0      0 LRU
```
