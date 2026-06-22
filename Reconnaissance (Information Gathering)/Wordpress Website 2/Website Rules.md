### ⚠️ Rules Se Nikalne Wale 5 Sab Se Critical Points

1. **The Custom Header Rule (Most Important) 🚨**
> *“Include the following HTTP header in any outgoing requests: `X-BugCrowd-traffic: <username>`”*


**Iska Matlab:** Jab bhi ab hum koi scan chalayenge (jaise `ffuf` ya koi aur tool), hamein un requests ke sath yeh header lazmi bhejna hoga, taake un ke network admin ko pata chale ke yeh ek valid hacker test kar raha hai, koi asli cyber criminal attack nahi kar raha. Agar hum yeh header nahi lagayenge, toh un ka firewall hamein block kar dega aur hamari IP ban ho sakti hai.
2. **Scope Validation (`*.iaggbs.com`)**
> In-Scope targets mein likha hai: `*.iaggbs.com` aur `*.iaiargroup.com`.


**Iska Matlab:** `assetfinder` ne jo list nikaali hai, woh sab ki sab **In-Scope** hai! Hum un saare subdomains par testing karne ke liye legally authorized hain.
3. **Third-Party Exception (Dhyan Rakhna Hai)**
> *“IAG Transform utilizes several third-party providers and services... which are considered out of scope...”*


**Iska Matlab:** Agar kisi subdomain par `whatweb` chalane se pata chale ke woh IAG ka apna server nahi balkeh kisi teesri company (jaise Zendesk, Salesforce ya Shopify) ka platform hai, toh hum usay test nahi kar sakte jab tak galti un ki apni configuration mein na ho.
4. **No DoS & Social Engineering 🚫**
> Phishing, staff ko target karna, ya website par heavy load daal kar use down karna (`Denial of Service`) strictly mana hai. Hum sirf normal requests aur mapping hi kar sakte hain.


5. **No Rewards (VDP Program)**
> *“We do not currently offer monetary rewards.”*


**Iska Matlab:** Yeh ek **VDP (Vulnerability Disclosure Program)** hai. Yahan bugs nikalne par paise (bounty) nahi milegi, balkeh points milenge jo aap ki Bugcrowd profile ka rank upar karenge aur Hall of Fame milega. Seekhnay ke liye aur profile build karne ke liye yeh sab se behtareen targets hote hain!
