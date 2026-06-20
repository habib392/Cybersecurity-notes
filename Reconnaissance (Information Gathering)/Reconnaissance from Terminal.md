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

# Next Command

### Command: Technology Detection (`whatweb`)

Apne terminal mein sab se pehle yeh command run karein:

```bash
whatweb https://staging.nineforbrands.com.au

```

---

### 📚 Is Command Ki Poori Detail:

#### 1. Is mein kaun sa Tool use ho raha hai?

Is mein **`whatweb`** naam ka tool use ho raha hai. Yeh Kali Linux mein pehle se installed hota hai. Is ka kaam website ke chehre (frontend code) ko dekh kar yeh pehchanna hota hai ke us ke peeche kaun kaun si technologies chupi hui hain.

#### 2. Yeh kya hai aur is se hum kya kar sakte hain?

Jab aap yeh command chalate hain, toh yeh website ko hack nahi karti, balkeh us se aik normal request karke uska "HTTP Header" aur "Source Code" check karti hai. Is se humein yeh pata chalta hai:

* Website par kaun sa **Web Server** chal raha hai (jaise Nginx ya Apache).
* Us par kaun sa **CMS (Content Management System)** hai (jaise WordPress, Drupal, ya Joomla) aur uska exact **Version** kya hai.
* Website mein kaun kaun se programming languages aur JavaScript libraries (jaise jQuery, React) use ho rahi hain.

#### 3. Agar is command se data mil gaya, toh hum us se kya faida utha sakte hain? (Hacker Logic)

* **Outdated Version Attack:** Farz karein `whatweb` aap ko batata hai ke website par `WordPress 5.8` chal raha hai. Aap foran Google ya Exploit-DB par ja kar search karenge: *"WordPress 5.8 Known Vulnerabilities / Exploits"*. Agar us version mein koi purana public bug (CVE) hua, toh aap ko website ke andar ghusne ka direct rasta mil sakta hai.
* **Exploit Tailoring (Targeted Attack):** Agar aap ko pata chal jaye ke server **Nginx** use kar raha hai, toh aap apna bohot sa waqt zaya hone se bacha lete hain kyunki ab aap Apache server par hone wale attacks is website par try nahi karenge. Aap sirf Nginx-specific cheezein dhoondein ge.
* **Staging vs Production Comparison:** Hum ne yeh command **`staging.`** wale subdomain par chalayi hai. Agar main website (`www.`) par WordPress ka version bilkul naya aur secure hua, lekin staging par developers ne purana version chora hua, toh hamara rasta clear ho jaye ga.

---

## Output from terminal 

**Yeh website ki orignal domain pr command nhi chalayi balky subdomain pr chalyi hai**

┌──(habib㉿kali)-[~]

└─$ whatweb https://staging.nineforbrands.com.au

https://staging.nineforbrands.com.au [401 Unauthorized] Country[UNITED STATES][US], HTTPServer[nginx], IP[34.151.94.237], Title[401 Authorization Required], WWW-Authenticate[ninestage][Basic], nginx 


### 🔍 Output Ka Post-Mortem Aur Hacker Logic

Aap ke terminal ne yeh data diya:

> `https://staging.nineforbrands.com.au [401 Unauthorized] Country[UNITED STATES][US], HTTPServer[nginx], IP[34.151.94.237], Title[401 Authorization Required], WWW-Authenticate[ninestage][Basic], nginx`

Hum is se yeh 4 baray points nikal sakte hain:

#### 1. `[401 Unauthorized]` aur `[401 Authorization Required]`

* **Yeh kya hai?** Jab aap ne is url par request bheji, toh server ne aage se aam website dikhane ke bajaye rasta rok liya aur kaha ke *"Pehle apni pehchan (username/password) do, tabhi andar jaane dunga."*
* **Hacker Logic / Faida:** Is ka matlab hai ke yeh website public ke liye nahi hai balkeh developers ka private area hai. Jab aam browser mein isay khola jaye ga, toh samne ek pop-up box (prompt) aa jaye ga jo username aur password maangta hai. Isay **HTTP Basic Authentication** kehte hain.

#### 2. `WWW-Authenticate[ninestage][Basic]`

* **Yeh kya hai?** Yeh us login prompt ka "Realm Name" (naam) hai jo developers ne rakha hai: **`ninestage`**.
* **Hacker Logic / Faida:** Yeh cheez confirm karti hai ke yeh `nineforbrands` ka hi testing environment (staging area) hai aur yeh "Basic" auth use kar raha hai.

#### 3. `HTTPServer[nginx]` aur `nginx`

* **Yeh kya hai?** Is website ke peeche jo software server chal raha hai, uska naam **Nginx** hai.
* **Hacker Logic / Faida:** Pehle jab hum ne main domain ka IP check kiya tha, toh lag raha تھا ke woh WordPress VIP infrastructure par hai. Lekin is `staging.` subdomain par yeh **Nginx** server chal raha hai. Ab agar hum ne is server par koi vulnerabilities check karni hain, toh hum sirf Nginx se related configuration flaws dhoondein ge, kisi aur server (jaise Apache) ke nahi.

#### 4. `IP[34.151.94.237]`

* **Yeh kya hai?** Yeh is staging subdomain ka exact IP address hai.
* **Hacker Logic / Faida:** Agar aap is IP address ko check karein, toh yeh **Google Cloud Platform (GCP)** ki range mein aata hai. Iska matlab hai ke main website shayed kisi aur network par ho, lekin inka staging server Google Cloud par chal raha hai!

---

### 🤔 Ab Agar Yeh Cheez Find Ho Gayi, Toh Hum Is Se Kya Kar Sakte Hain?

Chunke samne **401 Basic Auth Login Panel** khula hua hai, toh yahan se penetration testing ke do raste nikalte hain:

1. **Brute Force / Dictionary Attack:** Developers aksar testing environments par bohot hi aam ya default passwords rakh dete hain (jaise `admin:admin`, `test:test`, `nine:stage`). Hacker yahan aik wordlist use kar ke automatic login sahi credentials dhoondne ki koshish karte hain (Hydra ya Burp Suite ke zariye). Agar login ho jaye, toh poori staging site hamare samne khul jati hai.
2. **Directory Bruteforcing:** Kuch cases mein basic authentication sirf main page par lagi hoti hai, lekin agar hum is ke aage kisi specific folder ka naam likhein (jaise `/images/` ya `/wp-content/`), toh server ghalti se bina password ke woh directory dikha deta hai jise **Auth Bypass** kehte hain.

---

**Ab yeh command website ky orignal domain pr chalayi**

──(habib㉿kali)-[~]

└─$ whatweb https://www.nineforbrands.com.au    

https://www.nineforbrands.com.au [200 OK] Cookies[__cf_bm], Country[UNITED STATES][US], Frame, Google-Analytics[Universal][UA-150165338-1], Google-Tag-Manager[UA-150165338-1], HTML5, HTTPServer[cloudflare], HttpOnly[__cf_bm], IP[141.193.213.11], JQuery[2.10.1], Open-Graph-Protocol[website], PoweredBy[-nine/,Nine], Script[application/ld+json,speculationrules,text/html,text/javascript], Strict-Transport-Security[max-age=31536000], Title[Nine for Brands], UncommonHeaders[link,referrer-policy,x-content-type-options,x-cacheable,x-cache-group,content-security-policy,cf-cache-status,cf-ray,alt-svc], WordPress, X-Frame-Options[SAMEORIGIN], X-Powered-By, X-XSS-Protection[1; mode=block] 

### 🔍 Output Ka Post-Mortem Aur Hacker Logic

#### 1. `HTTPServer[cloudflare]` aur `Cookies[__cf_bm]`

* **Yeh kya hai?** Website ke aage **Cloudflare** laga hua hai. Cloudflare ek WAF (Web Application Firewall) aur Content Delivery Network (CDN) hai jo website ko cyber attacks aur ddos se bachata hai. `__cf_bm` cloudflare ki apni cookie hai.
* **Hacker Logic / Faida:** Yeh aap ke liye sab se zaroori warning hai. Iska matlab hai agar aap is main site par ab direct koi automatic tool (jaise sqlmap, dirbuster, ya aggressive nmap) chalayenge, toh Cloudflare aap ki requests ko foran detect karke aap ka IP block kar dega.
* **Strategy:** Isko bypass karne ka tareeqa yeh hota hai ke hum website ka "Real Origin IP" dhoondein (jo ke cloudflare ke peeche chupa hota hai) taake hum direct server par attack kar sakein, firewall ke upar se nahi.

#### 2. `WordPress`

