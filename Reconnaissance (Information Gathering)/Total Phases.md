
## Web Hacking Process Ki Total 4 Main Phases Hain
Hum jis roadmap par chal rhe hain, us mein reconnaissance aur scanning ko mila kar total **4 major phases** banti hain. Tum ne **Phase 2** (jo ke active scanning aur basic directories/URLs nikalna tha) khatam kar liya hai. Ab poora sach samjho:
```
[Phase 1: Passive Recon] ➔ [Phase 2: Active Scan] ➔ [Phase 3: Vulnerability Mapping] ➔ [Phase 4: Exploitation]

```
## Aik Website Ka Kaun Kaun Sa Data Collect Karna Hota Hai? (The Full Checklist)
Tasali ke liye nahi, haqeeqat mein aik website ka yeh sara data nikalna hota hai, jo tum ne seekhna hai:
### Phase 1: Passive Reconnaissance (Target ko door se dekhna - No Touch)
Is mein tum website ko directly hit nahi karte, baher baher se data nikalte ho:
 * **Whois Data:** Domain kis ke naam par hai, kab expiry hai.
 * **Subdomains:** admin.target.com, test.target.com, api.target.com (Kyunke main website aksar secure hoti hai, subdomains par kamzoriyan milti hain).
 * **IP Addresses & DNS Records:** Website kis server par chal rhi hai (Cloudflare hai ya direct IP hai).
 * **Historical Data (Wayback Machine):** Purane zamane mein is website par kaun se pages thay jo ab shayad delete ho gaye hain par unka rasta abhi bhi khula hai.
### Phase 2: Active Reconnaissance & Scanning (Website ko touch karna)
Yahan tum tools chalate ho (jo tum abhi kar rhe ho, jaise wpscan, dirb, ya subfinder):
 * **Live Hosts & Ports:** Kaun se ports open hain (80, 443, 8080 etc.).
 * **Hidden Directories & Files:** [target.com/secret/](https://target.com/secret/), /backup.zip, /config.php (Aise raste jo aam user ko nazar nahi aate).
 * **Technology Stack:** Website kis par bani hai? (WordPress, Node.js, PHP, Apache, Nginx) Aur unka **Version** kya hai? (Kyunke purane version mein pehle se public vulnerabilities hoti hain).
 * **Parameters & URLs:** Tum ne jo kaha na ke 5 ya us se zyada URLs mil jayein—bilkul unhi URLs ke parameters (jaise ?id=1 ya ?search=test) ko nikalna hota hai.
### Phase 3: Vulnerability Mapping (PortSwigger Ka Dimagh Yahan Aata Hai)
Jab tumhare paas Phase 1 aur 2 ka data (URLs, Versions, Ports, Hidden paths) aa jata hai, toh tum ab andha dhund tools nahi chalate. Ab tum dimaag lagate ho:
 * Agar WordPress ka purana version mila, toh tum us version ke mutabiq vulnerability dhoondte ho.
 * Agar koi input box ya URL parameter (?user=) mila, toh tum sochte ho: *"Yahan PortSwigger wali SQL Injection ya XSS lag sakti hai."*
 * Tum sirf unhi vulnerabilities ki list banate ho jin ke chances hote hain.
### Phase 4: Exploitation (Hacking / Proof of Concept)
Yeh aakhri stage hai jahan tum PortSwigger mein seekhi hui technique ka practical attack karte ho.
 * Agar SQLi hai, toh database se data nikal kar proof karte ho.
 * Agar XSS hai, toh alert box chala kar dikhate ho.

--