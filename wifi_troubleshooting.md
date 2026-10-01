INC-001 — Intermittent Wi-Fi connectivity

Date: 1 October 2026
Device: Windows laptop
Issue: Intermittent / poor Wi-Fi connection

Initial symptoms:
- Other devices on the same Wi-Fi were working normally.
- Laptop connection was intermittent.
- Internet requests were sometimes timing out.
- Ping latency was often very high.

Initial assessment:
Because other devices were functioning normally, the issue appeared
to be isolated to the laptop rather than the router or internet
connection.

Investigation:

1. Checked Wi-Fi connection
2. Tested connectivity using ping on both mobile hotspot and the wifi network
3. Compared results with another device
4. Forget wifi connection 
5. Identified adapter as Intel Wireless-AC 9461
6. Disabled and renebaled the wireless adapter
7. Re-tested connection
8. netsh wlan show interface

## Findings

* Pinging the mobile phone hotspot returned an average response time of approximately **8 ms**.
* Pinging the problematic Wi-Fi network produced very poor results:

Packets: Sent = 4, Received = 2, Lost = 2 (50% loss)

Approximate round trip times in milli-seconds:
    Minimum = 1452ms, Maximum = 1514ms, Average = 1483ms

* Another laptop was tested from the same distance from the modem and was able to ping the network with significantly better results, suggesting the issue was specific to the affected laptop rather than the Wi-Fi network itself.
* Forgetting and reconnecting to the Wi-Fi network produced the same result.
* Disabling and re-enabling the Wi-Fi network adapter produced the same result.
* Running `netsh wlan show interfaces` showed a **52% signal strength** on the problematic Wi-Fi network.
* When connected to the nearby mobile hotspot, the same laptop showed **97% signal strength**, with a receive and transmit rate of **72.2 Mbps**.
* These results indicate that the laptop is capable of establishing a good Wi-Fi connection at close range, but its connection quality and performance deteriorate significantly with distance from the Wi-Fi source.


Resolution:


Verification:


