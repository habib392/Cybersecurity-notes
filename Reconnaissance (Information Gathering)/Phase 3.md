**Phase 3: Manual Vulnerability Research & Analysis**

1. **Gravity Forms (Version 2.10.1)** — Jo out of date hai (Latest: 2.10.4).
2. **Yoast SEO (Version 27.5)** — Jo out of date hai (Latest: 27.8).

Chunke `searchsploit` par hamein direct un ke exploits nahi mile te, toh penetration testing ka rule yeh hai ke ab hum **Google Dorking** aur public **CVE (Common Vulnerabilities and Exposures)** databases par in makhsoos versions ka shajra-e-nasab nikalenge ke in mein kaun se bugs maujood hain jinhein company ne chupke se naye versions mein patch kiya hai.

---

### 🚀 Step 1: Gravity Forms 2.10.1 Ki Shanakht (Research)

Hum sab se pehle browser ya open-source intelligence ka istemal karte hue check karenge ke `2.10.1` aur `2.10.4` ke darmiyan kaun si security vulnerability report hui thi.

Aap ko internet par research karne se pata chalega ke Gravity Forms ke in makhsoos intermediate versions mein aksar **XSS (Cross-Site Scripting)** ya **Broken Access Control** jese gaps milte hain, jahan agar koi user form submit kare toh input sahi tarah sanitize nahi hota.

Lekin hamara target secure environment (Cloudflare) ke peeche hai, is liye hum direct koi offensive tool ya aggressive attack payload nahi phenk sakte (warna firewall foran ban kar dega). Hum bilkul silent aur logical tareeqay se chalenge.

Hum pehle check karenge ke website par Gravity Forms ka default form handle karne wala endpoint publicly accessible hai ya nahi.

Apne terminal mein yeh `curl` command run karein:

```bash
curl -I https://www.nineforbrands.com.au/wp-admin/admin-ajax.php

```

---

### 📚 Is Command Ki Detail (Notes ke liye):

#### 1. Is endpoint (`admin-ajax.php`) ka kya maqsad hai?

WordPress mein jitne bhi forms (jaise Gravity Forms) ya dynamic elements hote hain, woh background mein requests bhejne ke liye **`admin-ajax.php`** ka istemal karte hain. Agar yeh endpoint open hai, toh iska matlab hai ke hum forms ke functions ko backend par request bhej kar query kar sakte hain.

#### 2. Hacker Logic:

Hum dekhna chahte hain ke kya server is file par `200 OK` deta hai ya Cloudflare isay block karta hai? Agar yeh open hai, toh hamare paas Gravity Forms ke specific parameters ko check karne ka rasta khul jata hai.

Isay run karein aur dekhein ke status code kya aata hai!

---

## Output

┌──(habib㉿kali)-[~]
└─$ curl -I https://www.nineforbrands.com.au/wp-admin/admin-ajax.php
HTTP/2 400 
date: Sun, 21 Jun 2026 09:54:58 GMT
content-type: text/html; charset=UTF-8
server: cloudflare
cache-control: no-cache, must-revalidate, max-age=0, no-store, private
expires: Wed, 11 Jan 1984 05:00:00 GMT
status: 400 Bad Request
x-powered-by: WP Engine
x-robots-tag: noindex
x-cacheable: NO:Private
x-cache: MISS
x-pass-why: wp-admin
set-cookie: __cf_bm=MVc780aPQ4BdgBqE0RN_DrASw6L5O3Ejx4j.r9a0aao-1782035696.6107128-1.0.1.1-dpk_UZJnXABbFEhCZF2KOLLtlsP83iJTTEmLGFtmKzFQzXif9PuRfOKu9aOHgCPS1L3fKygAprESwfq4KmGukdeIQcG.TAnmdTlShc3tHCjCiwacG9JEhhOnYR6XfDhJ; HttpOnly; SameSite=None; Secure; Path=/; Domain=www.nineforbrands.com.au; Expires=Sun, 21 Jun 2026 10:24:58 GMT
cf-cache-status: DYNAMIC
cf-ray: a0f2227fcebbc697-KHI
alt-svc: h3=":443"; ma=86400

---

Aap shayad soch rahe honge ke `400` error aaya hai toh rasta band hai, lekin hacker logic ke mutabiq yeh **bohot achi khabar (Positive Result)** hai! Chalein samajhte hain kyun.

---

### 🔍 Is Output Ka Asal Meaning (Hacker Logic)

#### 1. Endpoint Maujood Hai Aur Active Hai! 🎯

WordPress ka default behavior yeh hai ke jab aap `admin-ajax.php` par bina kisi specific data ya query ke khali request (`curl -I`) bhejte hain, toh WordPress ka core backend aap ko **`400 Bad Request`** ya `0` return karta hai. Iska matlab hai ke server ne hamari request ko drop nahi kiya, balkeh request accept kar ke jawab diya ke *"Bhai data toh bhejo!"*

#### 2. Cloudflare Ne Block Nahi Kiya! 🛡️❌

