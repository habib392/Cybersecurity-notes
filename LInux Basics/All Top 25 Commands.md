## 📘 Linux Core Commands Notes (Part 1: 1-10)
### 1. pwd (Print Working Directory)
 * **Detail Usage:** Yeh command aap ko batati hai ke aap is waqt Linux ke kis folder ke andar khare hain. Yeh poora absolute path (/home/user/...) show karti hai.
 * **Web Security / Pentesting Use:** Jab aap kisi website par **File Upload Vulnerability** dhoond kar apni reverse shell script (web shell) upload karte hain, to server ke andar daakhil hote ہی aap pwd chalate hain taake aap ko pata chale ke aap website ke kis directory/folder mein khare hain aur wahan se aage kahan jana hai.
 * **How to run:**
   
   ```
   pwd
   ```
 * **Common Mistakes & Fixes:** Is mein aam tor par koi mistake nahi hoti kyun ke is ka koi flag nahi hota, bas spelling small letters mein hone chahiye.

---

### 2. cd (Change Directory)
 * **Detail Usage:** Aik folder se doosre folder mein jaane ke liye use hoti hai.
 * **Web Security / Pentesting Use:** Server par control milne ke baad aap ko sensitive folders (jaise /var/www/html jahan website ka code hota hai, ya /etc jahan configuration files hoti hain) mein jaane ke liye baar baar cd ka istamal karna parta hai.
 * **How to run:**
   * Specific folder mein jaane ke liye: cd Documents
   * Ek step peeche aane ke liye: cd ..
   * Seedha Home directory mein jaane ke liye: cd ~
 * **Common Mistakes & Fixes:** * **Mistake (Case Sensitivity):** cd documents (choti d ke sath) error dega no such file or directory.
   * **Fix:** Linux case-sensitive hai, is liye bilkul sahi capital ya small letters likhein (cd Documents).

---

### 3. ls (List)
 * **Detail Usage:** Yeh aap ke current folder ke andar maujood saari files aur folders ki list aap ko dikhati hai.
 * **Web Security / Pentesting Use:** Jab aap target machine par enter hote hain, to sab se pehle ls kar ke dekhte hain ke wahan kaun si files pari hain (jaise passwords.txt, config.php, ya koi backup file).
 * **Important Flags:**
   * -l (Long listing): Files ka size, owner, aur permissions (rwx) detail mein dikhata hai.
   * -a (All): Hidden files (jo . se shuru hoti hain) unhein bhi show karta hai. Pentesting mein hackers hidden configuration files dhoondne ke liye ls -la chalate hain.
 * **How to run:**
   ```bash
   ls -la
   
   ```
---

### 4. echo
 * **Detail Usage:** Yeh terminal par kisi bhi text ko print karne ya us text ko kisi file ke andar likhne ke liye istamal hota hai.
 * **Web Security / Pentesting Use:** Jab aap ko terminal se direct kisi file mein koi payload, exploit script, ya ip address daalna ho bina nano editor khole, to echo use hota hai.
 * **Redirection Operators (> and >>):**
   * > (Overwrite): Purana data mita kar naya likhta hai. echo "hacked" > test.txt
   * >> (Append): Purane data ke neeche nayi line jorta hai. echo "new line" >> test.txt
 * **Common Mistakes & Fixes:**
   * **Mistake (Quote Error):** echo "text... (agar aakhri quote band na ho) to terminal dquote> par phas jata hai.
   * **Fix:** Ctrl + C daba kar cancel karein aur hamesha double quotes band karein. Triple >>> jaisa koi operator nahi hota, lagane par parse error aayega.

---

### 5. cat (Concatenate)
 * **Detail Usage:** Kisi bhi file ke andar kya likha hai (content), use terminal par direct read karne ke liye use hoti hai.
 * **Web Security / Pentesting Use:** Website ke server par maujood sensitive files (jaise /etc/passwd users ki list dekhne ke liye, ya wp-config.php database ka password dekhne ke liye) read karne ke liye hamesha cat chalayi jati hai.
 * **How to run:**
   ```bash
   cat config.php
   
   ```
 * **Common Mistakes & Fixes:** Agar file bohot badi ho (jaise 10,000 lines ki wordlist), to cat chalane se terminal bhar jata hai. Badi files ke liye cat ki jagah less ya head/tail use karna chahiye.

---

### 6. cp (Copy)
 * **Detail Usage:** Kisi file ya folder ki copy bana kar doosri jagah ya doosre naam se save karne ke liye.
 * **Web Security / Pentesting Use:** Kisi sensitive script ya configuration file mein badlao karne se pehle hacker us ka backup banata hai taake agar system crash ho to backup kaam aaye.
 * **How to run:**
   ```bash
   cp original.txt backup_original.txt
   
   ```
 * **Common Mistakes & Fixes:** Agar poora folder copy karna ho to simple cp error deta hai. Folder ke liye hamesha -r (Recursive) flag lagayein: cp -r folder1 backup_folder1.

---

