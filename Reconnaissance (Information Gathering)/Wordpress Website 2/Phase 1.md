# Phase 1

## Output
┌──(habib㉿kali)-[~]
└─$ whois iaggbs.com
   Domain Name: IAGGBS.COM
   Registry Domain ID: 1747273008_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.corporatedomains.com
   Registrar URL: http://cscdbs.com
   Updated Date: 2026-05-28T11:33:37Z
   Creation Date: 2012-09-24T08:16:43Z
   Registry Expiry Date: 2026-09-24T08:16:43Z
   Registrar: CSC Corporate Domains, Inc.
   Registrar IANA ID: 299
   Registrar Abuse Contact Email: domainabuse@cscglobal.com
   Registrar Abuse Contact Phone: 8887802723
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Name Server: DNS1.CSCDNS.NET
   Name Server: DNS2.CSCDNS.NET
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2026-06-22T12:38:15Z <<<

For more information on Whois status codes, please visit https://icann.org/epp

NOTICE: The expiration date displayed in this record is the date the
registrar's sponsorship of the domain name registration in the registry is
currently set to expire. This date does not necessarily reflect the expiration
date of the domain name registrant's agreement with the sponsoring
registrar.  Users may consult the sponsoring registrar's Whois database to
view the registrar's reported date of expiration for this registration.

TERMS OF USE: You are not authorized to access or query our Whois
database through the use of electronic processes that are high-volume and
automated except as reasonably necessary to register domain names or
modify existing registrations; the Data in VeriSign Global Registry
Services' ("VeriSign") Whois database is provided by VeriSign for
information purposes only, and to assist persons in obtaining information
about or related to a domain name registration record. VeriSign does not
guarantee its accuracy. By submitting a Whois query, you agree to abide
by the following terms of use: You agree that you may use this Data only
for lawful purposes and that under no circumstances will you use this Data
to: (1) allow, enable, or otherwise support the transmission of mass
unsolicited, commercial advertising or solicitations via e-mail, telephone,
or facsimile; or (2) enable high volume, automated, electronic processes
that apply to VeriSign (or its computer systems). The compilation,
repackaging, dissemination or other use of this Data is expressly
prohibited without the prior written consent of VeriSign. You agree not to
use electronic processes that are automated and high-volume to access or
query the Whois database except as reasonably necessary to register
domain names or modify existing registrations. VeriSign reserves the right
to restrict your access to the Whois database in its sole discretion to ensure
operational stability.  VeriSign may restrict or terminate your access to the
Whois database for failure to abide by these terms of use. VeriSign
reserves the right to modify these terms at any time.

The Registry database contains ONLY .COM, .NET, .EDU domains and
Registrars.
connect: Network is unreachable

---

#### Pattern bilkul set hai aur pehla step mukammal ho gaya hai. `whois` ka data hamare saamne hai, chalein iska analysis karte hain ke pichli website ke mukabla mein yahan kya farq hai:

---

### 🔍 Is Output Ka Asal Meaning (Analysis)

#### 1. Registrar Detail (`CSC Corporate Domains, Inc.`)

* **Hacker Logic:** Pichli website GoDaddy par thi, lekin yeh website **CSC Corporate Domains** par registered hai. Yeh ek bohot bari enterprise-level service hai jo badi companies aur brands ke domains manage karti hai. Iska matlab hai target corporate level ka hai.

#### 2. Name Servers (`DNS1.CSCDNS.NET`, `DNS2.CSCDNS.NET`)

* **Hacker Logic:** Pichli website behind Cloudflare thi (`ns.cloudflare.com`). Lekin yahan name servers direct CSC ke apne hain. Iska matlab hai ke ho sakta hai yahan central Cloudflare ka WAF default lagaya hua na ho, ya protection ka tier mukhtalif ho.

#### 3. Operational Timeline

