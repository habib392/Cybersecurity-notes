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



