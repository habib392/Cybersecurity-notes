# Target Reconnaissance: Finding Website IP Addresses

Cyber Security aur Red Teaming (Information Gathering) ke dauran, kisi bhi target website ka IP address nikaalna sab se pehla aur ahem qadam hota hai. Linux terminal par is kaam ke liye kayi tools hain, lekin un ka maqsad aur use-case alag hota hai.

---

## 🏆 Most Used Commands (Jo Sab Se Zyada Use Hoti Hain)

### 1. `host` (Quickest & Simple)
* **Maqsad:** Agar aap ko faltu ki details nahi chahiye aur sirf to-the-point IP address dekhna ho, to yeh sab se behtareen aur fast command hai.
* **Command:**

```
  host kali.org
```


Why it's used:** Yeh aik line mein domain ka IPv4, IPv6 aur Mail Servers (MX records) nikaal kar de deti hai.

### 2. `dig` (Domain Information Groper)

* **Maqsad:** Yeh tool Cyber Security Professionals aur Network Administrators ka **sab se pasandida tool** hai kyun ke yeh poori DNS (Domain Name System) ki kundli nikaal leta hai.
* **Command:**

```
dig kali.org
```



* **Why it's used:** Yeh output ko bohot structured format mein dikhata hai (jaise `ANSWER SECTION`). Is se hamin pata chalta hai ke DNS query mein kitna time laga aur kaun sa DNS server (`8.8.8.8`) use hua.

---

## 🔍 Other Important Tools & Advanced Commands

### 3. `nslookup` (Name Server Lookup)

* **Maqsad:** Yeh aik purana aur legacy tool hai jo Linux aur Windows dono par chalta hai.
* **Command:**

```
nslookup kali.org
```


* **Why it's used:** Jab aap ko kisi aisi machine par kaam karna ho jahan `dig` install nahi hai (jaise Windows environment), wahan `nslookup` kaam aata hai.

### 4. `ping` (Live Check + IP)

* **Maqsad:** Asal kaam yeh check karna hai ke target server online (live) hai ya nahi, lekin yeh sath hi IP address bhi resolve kar leta hai.
* **Command:**
```
ping -c 3 kali.org
```



* **Why it's used:** Is se hamin Network Latency (RTT/time in ms) aur Packet Loss ka pata chalta hai. `-c 3` lagana zaroori hai taake sirf 3 packets chal kar command ruk jaye.

### 5. `traceroute` (Network Path Mapping)

* **Maqsad:** Yeh sirf IP nahi batata, balkay yeh batata hai ke aap ke computer se nikal kar packet kin kin routers (hops) se hota hua target server tak pouncha.
* **Command:**

```
traceroute kali.org
```



* **Why it's used:** Red Teaming mein Network Infrastructure ko map karne aur firewall ki sahi location dhoondne ke liye yeh command use hoti hai.

### 6. `curl` (Web Header Inspection)

* **Maqsad:** Terminal se website ko request bhej kar us ke response headers mein se IP aur server information nikaalna.
* **Command:**

```
curl -I [https://kali.org](https://kali.org)
```




* **Why it's used:** Is se yeh pata chalta hai ke website ke peechay kaun sa web server (jaise Nginx, Apache) chal raha hai aur kya koi Cloudflare jaisi security lagayi gayi hai ya nahi.

---

## 🎯 Summary Table for Quick Reference

| Command | Primary Purpose (Asal Kaam) | Output Depth (Detail) | Best Use Case |
| --- | --- | --- | --- |
| **`host`** | Quick IP Lookup | Low (To the point) | Jab jaldi se sirf IP dekhna ho |
| **`dig`** | Advanced DNS Query | High (Detailed sections) | **Industry Standard** for Recon |
| **`nslookup`** | Basic DNS Query | Medium | Cross-platform (Windows/Linux) |
| **`ping`** | Server Availability Check | Low | Network troubleshooting & latency check |
| **`traceroute`** | Route Path Discovery | High (Hop-by-hop path) | Network mapping & firewall detection |
| **`curl -I`** | Web Server Inspection | Medium (HTTP Headers) | Web technology fingerprinting |

---

*Notes compiled during Linux training labs for Cyber Security roadmap.*


---