* **Creation Date:** 2012-09-24 (Purani aur established website hai).
* **Updated Date:** 2026-05-28 (Haal hi mein is par koi update ya nameserver change hua hai).

> ⚠️ **Note:** Aakhri line mein `connect: Network is unreachable` aaya hai, yeh generic socket timeout ki wajah se aata hai jab WHOIS server ka background operational port response delay kare, hamare data par is se koi farq nahi parta.

---

### 🚀 Ab Chalte Hain Step 2 Par!

Ab is `whois` ke data ki teh tak jaane ke liye, hum check karenge ke is domain ka **Asal IP Address (A Record)** kya hai aur in ka **Mail Server (MX Record)** kahan point kar raha hai.

Apne terminal mein ab yeh command run karein:

```bash
dig iaggbs.com A +short && dig iaggbs.com MX +short

```

## Output 

┌──(habib㉿kali)-[~]
└─$ dig iaggbs.com A +short && dig iaggbs.com MX +short
138.68.170.103
0 iaggbs-com.mail.protection.outlook.com.

---

#### Data hamare saamne hai aur is output ne pichli website ke muqable mein do (2) bohot bade aur solid haqeeqat samne laaye hain. Chalein, is data ki teh tak jaate hain aur dekhte hain ke ek expert hacker is se kya nikalta hai:

---

### 🔍 Is Output Ka Deep Analysis (Teh Tak Janna)

#### 1. IP Address Target (`138.68.170.103`) — DigitalOcean Cloud Hosting!

* **Hacker Logic:** Pichli website behind Cloudflare proxy thi, jis ki wajah se hamein us ka asli server IP nahi mil raha tha. Lekin yahan jo IP mila hai (`138.68.170.103`), yeh **DigitalOcean** ka IP range hai.
* **Asli Server Exposed:** Iska matlab hai ke yeh website direct internet par exposed hai aur is ke aage Cloudflare ka security shield/proxy protection **nahi laga hua**! Hum direct un ke server ko hit kar rahe hain.

#### 2. Mail Server (`iaggbs-com.mail.protection.outlook.com.`) — Microsoft Office 365!

* **Hacker Logic:** In ka corporate email network **Microsoft Office 365 Enterprise** par chal raha hai. Iska matlab hai ke in ki internal communication bohot secure environment mein hai, lekin hamara focus abhi web application server (DigitalOcean) par hi rahega.

---

### 🚀 Agla Kadam: Step 3 (Subdomain Enumeration)

Hum ne main domain (`iaggbs.com`) ka IP nikal liya. Lekin jaisa hum ne pehle discuss kiya tha ke expert hackers sirf main site par nahi baithte, balkeh attack surface ko phelate hain taake bugs milne ke chances barh sakein.

Ab hamare latest blueprint ke mutabiq **Step 3** par chalte hain, taake is company ke baki chhupe huve subdomains ka shajra nikala ja sake.

Apne terminal mein yeh command run karein:

```bash
assetfinder --subs-only iaggbs.com

```

## Output

