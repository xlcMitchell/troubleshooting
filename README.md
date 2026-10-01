# INC-001 — Intermittent Wi-Fi Connectivity

**Date:** 1 October 2026
**Device:** Windows laptop
**Status:** 🟡 Monitoring / Intermittent
**Issue:** Intermittent and poor Wi-Fi connectivity

---

## Initial Symptoms

* Other devices on the same Wi-Fi network were working normally.
* The laptop's connection was intermittent.
* Internet requests were sometimes timing out.
* Ping latency was frequently very high.

### Initial Assessment

Because other devices were functioning normally, the issue initially appeared to be isolated to the laptop rather than the router or internet connection.

---

## Investigation

The following troubleshooting steps were performed:

1. Checked the laptop's Wi-Fi connection.
2. Tested connectivity using `ping` against both a mobile hotspot and the affected Wi-Fi network.
3. Compared the results with another laptop connected from the same location.
4. Forgot and reconnected to the Wi-Fi network.
5. Identified the wireless adapter as an **Intel Wireless-AC 9461**.
6. Disabled and re-enabled the wireless adapter.
7. Re-tested the connection.
8. Used `netsh wlan show interfaces` to examine signal strength and connection rates.
9. Reinstalled the Wi-Fi driver to rule out a driver-related issue.
10. Checked the Wi-Fi antenna connection following the motherboard replacement.
11. Reset the nearby Wi-Fi extender.
12. Re-tested connectivity after resetting the extender.

---

## Findings

### Initial Connectivity Test

Pinging the mobile phone hotspot returned an average response time of approximately **8 ms**.

The affected Wi-Fi connection initially produced significantly worse results:

```text
Packets: Sent = 4, Received = 2, Lost = 2 (50% loss)

Approximate round trip times in milli-seconds:
    Minimum = 1452ms
    Maximum = 1514ms
    Average = 1483ms
```

Another laptop was tested from approximately the same distance from the Wi-Fi equipment and produced significantly better results. This suggested that the issue was not simply a general internet connectivity problem.

### Wi-Fi Signal and Connection Rates

`netsh wlan show interfaces` initially showed:

* **Signal:** 52%
* **Receive rate:** 11 Mbps
* **Transmit rate:** 1 Mbps

When connected to a nearby mobile hotspot, the same laptop showed:

* **Signal:** 97%
* **Receive rate:** 72.2 Mbps
* **Transmit rate:** 72.2 Mbps

This demonstrated that the laptop's wireless adapter was capable of establishing a good connection at close range, while connection quality deteriorated significantly with distance from the Wi-Fi source.

### Additional Troubleshooting

* Forgetting and reconnecting to the Wi-Fi network produced the same symptoms.
* Disabling and re-enabling the wireless adapter produced the same symptoms.
* Reinstalling the Wi-Fi driver did not resolve the issue.
* The Wi-Fi antenna connection was checked and appeared to be connected correctly.
* These results reduced the likelihood of a simple Wi-Fi profile or driver issue.

### Extender Reset

The nearby Wi-Fi extender was reset and the connection improved significantly.

A subsequent connectivity test produced:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)

Approximate round trip times in milli-seconds:
    Minimum = 2ms
    Maximum = 2ms
    Average = 2ms
```

The Wi-Fi interface also subsequently reported substantially improved connection characteristics:

* **Band:** 5 GHz
* **Radio:** 802.11ac
* **Signal:** 83%
* **Receive rate:** 433.3 Mbps
* **Transmit rate:** 390 Mbps

---

## Resolution / Current Status

**Resetting the nearby Wi-Fi extender significantly improved the connection.**

However, the issue has since appeared to become intermittent again. Therefore, the issue is **not currently considered permanently resolved** and remains under observation.

The current evidence suggests that the problem may involve the Wi-Fi extender or the quality of the wireless connection between the laptop and the Wi-Fi equipment. A laptop-side hardware issue, such as the antenna system, has not been completely ruled out.

---

## Verification

Following the extender reset, connectivity was tested using `ping` and `netsh wlan show interfaces`.

The immediate results showed:

* 0% packet loss
* Approximately 2 ms average latency
* 83% signal strength
* 433.3 Mbps receive rate
* 390 Mbps transmit rate

Further testing is required to determine whether these improvements remain stable over time.

---

## Lessons Learned

* Compare the affected device with another device on the same network before assuming the router or internet connection is at fault.
* Test both connectivity and Wi-Fi signal/connection characteristics.
* A device can connect successfully while still having a poor-quality wireless connection.
* Re-testing after each troubleshooting step helps identify which change affected the issue.
* A temporary improvement should not be treated as a permanent resolution without verification over time.
