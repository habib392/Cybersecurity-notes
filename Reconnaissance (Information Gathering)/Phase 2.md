## Phase 2

```bash
wpscan --url https://www.nineforbrands.com.au --enumerate p,t --stealthy

```

---

### 📚 Is Command Ki Poori Detail (Notes ke liye):

#### 1. Is mein kaun sa Tool use ho raha hai?

Is mein **`wpscan`** (WordPress Security Scanner) use ho raha hai. Yeh Kali Linux ka default aur sab se powerfull tool hai jo sirf aur sirf WordPress websites par vulnerabilities, out-dated plugins, themes, aur users dhoondne ke liye design kiya gaya hai.

#### 2. Is command ke Flags ka kya matlab hai?

* **`--url`**: Target website ka direct link.
* **`--enumerate p,t`**: **Enumerate** ka matlab hota hai ek ek karke dhoondna aur list banana. **`p`** ka matlab hai *Plugins* aur **`t`** ka matlab hai *Themes*. Hum tool ko keh rahe hain ke is website par jitne bhi plugins aur themes install hain, unka pata lagao.
* **`--stealthy`**: Chunke is website par Cloudflare aur AWS ki security shields lagi hui hain, yeh flag hamari scanning ki speed aur pattern ko thora badal deta hai taake firewall hamare tool ko block na kare aur scan khamoshi se nikal jaye.

#### 3. Agar is command se data mil gaya, toh hum us se kya faida utha sakte hain? (Hacker Logic)

* **Find Third-Party Vulnerabilities:** WordPress ka core code bohot strong hota hai, lekin jo extra plugins (jaise sliders, forms, ecommerce tools) log install karte hain, un mein aksar security gaps hote hain. Agar WPScan hamein kisi plugin ka exact name aur version nikal kar de deta hai, toh hamara 80% kaam aasan ho jata hai.
* **Exploit Verification:** Agar koi out-dated plugin milta hai, toh hum internet par (Exploit-DB ya CVE Databases) par ja kar dekhte hain ke kya us version par koi direct exploit ya payload available hai, jis se hum Cross-Site Scripting (XSS) ya SQL Injection test kar sakein.