┌──(habib㉿kali)-[~]
└─$ assetfinder --subs-only iaggbs.com
www.iaggbs.com
iagchat.iaggbs.com
iagchat.dev.iaggbs.com
dev.iag.tenderportal.iaggbs.com
iaggbs.com
forum.dev.procurement.iaggbs.com
www.procurement.iaggbs.com
procurement.iaggbs.com
dev.procurement.iaggbs.com
ess.iaggbs.com
www.dev.iag.tenderportal.iaggbs.com
ssdd.cfs.iaggbs.com
ssdp.cfs.iaggbs.com
ssdq.cfs.iaggbs.com
ssdx.cfs.iaggbs.com
link.iaggbs.com
forum.procurement.iaggbs.com
iaggbs.com
www.iaggbs.com
ssdd.cfs.iaggbs.com
ssdp.cfs.iaggbs.com
ssdq.cfs.iaggbs.com
ssdx.cfs.iaggbs.com
iaggbs.com
iaggbs.com
procurement.iaggbs.com
procurement.iaggbs.com
dev.procurement.iaggbs.com
dev.procurement.iaggbs.com
iag.tenderportal.iaggbs.com
iag.tenderportal.iaggbs.com
dev.iag.tenderportal.iaggbs.com
dev.iag.tenderportal.iaggbs.com
ifcomms.cmt.procurement.iaggbs.com
www.ifcomms.cmt.procurement.iaggbs.com
dev.ifcomms.cmt.procurement.iaggbs.com
www.dev.ifcomms.cmt.procurement.iaggbs.com
iagchat.prod.iaggbs.com
ssdd.cfs.iaggbs.com
ssdp.cfs.iaggbs.com
ssdq.cfs.iaggbs.com
xxx.ssdd.cfs.iaggbs.com
xxx.ssdp.cfs.iaggbs.com
xxx.ssdq.cfs.iaggbs.com
idam-nonprod-signing.iaggbs.com
idam-signing.iaggbs.com
cpanel.iaggbs.com
cpcalendars.iaggbs.com
cpcontacts.iaggbs.com
iaggbs.com
mail.iaggbs.com
webdisk.iaggbs.com
webmail.iaggbs.com
www.iaggbs.com
cpanel.iaggbs.com
iaggbs.com
mail.iaggbs.com
webdisk.iaggbs.com
webmail.iaggbs.com
www.iaggbs.com

---

#### Yeh dekhain, ise kehte hain asli **Attack Surface Expansion**! Kahan hum sirf aik main domain `www.iaggbs.com` par phanse huve the, aur kahan `assetfinder` ne hamein poori company ka khandaan nikaal kar de diya hai.

Bande ke paas jab itna zyada data aa jaye, toh expert hacker yahin par **data ki teh tak jaane** wala rule dubara lagata hai.

---

### 🔍 Is Data Ka Deep Analysis (Teh Tak Janna)

Agar aap ghaur se is list ko dekhein, toh is mein se kuch aesi zard-khez (juicy) targets nikal rahe hain jahan bugs milne ke chances **90% barh jaate hain**:

1. **Development & Staging Environments (Sab Se Khas Raste):**
* `iagchat.dev.iaggbs.com`
* `dev.iag.tenderportal.iaggbs.com`
* `dev.procurement.iaggbs.com`
* `dev.ifcomms.cmt.procurement.iaggbs.com`
* **Hacker Logic:** Developers jab testing karte hain, toh `dev` ya `staging` subdomains par security firewalls (WAF) lagana bhool jaate hain aur purana code chorr dete hain. Yeh hamare prime targets hain.


2. **Internal Portals & Portals (Tender/Procurement):**
* `iag.tenderportal.iaggbs.com` (Tender portal jahan files ya bids upload hoti hain).
* `forum.procurement.iaggbs.com` (Forums jahan log baatein karte hain - yahan XSS ke chances bohot hote hain).


3. **Legacy/Control Panels (Old Infrastructure):**
* `cpanel.iaggbs.com`
* `webmail.iaggbs.com`
* **Hacker Logic:** Yeh cPanel aur Webmail ke direct login portals hain. Agar server purana ho, toh yahan direct exploit mil sakta hai.



---

### 🚀 Agla Kadam: Latest Blueprint Ka Step 4 (Technology Fingerprinting)

Hum ne rule banaya tha ke data dekh kar aglay step par jana hai. Ab hamare paas subdomains ki list aa gayi hai. Hamara **Step 4** tha ke hum in ki technology check karein (`whatweb`).

Lekin pehle hum saare subdomains par `whatweb` chala kar terminal ko load nahi karenge, balkeh sab se pehle hum sirf **main domain** par check karenge, aur un subdomains par check karenge jo sab se unique lag rahe hain.