### 7. rm (Remove)
 * **Detail Usage:** Files ya folders ko hamesha ke liye delete karne ke liye. Linux mein Windows ki tarah Recycle Bin nahi hota, yahan se gayi file wapas nahi aati.
 * **Web Security / Pentesting Use:** Jab aap ka penetration test mukammal ho jaye (Cleanup phase), to aap ko apne saare traces, uploaded web shells, aur tools target server se delete karne hote hain taake kal ko koi real hacker un ka faida na utha sake.
 * **Important Flags:**
   * -f (Force): Bina pooche delete kar deta hai.
   * -r (Recursive): Poore folder ko delete karne ke liye.
 * **How to run:**
   ```bash
   rm -rf web_shell.php
   
   ```

---

### 8. sleep
 * **Detail Usage:** Terminal ke execution ko kuch seconds ke liye rokh (pause) deta hai.
 * **Web Security / Pentesting Use:** 1. **Automation Scripts:** Do requests ke darmiyan gap dene ke liye taake web firewall (WAF) aap ka IP block na kare.
   2. **Time-Based Blind SQL Injection:** Database ko check karne ke liye ke woh vulnerable hai ya nahi, hacker server ko command bhejta hai ke agar mera andaza sahi hai to sleep 10 (10 seconds so jao). Agar response delay ho jaye, to bug confirm ho jata hai.
 * **How to run (Background process ke sath):**
   ```bash
   sleep 300 &
   
   ```
   *(Ampersand & lagane se terminal free ho jata hai aur sleep background mein chalta rehta hai, aur aap ko aik PID number milta hai).*

---

### 9. kill
 * **Detail Usage:** Background mein chalne wale kisi bhi active process ko terminate (band) karne ke liye istamal hota hai.
 * **Web Security / Pentesting Use:** Agar aap ne koi scanning tool (jaise Nmap ya Buster) background mein lagaya aur woh phas gaya ya aap usay rokhna chahte hain, to kill command use hoti hai.
 * **Important Flags:** -9 (Force Kill) - Yeh process ko har haal mein foran band kar deta hai.
 * **How to run:**
   ```bash
   kill -9 <PID_NUMBER>
   
   ```
   *(PID number aap ko process shuru karte waqt ya ps command se milta hai).*

---

### 10. history
 * **Detail Usage:** Aap ne terminal par shuru se ab tak jitni bhi commands chalayi hain, yeh un ki poori list number ke sath dikha deta hai.
 * **Web Security / Pentesting Use:** Pentesting ke aakhri mein report banate waqt hacker check karta hai ke us ne kaun kaun si commands chalayi thin taake woh client ko bata sake.
 * **Pro Tip (Chaining with tail):** Poori history dekhne ke bajaye sirf aakhri 10 commands dekhne ke liye tail ke sath pipe karte hain:
   ```bash
   history | tail -n 10
   
   ```
---

### 11. grep (Global Regular Expression Print)
 * **Detail Usage:** Yeh Linux ka built-in search engine hai. Is ka kaam kisi file ke andar se ya kisi doosri command ke output mein se aap ka bataya hua specific word ya pattern dhoond kar nikalna hai.
 * **Web Security / Pentesting Use:** Jab aap kisi website ki JavaScript files scan karte hain aur un mein se sensitive information jaise "API_KEY", "token", ya "admin_url" dhoondna chahte hain, to hazaron lines ka code manually parhne ke bajaye grep chalaya jata hai.
 * **Important Flags:**
   * -i: Ignore Case (Yani bade aur chote letters ka farq khatam kar deta hai. grep -i "admin" karne se Admin aur ADMIN sab samne aa jayenge).
   * -r: Recursive (Poore folder aur us ke andar ke saare sub-folders mein dhoondne ke liye).
   * -v: Invert Match (Jo word aap ne likha, us ke alawa baqi saara data dikhayega).
 * **How to run:**
   ```bash
   grep -i "api_key" configuration.js
   
   ```
---

### 12. sort
 * **Detail Usage:** Yeh kisi bhi file ke data ko ya doosri command ke output ko alphabetically (A to Z) ya numerically ek tarteeb (order) mein le aata hai.
 * **Web Security / Pentesting Use:** Jab aap Bug Bounty ke doran kisi website ke hazaron subdomains nikalte hain (jaise Subfinder tool se), to un subdomains ki list ko ek proper order mein laane ke liye sort use hota hai taake analyze karna aasan ho.
 * **How to run:**
   ```bash
   sort subdomains.txt
   
   ```

---

### 13. uniq (Unique)
 * **Detail Usage:** Yeh data mein se duplicate lines (jo baar baar aa rahi hon) unhein mita deta hai aur sirf single unique copy rakhta hai.
 * **CRITICAL RULE (Jo aap se galti hui thi):** uniq command poori file mein door door pari duplicate lines ko nahi pehchanti. Yeh sirf tab kaam karti hai jab duplicate lines aik doosre ke bilkul upar-neeche (adjacent) hon. Is liye isay hamesha sort ke sath pipe (|) kar ke chalaya jata hai.
 * **Important Flags:**
   * -i: Case-insensitive (Yani Abd.com aur abd.com ka farq mita kar unhein duplicate samjhega aur ek ko delete kar dega).
   * -c: Count (Yeh batata hai ke kaun si line file mein kitni baar aayi thi).
 * **How to run:**
   ```bash
   sort sorttest.txt | uniq -i
   
   ```

