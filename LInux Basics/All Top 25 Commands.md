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
### 10. history
 * **Detail Usage:** Aap ne terminal par shuru se ab tak jitni bhi commands chalayi hain, yeh un ki poori list number ke sath dikha deta hai.
 * **Web Security / Pentesting Use:** Pentesting ke aakhri mein report banate waqt hacker check karta hai ke us ne kaun kaun si commands chalayi thin taake woh client ko bata sake.
 * **Pro Tip (Chaining with tail):** Poori history dekhne ke bajaye sirf aakhri 10 commands dekhne ke liye tail ke sath pipe karte hain:
   ```bash
   history | tail -n 10
   
   ```
---