Apne terminal mein is interesting subdomain par `whatweb` chalayein aur dekhein kya yeh bhi WordPress hai ya yahan technology badal gayi hai:

```bash
whatweb https://dev.procurement.iaggbs.com/

```

# According to Website Rules

## Output

┌──(habib㉿kali)-[~]
└─$ whatweb --custom-header="X-BugCrowd-traffic: habib_kali" https://dev.procurement.iaggbs.com/
/usr/bin/whatweb: unrecognized option `--custom-header=X-BugCrowd-traffic: habib_kali'
Error in processing commandline options - unrecognized option `--custom-header=X-BugCrowd-traffic: habib_kali'

---

#### Yeh jo terminal par error aaya hai na, iska matlab hai ke `whatweb` ke andar `--custom-header` naam ka koi option exist hi nahi karta. Tool ne option ko pehchana nahi aur execute hone se mana kar diya.

Cyber security mein jab ek tool mein custom features na hon, toh tester foran apne baqi tools ka rasta nikaalta hai. `whatweb` mein custom header lagane ke liye `--custom-header` nahi, balkeh **`-H`** ya **`--header`** ka flag istemal hota hai.

Chalein, command ko sahi kar ke dubara try karte hain:

```bash
whatweb --header="X-BugCrowd-traffic: habib_kali" https://dev.procurement.iaggbs.com/

```

### 💡 Ek Aur Tarika (Agar `whatweb` phir bhi nakhre kare):

Agar aap standard `curl` ke zariye pehle sirf is subdomain ke raw headers aur server dekhna chahte hain (jo hum ne blueprint mein seekha tha), toh `curl` mein `-H` ka flag bilkul perfectly kaam karega:

```bash
curl -I -H "X-BugCrowd-traffic: habib_kali" https://dev.procurement.iaggbs.com/

```
## Output
                                                                                                           
┌──(habib㉿kali)-[~]
└─$ whatweb --header="X-BugCrowd-traffic: habib_kali" https://dev.procurement.iaggbs.com/
ERROR Opening: https://dev.procurement.iaggbs.com/ - no address for dev.procurement.iaggbs.com
                                                                                                           
┌──(habib㉿kali)-[~]
└─$ curl -I -H "X-BugCrowd-traffic: habib_kali" https://dev.procurement.iaggbs.com/
curl: (6) Could not resolve host: dev.procurement.iaggbs.com

---

#### Yeh jo error aaya hai na—**`no address for dev.procurement.iaggbs.com`** aur **`Could not resolve host`**—yeh penetration testing ka aik aur bohot bara aur mazy dar sabaq hai!

Iska matlab yeh nahi hai ke aap ki command ghalt hai. Command aap ne 100% sahi chalayi hai. Iska asli matlab hacker logic mein bohot gahra hai:

---

### 🔍 Is Error Ka Asal Matlab (Subdomain ki Teh Tak Jaana)

Subdomain enumeration tools (jaise `assetfinder`) internet par majood purane records, search engines, aur archives se saare subdomains utha lete hain jo kabhi na kabhi exist karte the ya records mein hain.

Lekin jab hum unhein actual hit karte hain aur error aata hai `Could not resolve host`, toh iske **do (2) matlab** hote hain:

1. **Dead or Inactive Subdomain:** Yeh subdomain pehle kabhi tha, lekin ab company ne iska server delete kar diya hai ya iska DNS record khatam kar diya hai. Yani yeh rasta ab internet par zinda nahi hai.
2. **Internal DNS / Private Network:** Yeh subdomain sirf company ke andar ke log (employees) apne private VPN ya internal office network par chala sakte hain, bahar ki dunya ke liye iska DNS public nahi kiya gaya.

---

### 🏁 Data-Driven Rule: Fake/Dead Subdomains Ko Kaise Filter Karein?

Chunke hamare paas `assetfinder` ne bohot lambi list di hai, agar hum ek ek par manually `whatweb` chalayenge aur woh dead nikli, toh hamara bohot time zaya hoga.

