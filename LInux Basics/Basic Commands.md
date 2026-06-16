### 📁 Files Aur Folders Ke Sath Khelna

* **`ls`**: Yeh samajh lo terminal ki ankhein hain. Jab bhi tum kisi folder mein jatay ho aur dekhna chahte ho ke yahan kaun kaun si files pari hain, to tum `ls` likhtay ho. Agar chupi hui (hidden) files dekhni hon, to sath `-a` laga detay hain.
* **`cd`**: Yeh aik folder se doosre folder mein chalay jaane ka rasta hai. Jaise `cd Documents` likha to tum Documents ke andar ghuss gaye. Wapas peeche aana ho to `cd ..` likh do.
* **`mkdir`**: Iska matlab hai "Make Directory", yaani aik naya khali folder banana.
* **`touch`**: Agar folder nahi banana balkay aik bilkul khali text file banani hai (jaise notepad ki file hoti hai), to `touch file.txt` likh do, file tayar!
* **`mv`**: Is ke do kaam hain. Ya to tum is se kisi file ko utha kar doosre folder mein shift (move) kar do, ya phir agar tum ne kisi file ka naam badalna (rename karna) ho, to bhi yahi use hoti hai.

---

### 📄 File Ke Andar Ka Data Aur Permissions

* **`cat`**: Yeh kisi file ko open kiye baghair, terminal ki screen par hi us ka sara text parhne ke liye use hoti है. Bas `cat file.txt` likho aur andar ka maal samne.
* **`>` (Single bracket)**: Yeh bohot khatarnak aur tez cheez hai. Agar tum likho `echo "hello" > file.txt`, to yeh file mein pehle se jo kuch bhi likha hoga usay dho kar (delete kar ke) naya text likh dega. Aur agar tum akele `> file.txt` likhoge, to file ka sara data urr jayega aur file bilkul khali ho jayegi.
* **`>>` (Double bracket)**: Yeh thoda tameezdar hai. Yeh purane data ko delete nahi karta, balkay us ke neechay naya text add (append) kar deta hai.
* **`chmod 400`**: Cyber security mein yeh bohot kaam aayegi. Is ka matlab hota hai ke tum apni file par sakht qofal (lock) laga rahe ho taake tumhare ilawa koi aur usay na parh sakay aur na hi edit kar sakay.

---

### 💻 System Ki Detail Aur Filtering

* **`uname -a`**: Yeh Linux ka identity card check karne ke liye hai. Is se system ka poora version aur kernel detail mil jati hai, jo hackers ke liye exploits dhoondne mein bohot zaroori hoti hai.
* **`grep`**: Yeh bohot kamal ka filter hai. Agar aik file mein 10,000 lines hain aur tum ne sirf word "admin" dhoondna hai, to tum `grep "admin" file.txt` likhoge. Yeh baqi sab chupa dega aur sirf admin wali line tumhare samne le aayega.

---

### 📝 Nano Editor Ke Short-cuts (Jab Tum File Ke Andar Ho)

Jab tum terminal par `nano file.txt` likh kar file ke andar chalay jatay ho, to mouse kaam nahi karta. Wahan sara khel in buttons ka hai:

* **`Alt + A`**: Is se selection mode on ho jata hai. Isay daba kar jab tum arrow keys chalate ho to text select (highlight) hona shuru ho jata hai.
* **`Ctrl + End`**: Agar tum ne `Alt + A` dabaya hua hai aur sath hi `Ctrl + End` daba do, to file ka **sara ka sara data ek hi jhatkay mein select** ho jata hai.
* **`Ctrl + O`**: Jo kuch tum ne naya likha ya edit kiya hai, usay **Save** karne ke liye pehle yeh daba kar Enter marna parta hai.
* **`Ctrl + X`**: File se **bahar nikalne** ke liye aur wapas normal terminal screen par aane ke liye yeh dabate hain.

---

### ⚡ Terminal Ko Control Karne Wale Buttons

* **`Ctrl + C`**: Yeh Linux ka emergency brake hai! Agar koi command phans gayi hai, ya tum ne galti se kuch galat chala diya hai aur screen ruk nahi rahi, to `Ctrl + C` dabao, woh chalte hue kaam ko jhat se cancel kar ke tumhein naya saaf prompt de dega.
* **`Ctrl + Shift + C`**: Linux terminal par normal `Ctrl + C` se text copy nahi hota kyun ke woh interrupt ke liye hota hai. Is liye terminal se koi bhi IP address ya code copy karne ke liye hamesha `Ctrl + Shift + C` dabana parta hai. Aur agar terminal par kuch paste karna ho, to **`Ctrl + Shift + V`** use hota hai.
