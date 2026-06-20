# 📝 Web Pentesting & Bug Bounty Notes
> **Rule 1:** Internet ki kisi bhi website ya target par kaam shuru karne se pehle yeh **Reconnaissance (Information Gathering)** phase lazmi follow karna hai. Direct attack nahi karna, pehle target ko samajhna hai.
> 
## 🛠️ Step 1: WHOIS Lookup (Owner aur Identity ki Pehchan)
**Command:**
```bash
whois target.com

```
 * **Yeh kya batati hai?** Website kis company ya bande ke naam par register hai (Registrant Name), un ka email, aur kaun se Name Servers use ho rahe hain.
 * **Hacker Logic / Faida:** 1. **Scope aur Assets:** Is se main company ke owner ka naam (jaise *Fairfax Digital*) pata chalta hai. Phir hum internet par us owner ke baaki chupe hue domains aur assets bhi dhoond sakte hain jahan security kamzor ho sakti hai (**Pivot Attack**).

---

   2. **Legal Safety:** Yeh confirm karta hai ke hum sahi target par hain aur ghalti se kisi aisi IP ya website par scan nahi maar rahe jo scope mein nahi hai, taake hum kisi legal action (FIR/Case) se bachein.

---

   3. **Social Engineering / Phishing:** Agar Admin ka naam ya contact mil jaye, toh hacker unhi ke mutabiq fake login page (jaise WordPress Login clone) banakar phishing email bhejte hain taake Admin ka password mil jaye.
## 🛠️ Step 2: DNS IP Records (Target ka Asal Ghar ka Pata)
**Command:**
```bash
dig target.com A +short

```
 * **Yeh kya batati hai?** Website kis IP address par chal rahi hai.
 * **Hacker Logic / Faida:** 1. **Hosting Provider ki Pehchan:** IP address se pata chalta hai ke website kahan hosted hai (jaise *WordPress VIP* ya *AWS*). Agar WordPress VIP ka IP hai, toh operating system bohot tight hoga, is liye hamara poora focus sirf web-plugins aur custom code par hona chahiye.
   2. **Reverse IP Lookup (Shared Hosting Check):** Hum check karte hain ke kya is ek hi IP address par baaki aur logon ki websites bhi chal rahi hain? Agar chal rahi hain aur hamara main target bohot secure hai, toh hum usi IP par maujood kisi doosri kamzor website ko hack karke server ke andar ghustay hain aur phir wahan se main target ki files access kar lete hain (**Symlink Bypass / Cross-Site Contamination**).
## 🛠️ Step 3: Name Servers Identification (DNS Route)
**Command:**
```bash
dig target.com NS

```
 * **Yeh kya batati hai?** Target ka DNS record kaun manage kar raha hai (jaise awsdns-*.com yani Amazon Route 53).
 * **Hacker Logic / Faida:** 1. **Cloud Infrastructure:** Agar AWS Route 53 ya Cloudflare dikhe, toh samajh lo ke peeche **Cloud Servers** (kisi doosri bari company ke high-security servers jo rent par liye gaye hain) chal rahe hain.
   2. **Bypassing Firewalls:** Cloud servers par firewalls (WAF) bohot sakhth hote hain. Is liye hum requests ki speed bohot slow rakhte hain (jaise 2 second mein 1 request) taake firewall detect na kare aur hum security bypass kar sakein.
   3. **DNS Vulnerabilities:** Purane name servers par **DNS Zone Transfer (axfr)** ya **DNS Takeover** ke bugs check kiye jaate hain jin se ek hi jhatke mein saare subdomains leak ho jaate hain.

---

## 🛠️ Step 4: MX Records (Mail Servers Check)
**Command:**
```bash
dig target.com MX

```
 * **Yeh kya batati hai?** Website ke email incoming servers kaun se hain (jaise Google Workspaces, Outlook, ya unka apna server).
 * **Hacker Logic / Faida:** * Agar yahan koi specific mail server response de (jaise ANSWER: 1), toh hum us mail server ka version check karte hain ke kahin woh out-dated toh nahi. Agar response khali aaye (ANSWER: 0), toh iska matlab is specific domain par direct emails handle nahi ho rahi hain.
## 🛠️ Step 5: Subdomain Enumeration (Attack Surface Barhana)
**Command:**
```bash
assetfinder --subs-only target.com

```
 * **Yeh kya batati hai?** Main domain ke sath jitne bhi subdomains connected hain un ki list nikalta hai (jaise www., events., staging.).
 * **Hacker Logic / Faida:** 1. Main website par hamesha heavy security hoti hai, lekin subdomains aksar kam secure hote hain.

---

   2. **Staging Subdomains (staging.target.com):** Yeh developers ka test area hota hai jahan naye features test kiye jaate hain. Yahan aksar firewalls (WAF) off hote hain, error messages khule hote hain jo database ka structure leak karte hain, aur bina password ke testing admin panels mil jaate hain. Yeh hackers ke liye **Gold Mine** hote hain.
## 🛠️ Step 6: Connectivity & Route Testing
**Commands:**
```bash
ping -c 4 target.com
traceroute target.com

```
 * **Yeh kya batati hain?** Target server live hai ya nahi, aur hamare computer se lekar target server tak traffic kin-kin raaston (hops) se guzar kar ja rahi hai.
 * **Hacker Logic / Faida:** * Agar ping mein packet loss dikhe lekin traceroute complete ho raha ho, toh iska matlab hai ke server up hai aur sahi kaam kar raha hai, bas unho ne firewall lagaya hua hai jo automated ping requests ko block kar raha hai.

---

## 💡 Cloud Bucket Misconfiguration (Extra Note)
 * **Concept:** Cloud par website ka data (images, backups, files) store karne ke liye "Buckets" (jaise AWS S3) use hoti hain.
 * **Hacker Kaise Dhoondta Hai?** Website par right-click karke View Source check kiya jata hai. Agar images ke links mein s3.amazonaws.com/bucket-name dikhe, toh woh bucket ka URL hota hai. Agar developer ghalti se iski permission "Public" chor de, toh hacker bina kisi hacking ke un ka sensitive data aur backups download kar leta hai.

---