Expert hackers is data ki teh tak jaane ke liye pehle yeh check karte hain ke **kaun sa subdomain sach mein zinda (Live) hai aur kis ka IP address mil raha hai.**

Hum wapas apne blueprint ke **Step 2 (DNS Discovery)** wale logic par aayenge aur list ke baqi unique subdomains ko check karenge jo zinda ho sakte hain. Chalein, is unique forum wale portal ko check karte hain ke kya yeh zinda hai ya dead hai:

```bash
dig forum.procurement.iaggbs.com A +short

```

### 🚀 Agar Yeh Bhi Dead Nikla Toh?

Agar iska bhi IP na aaya (`dig` khali raha), toh hum main dashboard wale subdomain ko check karenge jo inka live portal lag raha hai:

```bash
dig procurement.iaggbs.com A +short

```

Aap pehle `forum.procurement` wali `dig` command run karein aur dekhein ke kya iska koi IP address (A record) nikalta hai ya yeh bhi dead rasta hai!

---

## Outputs

┌──(habib㉿kali)-[~]
└─$ dig forum.procurement.iaggbs.com A +short
34.248.189.5
                                                                                                           
┌──(habib㉿kali)-[~]
└─$ dig procurement.iaggbs.com A +short
d1bqwj1jrl12n6.cloudfront.net.

---

#### Hum ne jab `dev.procurement` par check kiya toh woh dead nikla, lekin jab aap ne in dono subdomains par `dig` chalaya, toh hamare saamne **bohot hi mazy dar aur alag kism ka data** aaya hai.

Chalein, is data ki mukammal teh tak jaate hain aur dekhein ke aik professional hacker is se kya nikalta hai:

---

### 🔍 Is Output Ka Deep Analysis (Teh Tak Janna)

#### 1. `forum.procurement.iaggbs.com` ──> **Zinda Target (Live IP: `34.248.189.5`)**

* **Hacker Logic:** Yeh subdomain bilkul zinda (Live) hai! Aur iska IP address (`34.248.189.5`) **AWS (Amazon Web Services)** ka hai.
* Remember, main website DigitalOcean par thi, lekin inka yeh forum wala section Amazon AWS par host ho raha hai. Aur sub se barh kar, is ke aage koi Cloudflare ya Cloudfront ki proxy nahi dikh rahi, direct IP exposed hai! Forums par testing karne ka maza hi alag hota hai kyunki wahan user input boxes bohot zyada hote hain jahan **XSS (Cross-Site Scripting)** ya **Stored HTML Injection** milne ke chances bohot high hote hain.

#### 2. `procurement.iaggbs.com` ──> **AWS CloudFront CDN (`cloudfront.net`)**

* **Hacker Logic:** Yeh target direct IP nahi de raha balkeh **AWS CloudFront** (jo ke Amazon ka ek Content Delivery Network aur caching system hai) ke peeche chhupa hua hai.
* CloudFront aksar basic security features aur optimization ke liye use hota hai. Iska matlab hai is par direct network level attacks nahi chalenge, balkeh is par hamara focus pure web-application testing aur queries parameter par hoga.

---

### 🚀 Agla Kadam: Latest Blueprint Ka Step 4 (Technology Fingerprinting)

Hum ne data nikal kar dead subdomains ko filter kar diya aur live targets ko alag kar liya. Ab bari hai in live targets ki technology check karne ki (`whatweb`), aur yaad rahe—**Bugcrowd Custom Header ke sath!**

Chalein, hamare sequence ke mutabiq is **AWS wale Live Forum** par finger-printing karte hain.

Apne terminal mein yeh command run karein (main ne aap ka custom header bilkul sahi format mein likh diya hai):

```bash
whatweb --header="X-BugCrowd-traffic: habib_kali" https://forum.procurement.iaggbs.com/

```