* **Yeh kya hai?** `whatweb` ne confirm kar diya ke yeh website **WordPress CMS** par chal rahi hai.
* **Hacker Logic / Faida:** Ab aap ka generic scanning ka waqt bach gaya. Aap ko pata hai ke aap ko Linux ya Windows ke bugs dhoondne ke bajaye sirf aur sirf WordPress core, WordPress themes, aur is par chalne wale plugins ko target karna hai.

#### 3. `JQuery[2.10.1]`

* **Yeh kya hai?** Yeh website par use hone wali ek JavaScript library (jQuery) ka exact version hai.
* **Hacker Logic / Faida:** Yeh version bohot purana lag raha hai. Jab aap Google ya Exploit-DB par search karenge: `"jQuery 2.10.1 Known Vulnerabilities"`, toh aap ko pata chal sakta hai ke kya is mein koi **XSS (Cross-Site Scripting)** ya dusra jana-pechana bug hai jo is website par kam kar jaye.

#### 4. `X-XSS-Protection[1; mode=block]` aur `Strict-Transport-Security`

* **Yeh kya hai?** Yeh website ke security headers hain jo browser ko mazeed secure banate hain.
* **Hacker Logic / Faida:** `mode=block` ka matlab hai ke developer ne basic Cross-Site Scripting (XSS) ko block karne ke liye browser level security on ki hui hai. Is se hacker ko samajh aati hai ke aam ya simple XSS payloads yahan kam nahi karenge, agar XSS dhoondni hai toh firewall/header bypass wale complex payloads lagane parenge.

#### 5. `Google-Analytics[Universal][UA-150165338-1]`

* **Yeh kya hai?** Yeh inka unique tracking ID hai jo website ki traffic monitor karne ke liye use hota hai.
* **Hacker Logic / Faida (OSINT):** Cyber security (OSINT) mein is unique ID (`UA-150165338-1`) ka bohot bara faida hota hai. Agar is company ke 10 mazeed chupe hue domains internet par hain jin ka kisi ko nahi pata, aur unho ne un sub par yehi same analytics ID use ki hui hai, toh hum reverse analytics lookup tools se un ke saare khufia domains ki list nikal sakte hain.

---

### 🔥 Summary (Asal Faida)

Is output ne aap ko andhere se nikal kar clear rasta dikha diya hai:

> "Main website live hai (`200 OK`), WordPress par bani hai, lekin iske aage **Cloudflare Firewall** khada hai aur browser security headers active hain. Is par seedha hamla block ho jayega, is liye pehle ya toh cloudflare bypass dhoondo ya phir un plugins par focus karo jo cloudflare ke zariye filter nahi ho pa rahe."

---

### 1. Main Website (`www.nineforbrands.com.au`) ka Haal:

* **Status:** `200 OK` (Live hai)
* **Security:** Is ke aage **Cloudflare Firewall (WAF)** khada hai, security headers (`X-XSS-Protection`) active hain, aur yeh WordPress VIP ki secure infrastructure par hai.
* **Attack Challenge:** Agar aap is par koi aggressive test ya scanning chalayenge, toh Cloudflare aap ko foran block kar dega. Is par rasta mushkil hai.

### 2. Subdomain (`staging.nineforbrands.com.au`) ka Haal:

* **Status:** `401 Unauthorized` (Basic Auth Login Panel khula hai)
* **Security:** Is ke aage Cloudflare nahi hai, yeh direct **Nginx** server par chal rahi hai aur Google Cloud par host hai.
* **Attack Opportunity:** Chunke yeh developers ka testing area hai, is liye yahan security policies aksar bohot dheeli hoti hain. Agar hum is ke login panel ko crack kar lein ya is ke aage kisi open directory ko dhoond lein, toh humein direct access mil sakta hai.

---

### 🔥 Final Faisla: **Subdomain (`staging.`) par pehle kaam karenge!**

Cyber security ka asool hai: **"Path of Least Resistance"**—yani us raste se jao jahan rukawat sab se kam ho. Main domain par hathi (Cloudflare) khada hai, jabki subdomain par sirf ek kamzor darwaza (Nginx Basic Auth) hai.

Agar hum `staging.` ko pehle target banayein, toh hamare jeetne ke chances zyada hain.

---

### Agla Step (Next Command) Kya Hoga?

Hum `staging.` subdomain par check karenge ke kya developers ne sirf main page par password lagaya hai, ya unho ne baaki folders (directories) ko bhi block kiya hua hai. Is ke liye hum directory scanning ka aik safe test karenge.

---