---

### 14. awk
 * **Detail Usage:** Yeh Linux ka ek bohot hi powerful data manipulation tool hai jo text ko columns (hissoun) mein torta hai. Default tor par yeh spaces ya tabs ko dekh kar columns banata hai.
 * **Web Security / Pentesting Use:** Maan lein aap ne Nmap chalaya aur line aayi: 80/tcp open http. Aap ko is poori line mein se sirf port number (80/tcp) chahiye, baqi text nahi chahiye script ke liye. To aap awk se pehla column print karwa lete hain.
 * **How to run:**
   ```bash
   echo "80/tcp open http" | awk '{print $1}'
   
   ```
   *(Yahan $1 ka matlab pehla column hai. Agar $3 likhenge to http print hoga).*

---

### 15. chmod (Change Mode)
 * **Detail Usage:** Yeh kisi bhi file ya folder ki permissions (Read r, Write w, Execute x) ko badalne ke liye hota hai. Linux mein har permission ka ek number hota hai: Read=4, Write=2, Execute=1. (4+2+1 = 7, yaani Full Control).
 * **Web Security / Pentesting Use:** Jab aap GitHub se koi exploit script (jaise exploit.sh ya reverse_shell.py) download karte hain, to Linux use execute karne nahi deta aur "Permission Denied" ka error deta hai. Aap ko use chalane ke liye execution access dena parta hai.
 * **How to run:**
   ```bash
   chmod +x exploit.sh
   
   ```
   *(Ya full access ke liye jo aap ne chalaya: chmod 777 latest.tar.gz)*

---

### 16. chown (Change Owner)
 * **Detail Usage:** Yeh file ya folder ka asal maalik (User) ya us ka Group badalne ke liye istamal hota hai. Is command ko chalane ke liye hamesha sudo (root power) chahiye hoti hai.
 * **Web Security / Pentesting Use:** Kuch sensitive security tools ya system logs sirf root user hi read/write kar sakta hai. Agar aap ne normal user mein koi reverse shell script banayi hai aur aap chahte hain ke system use admin level par treat kare, to aap ownership change karte hain.
 * **How to run:**
   ```bash
   sudo chown root latest.tar.gz
   
   ```
   *(Is se file ka owner habib se badal kar root ho jata hai).*

---

### 17. curl (Client URL)
 * **Detail Usage:** Yeh terminal ka apna "Web Browser" hai. Yeh bina koi GUI browser (Chrome/Firefox) khole, direct terminal se kisi bhi website ya web server ko HTTP requests bhejta hai aur us ka response fetch karta hai.
 * **Web Security / Pentesting Use:** Website ke background status codes (200 OK, 403 Forbidden, 302 Redirect) check karne ke liye, custom HTTP Headers dekhne ke liye, ya direct exploit payloads website par test karne ke liye.
 * **Important Flags:**
   * -I: Fetch headers only (Website ka poora HTML code nahi dikhayega, sirf oper ka security data aur server name dikhayega).
   * -X: Request method badalna (Jaise POST, PUT, DELETE requests bhejna API testing mein).
 * **How to run:**
   ```bash
   curl -I https://google.com
   
   ```

---

### 18. wget
 * **Detail Usage:** Yeh terminal ka "Download Manager" hai jo internet se direct links ke zariye files, tools, ya archives download karta hai.
 * **Common Mistakes & Fixes (Jo aap se galti hui thi):** Jab link ke andar & ya ? jaise special characters hon, to Zsh terminal parse error de deta hai kyun ke & ka matlab background process hota hai Linux mein.
   * **Fix:** Hamesha poore link ko **Double Quotes ""** ke andar band kar ke chalayein.
 * **Important Flags:**
   * -O (Capital O): File ka naam apni marzi se chota rakhne ke liye download karte waqt.
 * **How to run:**
   ```bash
   wget -O picture.jpg "https://cdn.sanity.io/images/...&w=1351"
   
   ```

---

### 19. ping
 * **Detail Usage:** Yeh check karta hai ke target website ya server internet par active (online) hai ya nahi. Yeh ICMP packets bhejta hai aur wapas aane ka waqt check karta hai.
 * **Web Security / Pentesting Use:** Kisi bhi website ka real IP address maloom karne ke liye ya yeh check karne ke liye ke target machine ke sath aap ka networking connection block to nahi ho raha.
 * **Important Flags:**
   * -c: Count (Linux default mein lagatar ping karta rehta hai, use rokhne ke liye limit lagate hain).
 * **How to run:**
   ```bash
   ping -c 4 google.com
   
   ```
---