Sab se bari baat: Yeh error Cloudflare ka nahi hai, balkeh **WP Engine (Real Server)** ka apna response hai (`x-powered-by: WP Engine`). Iska matlab hai ke Cloudflare ne `admin-ajax.php` par hamari request ko block (`403`) nahi kiya, rasta bilkul saaf hai!

#### 3. Info Leak (`x-pass-why: wp-admin`)

Header mein ek bohot interesting cheez leak hui hai: **`x-pass-why: wp-admin`**. Yeh WP Engine ka internal caching header hai jo confirm kar raha hai ke yeh request un ke cache ko bypass kar ke direct real backend system par hit kar rahi hai.

---

### 💡 Hacker Logic: Gravity Forms Ko Check Kaise Karein?

Chunke hamara `admin-ajax.php` khula hua hai, toh Gravity Forms plugin backend par data process karne ke liye ek makhsoos "Action" use karta hai.

Gravity Forms ke purane versions (jaise `2.10.1`) mein developers aksar ek default handle check karte hain jise **`gf_`** ya **`gravityforms_`** actions kehte hain. Agar hum sahi action parameters ke sath `POST` request bhejein, toh hum dekh sakte hain ke kya form ka internal file upload ya structure trigger hota hai ya nahi.

Chalein ek advance manual testing karte hain yeh check karne ke liye ke kya hamari request Gravity Forms ke core handler tak pahonchti hai.

Apne terminal mein ab yeh `POST` command run karein (is baar hum sirf status header nahi, balkeh thora sa body data bhejenge):

```bash
curl -d "action=gf_vulnerability_test" https://www.nineforbrands.com.au/wp-admin/admin-ajax.php

```

---

### 📚 Is Command Ki Detail (Notes ke liye):

* **`-d "action=gf_vulnerability_test"`**: Yeh `-d` flag (Data) bhej raha hai. Hum WordPress backend ko ek dummy action parameter bhej kar check kar rahe hain ke server ab `400 Bad Request` deta hai ya hamara data process kar ke koi different response (jaise `0` ya `-1`) deta hai.
---

## Output

┌──(habib㉿kali)-[~]
└─$ curl -d "action=gf_vulnerability_test" https://www.nineforbrands.com.au/wp-admin/admin-ajax.php
0 

---

#### Yeh WordPress penetration testing mein ek bohot hi iconic aur classic response hai.

Chalein is `0` ka asal hacker logic samajhte hain ke is ne hamein kya confirm kar ke diya hai.

---

### 🔍 Is `0` Response Ka Asal Matlab (Analysis)

#### 1. Core WordPress Ajax Architecture Confirm 🎯

WordPress ka rule hai ke jab bhi aap `/wp-admin/admin-ajax.php` par koi `POST` request bhejte hain aur aap ka bheja hua `action` parameter backend par registered nahi hota ya dynamic handler execute ho kar khali hath lautta hai, toh WordPress core hamesha default output mein **`0`** return karta hai.

#### 2. Confirm: Rasta Bilkul Khula Hai! 🚀

Sab se bari baat yeh hai ke hamari request bina kisi rukawat ke direct WordPress core database aur PHP processing engine tak ja kar takraayi hai. Cloudflare ne is `POST` request ke body data ko check kar ke block nahi kiya. Iska matlab hai ke hum safely custom hooks aur parameters test kar sakte hain bina firewall ke darr ke.

---

### 💡 Hacker Logic: Ab Vulnerability Research Ko Agay Kaise Barhana Hai?

Hum ne yeh confirm kar liya ke `admin-ajax.php` open hai aur `0` de raha hai. Ab hum wapas aate hain Gravity Forms ke us makhsoos version (`2.10.1`) par.

Jab hum public CVEs (Common Vulnerabilities and Exposures) aur security advisories ko review karte hain, toh Gravity Forms aur Yoast SEO ke in versions ke darmiyan zyada tar flaws ya toh **Sensitive Information Disclosure** (baaz admin ya config endpoints ka access) ke hote hain ya phir frontend par **Stored/Reflected XSS** ke.

Chunke hamara target `WP Engine` par hosted hai jo ke bohot aggressive automatic internal patching karta hai, is liye aksar unho ne critical execution bugs ko server-level par hi block kiya hota hai.

Ab hamara agla logical qadam yeh hai ke hum check karein ke kya is website ka standard API endpoint open hai, kyunki aksar plugins ke vulnerabilities REST API ke raste se execute hoti hain.

Apne terminal mein yeh single command run karein:

```bash
curl -I https://www.nineforbrands.com.au/wp-json/

```

---

### 📚 Is Command Ki Detail:

Hum WordPress ke official **REST API (`/wp-json/`)** ka status check kar rahe hain. Agar yahan `200 OK` aata hai, toh hamare paas plugins ke endpoints (jaise Gravity Forms API ya Yoast API routes) ko bariki se examine karne ka aik naya rasta khul jayega.

---

