**Phase 2: Active Scanning & Enumeration** ka aghaaz kar rahe hain.

Phase 1 mein hum ne sirf door se jaasusi ki thi, lekin Phase 2 mein hum target server ko direct hit karenge aur us ke andar chhupe huve kamray (directories aur files) dhoondenge.

Chunke yeh website **WordPress** par chal rahi hai, toh expert hackers Phase 2 ko do tarike se chalate hain:

1. **Directory Brute-Forcing (`ffuf` ke sath):** Taake aam hidden pages aur files ka pata chale.
2. **CMS Specific Scanning (`wpscan` ke sath):** Jo sirf WordPress ke bugs dhoondta hai (yeh hum is ke baad karenge).

---

### 🚀 Phase 2 Ka Pehla Kadam: `ffuf` Configuration

Aap ka pichla pattern yaad hai? Hum ne `ffuf` chalayi thi, lekin is baar hamare paas do nayi cheezein hain:

1. Target badal gaya hai (`https://www.iaggbs.com/`).
2. Bugcrowd ka **Custom Header** (`X-BugCrowd-traffic`) lagana lazmi hai, warna unka firewall hamare scan ko block kar dega.

`ffuf` mein header lagane ke liye **`-H`** ka flag use hota hai.

Apne terminal mein yeh command run karein:

```bash
ffuf -u https://www.iaggbs.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -H "X-BugCrowd-traffic: habib_kali" -mc 200,301,302

```

---

### 🔍 Is Command Ko Samajh Lein:

* **`-u`**: Hamara target URL, jahan `/FUZZ` ki jagah `common.txt` ka har ek word fit ho kar check hoga.
* **`-w`**: Kali Linux ki default wordlist (`common.txt`) ka rasta.
* **`-H`**: Hamara Bugcrowd traffic header taake hum rules ke mutabiq safe rahein.
* **`-mc 200,301,302`**: Hamein sirf wahi results dikhao jo successful hon (`200 OK`) ya redirect ho rahe hon (`301`, `302`), taake faltu `404 Not Found` wale errors se terminal na bhare.

---

## Output

└─$ ffuf -u https://www.iaggbs.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -H "X-BugCrowd-traffic: habib_kali" -mc 200,301,302

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : https://www.iaggbs.com/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirb/common.txt
 :: Header           : X-Bugcrowd-Traffic: habib_kali
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,301,302
________________________________________________

:: Progress: [1/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:01] :: Error:: Progress: [40/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:02] :: Error:: Progress: [41/4614] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:02] :: Error:: Progress: [72/4614] :: Job [1/1] :: 244 req/sec :: Duration: [0:00:02] :: Err                        [Status: 200, Size: 45460, Words: 6131, Lines: 564, Duration: 303ms]
:: Progress: [80/4614] :: Job [1/1] :: 245 req/sec :: Duration: [0:00:02] :: Err:: Progress: [90/4614] :: Job [1/1] :: 197 req/sec :: Duration: [0:00:02] :: Err:: Progress: [96/4614] :: Job [1/1] :: 153 req/sec :: Duration: [0:00:02] :: Err:: Progress: [115/4614] :: Job [1/1] :: 154 req/sec :: Duration: [0:00:02] :: Er:: Progress: [127/4614] :: Job [1/1] :: 138 req/sec :: Duration: [0:00:02] :: Er:: Progress: [140/4614] :: Job [1/1] :: 136 req/sec :: Duration: [0:00:02] :: Er:: Progress: [157/4614] :: Job [1/1] :: 131 req/sec :: Duration: [0:00:03] :: Er:: Progress: [174/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:03] :: Er:: Progress: [185/4614] :: Job [1/1] :: 127 req/sec :: Duration: [0:00:03] :: Er:: Progress: [207/4614] :: Job [1/1] :: 132 req/sec :: Duration: [0:00:03] :: Er:: Progress: [221/4614] :: Job [1/1] :: 130 req/sec :: Duration: [0:00:03] :: Er:: Progress: [235/4614] :: Job [1/1] :: 128 req/sec :: Duration: [0:00:03] :: Er:: Progress: [247/4614] :: Job [1/1] :: 126 req/sec :: Duration: [0:00:03] :: Er:: Progress: [260/4614] :: Job [1/1] :: 123 req/sec :: Duration: [0:00:03] :: Er:: Progress: [280/4614] :: Job [1/1] :: 117 req/sec :: Duration: [0:00:04] :: Er:: Progress: [295/4614] :: Job [1/1] :: 120 req/sec :: Duration: [0:00:04] :: Er:: Progress: [307/4614] :: Job [1/1] :: 119 req/sec :: Duration: [0:00:04] :: Er:: Progress: [325/4614] :: Job [1/1] :: 119 req/sec :: Duration: [0:00:04] :: Er:: Progress: [345/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:04] :: Er:: Progress: [359/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:04] :: Er:: Progress: [377/4614] :: Job [1/1] :: 127 req/sec :: Duration: [0:00:04] :: Er:: Progress: [393/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:04] :: Er:: Progress: [411/4614] :: Job [1/1] :: 126 req/sec :: Duration: [0:00:05] :: Er:: Progress: [421/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:05] :: Er:: Progress: [436/4614] :: Job [1/1] :: 127 req/sec :: Duration: [0:00:05] :: Er:: Progress: [455/4614] :: Job [1/1] :: 127 req/sec :: Duration: [0:00:05] :: Er:: Progress: [471/4614] :: Job [1/1] :: 129 req/sec :: Duration: [0:00:05] :: Er:: Progress: [486/4614] :: Job [1/1] :: 128 req/sec :: Duration: [0:00:05] :: Er:: Progress: [506/4614] :: Job [1/1] :: 129 req/sec :: Duration: [0:00:05] :: Er:: Progress: [523/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:05] :: Er:: Progress: [539/4614] :: Job [1/1] :: 131 req/sec :: Duration: [0:00:06] :: Er:: Progress: [554/4614] :: Job [1/1] :: 130 req/sec :: Duration: [0:00:06] :: Er:: Progress: [575/4614] :: Job [1/1] :: 131 req/sec :: Duration: [0:00:06] :: Er:: Progress: [595/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:06] :: Er:: Progress: [609/4614] :: Job [1/1] :: 132 req/sec :: Duration: [0:00:06] :: Er:: Progress: [621/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:06] :: Er:: Progress: [637/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:06] :: Er:: Progress: [654/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:06] :: Er:: Progress: [669/4614] :: Job [1/1] :: 130 req/sec :: Duration: [0:00:07] :: Er:: Progress: [685/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:07] :: Er:: Progress: [704/4614] :: Job [1/1] :: 132 req/sec :: Duration: [0:00:07] :: Er:: Progress: [719/4614] :: Job [1/1] :: 130 req/sec :: Duration: [0:00:07] :: Er:: Progress: [733/4614] :: Job [1/1] :: 131 req/sec :: Duration: [0:00:07] :: Er:: Progress: [749/4614] :: Job [1/1] :: 128 req/sec :: Duration: [0:00:07] :: Er:: Progress: [761/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:07] :: Er:: Progress: [773/4614] :: Job [1/1] :: 122 req/sec :: Duration: [0:00:07] :: Er:: Progress: [795/4614] :: Job [1/1] :: 123 req/sec :: Duration: [0:00:08] :: Er:: Progress: [802/4614] :: Job [1/1] :: 121 req/sec :: Duration: [0:00:08] :: Er:: Progress: [820/4614] :: Job [1/1] :: 122 req/sec :: Duration: [0:00:08] :: Er:: Progress: [837/4614] :: Job [1/1] :: 123 req/sec :: Duration: [0:00:08] :: Er:: Progress: [845/4614] :: Job [1/1] :: 117 req/sec :: Duration: [0:00:08] :: Er:: Progress: [861/4614] :: Job [1/1] :: 116 req/sec :: Duration: [0:00:08] :: Er:: Progress: [879/4614] :: Job [1/1] :: 119 req/sec :: Duration: [0:00:08] :: Er:: Progress: [890/4614] :: Job [1/1] :: 116 req/sec :: Duration: [0:00:08] :: Er:: Progress: [903/4614] :: Job [1/1] :: 114 req/sec :: Duration: [0:00:09] :: Er:: Progress: [919/4614] :: Job [1/1] :: 116 req/sec :: Duration: [0:00:09] :: Er:: Progress: [932/4614] :: Job [1/1] :: 113 req/sec :: Duration: [0:00:09] :: Er:: Progress: [946/4614] :: Job [1/1] :: 111 req/sec :: Duration: [0:00:09] :: Er:: Progress: [962/4614] :: Job [1/1] :: 117 req/sec :: Duration: [0:00:09] :: Er:: Progress: [977/4614] :: Job [1/1] :: 115 req/sec :: Duration: [0:00:09] :: Er:: Progress: [987/4614] :: Job [1/1] :: 114 req/sec :: Duration: [0:00:09] :: Ercompanies               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 260ms]
:: Progress: [994/4614] :: Job [1/1] :: 110 req/sec :: Duration: [0:00:09] :: Ercompare                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 259ms]
:: Progress: [995/4614] :: Job [1/1] :: 111 req/sec :: Duration: [0:00:09] :: Ercomparison_list         [Status: 200, Size: 11836, Words: 1499, Lines: 151, Duration: 255ms]
:: Progress: [997/4614] :: Job [1/1] :: 111 req/sec :: Duration: [0:00:09] :: Ercompact                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 264ms]
:: Progress: [999/4614] :: Job [1/1] :: 111 req/sec :: Duration: [0:00:09] :: Ercompiled                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 222ms]
:: Progress: [999/4614] :: Job [1/1] :: 111 req/sec :: Duration: [0:00:09] :: Ercompare_product         [Status: 200, Size: 11836, Words: 1499, Lines: 151, Duration: 265ms]
:: Progress: [1001/4614] :: Job [1/1] :: 118 req/sec :: Duration: [0:00:09] :: Ecompany                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 267ms]
:: Progress: [1002/4614] :: Job [1/1] :: 118 req/sec :: Duration: [0:00:09] :: Ecompliance              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 197ms]
:: Progress: [1003/4614] :: Job [1/1] :: 118 req/sec :: Duration: [0:00:09] :: Ecomplaints              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 208ms]
:: Progress: [1004/4614] :: Job [1/1] :: 118 req/sec :: Duration: [0:00:09] :: Ecompat                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 266ms]
:: Progress: [1009/4614] :: Job [1/1] :: 123 req/sec :: Duration: [0:00:09] :: Ecomponent               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 208ms]
:: Progress: [1013/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:09] :: Ecomparison              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 285ms]
:: Progress: [1014/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:09] :: Ecompose                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 183ms]
:: Progress: [1015/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:09] :: Ecomplaint               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 233ms]
:: Progress: [1015/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:09] :: Ecomponents              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 200ms]
:: Progress: [1017/4614] :: Job [1/1] :: 125 req/sec :: Duration: [0:00:09] :: Ecomposer                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 195ms]
:: Progress: [1019/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:09] :: Ecompress                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 179ms]
:: Progress: [1020/4614] :: Job [1/1] :: 125 req/sec :: Duration: [0:00:09] :: Ecompressed              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 160ms]
:: Progress: [1021/4614] :: Job [1/1] :: 125 req/sec :: Duration: [0:00:09] :: Ecomputer                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 166ms]
:: Progress: [1022/4614] :: Job [1/1] :: 126 req/sec :: Duration: [0:00:09] :: EComputers               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 160ms]
:: Progress: [1023/4614] :: Job [1/1] :: 125 req/sec :: Duration: [0:00:09] :: Ecomputing               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 157ms]
:: Progress: [1024/4614] :: Job [1/1] :: 129 req/sec :: Duration: [0:00:09] :: Ecomunicator             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 159ms]
:: Progress: [1025/4614] :: Job [1/1] :: 128 req/sec :: Duration: [0:00:09] :: Ecomputers               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 171ms]
:: Progress: [1026/4614] :: Job [1/1] :: 128 req/sec :: Duration: [0:00:09] :: E:: Progress: [1027/4614] :: Job [1/1] :: 127 req/sec :: Duration: [0:00:09] :: Econditions              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 160ms]
:: Progress: [1027/4614] :: Job [1/1] :: 127 req/sec :: Duration: [0:00:10] :: Econcrete                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 163ms]
:: Progress: [1027/4614] :: Job [1/1] :: 127 req/sec :: Duration: [0:00:10] :: Econ                     [Status: 200, Size: 11824, Words: 1499, Lines: 151, Duration: 175ms]
:: Progress: [1029/4614] :: Job [1/1] :: 123 req/sec :: Duration: [0:00:10] :: Econf                    [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 174ms]
:: Progress: [1030/4614] :: Job [1/1] :: 122 req/sec :: Duration: [0:00:10] :: Econfig.local            [Status: 200, Size: 11833, Words: 1499, Lines: 151, Duration: 160ms]
:: Progress: [1031/4614] :: Job [1/1] :: 122 req/sec :: Duration: [0:00:10] :: Econfigs                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 161ms]
:: Progress: [1032/4614] :: Job [1/1] :: 122 req/sec :: Duration: [0:00:10] :: Econfiguration           [Status: 200, Size: 11834, Words: 1499, Lines: 151, Duration: 164ms]
:: Progress: [1033/4614] :: Job [1/1] :: 124 req/sec :: Duration: [0:00:10] :: Econfig                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 168ms]
:: Progress: [1034/4614] :: Job [1/1] :: 125 req/sec :: Duration: [0:00:10] :: Econferences             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 179ms]
:: Progress: [1034/4614] :: Job [1/1] :: 123 req/sec :: Duration: [0:00:10] :: Econfirm                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 174ms]
:: Progress: [1034/4614] :: Job [1/1] :: 123 req/sec :: Duration: [0:00:10] :: Econlib                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 183ms]
:: Progress: [1034/4614] :: Job [1/1] :: 125 req/sec :: Duration: [0:00:10] :: Econfigure               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 176ms]
:: Progress: [1034/4614] :: Job [1/1] :: 130 req/sec :: Duration: [0:00:10] :: Econfirmed               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 174ms]
:: Progress: [1034/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econnect                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 168ms]
:: Progress: [1034/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econference              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 185ms]
:: Progress: [1041/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econnections             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 174ms]
:: Progress: [1042/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econn                    [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 172ms]
:: Progress: [1043/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econstant                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 167ms]
:: Progress: [1044/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econtact_us              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 171ms]
:: Progress: [1045/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econtact                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 173ms]
:: Progress: [1046/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econnectors              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 178ms]
:: Progress: [1047/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econnector               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 180ms]
:: Progress: [1048/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econsumer                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 177ms]
:: Progress: [1048/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econt                    [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 176ms]
:: Progress: [1048/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econsole                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 180ms]
:: Progress: [1051/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econstants               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 184ms]
contact_bean            [Status: 200, Size: 11833, Words: 1499, Lines: 151, Duration: 184ms]
Contact                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 181ms]
:: Progress: [1051/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: E:: Progress: [1051/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: E:: Progress: [1051/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: E:: Progress: [1054/4614] :: Job [1/1] :: 133 req/sec :: Duration: [0:00:10] :: Econtacto                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 175ms]
:: Progress: [1055/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:10] :: Econsulting              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 193ms]
:: Progress: [1056/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:10] :: Econtacts                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 180ms]
:: Progress: [1057/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:10] :: Econtactinfo             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 183ms]
:: Progress: [1058/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:10] :: Econtact-form            [Status: 200, Size: 11833, Words: 1499, Lines: 151, Duration: 197ms]
:: Progress: [1059/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:10] :: Econtact-us              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 173ms]
:: Progress: [1059/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:10] :: Econtactus               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 177ms]
:: Progress: [1061/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: EContactUs               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 174ms]
:: Progress: [1062/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: Econtato                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 182ms]
:: Progress: [1063/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: Econtao                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 185ms]
contenido               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 178ms]
:: Progress: [1063/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: E:: Progress: [1063/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: Econtent                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 179ms]
:: Progress: [1066/4614] :: Job [1/1] :: 142 req/sec :: Duration: [0:00:10] :: EContent                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 159ms]
:: Progress: [1067/4614] :: Job [1/1] :: 142 req/sec :: Duration: [0:00:10] :: Econtents                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 159ms]
:: Progress: [1068/4614] :: Job [1/1] :: 138 req/sec :: Duration: [0:00:10] :: E:: Progress: [1069/4614] :: Job [1/1] :: 138 req/sec :: Duration: [0:00:10] :: Econtests                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 185ms]
:: Progress: [1069/4614] :: Job [1/1] :: 138 req/sec :: Duration: [0:00:10] :: Econtracts               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 190ms]
:: Progress: [1070/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:10] :: Econtest                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 197ms]
:: Progress: [1071/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:10] :: Econtract                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 193ms]
:: Progress: [1072/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:10] :: Econtrib                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 194ms]
:: Progress: [1073/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:10] :: Econtrolpanel            [Status: 200, Size: 11833, Words: 1499, Lines: 151, Duration: 184ms]
:: Progress: [1074/4614] :: Job [1/1] :: 135 req/sec :: Duration: [0:00:10] :: Econtrols                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 187ms]
:: Progress: [1075/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:10] :: Econtrollers             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 187ms]
:: Progress: [1076/4614] :: Job [1/1] :: 134 req/sec :: Duration: [0:00:10] :: Econtribute              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 190ms]
:: Progress: [1077/4614] :: Job [1/1] :: 137 req/sec :: Duration: [0:00:10] :: Econtributor             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 198ms]
:: Progress: [1078/4614] :: Job [1/1] :: 137 req/sec :: Duration: [0:00:10] :: Ecookie                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 195ms]
:: Progress: [1079/4614] :: Job [1/1] :: 141 req/sec :: Duration: [0:00:10] :: Ecookie_usage            [Status: 200, Size: 11833, Words: 1499, Lines: 151, Duration: 195ms]
:: Progress: [1080/4614] :: Job [1/1] :: 143 req/sec :: Duration: [0:00:10] :: Econtrol                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 204ms]
:: Progress: [1081/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: Econverge_local          [Status: 200, Size: 11835, Words: 1499, Lines: 151, Duration: 207ms]
:: Progress: [1082/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: Ecoreg                   [Status: 200, Size: 11826, Words: 1499, Lines: 151, Duration: 178ms]
:: Progress: [1083/4614] :: Job [1/1] :: 144 req/sec :: Duration: [0:00:10] :: Econtroller              [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 209ms]
:: Progress: [1084/4614] :: Job [1/1] :: 147 req/sec :: Duration: [0:00:10] :: Ecopies                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 195ms]
:: Progress: [1084/4614] :: Job [1/1] :: 148 req/sec :: Duration: [0:00:10] :: Ecookies                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 199ms]
:: Progress: [1086/4614] :: Job [1/1] :: 149 req/sec :: Duration: [0:00:10] :: Ecopy                    [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 197ms]
:: Progress: [1087/4614] :: Job [1/1] :: 149 req/sec :: Duration: [0:00:10] :: Ecool                    [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 205ms]
:: Progress: [1088/4614] :: Job [1/1] :: 149 req/sec :: Duration: [0:00:10] :: Ecopyright               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 202ms]
:: Progress: [1089/4614] :: Job [1/1] :: 149 req/sec :: Duration: [0:00:10] :: Ecore                    [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 193ms]
:: Progress: [1089/4614] :: Job [1/1] :: 149 req/sec :: Duration: [0:00:10] :: Ecorp                    [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 193ms]
:: Progress: [1090/4614] :: Job [1/1] :: 157 req/sec :: Duration: [0:00:10] :: Ecorpo                   [Status: 200, Size: 11826, Words: 1499, Lines: 151, Duration: 193ms]
:: Progress: [1091/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: Ecount                   [Status: 200, Size: 11826, Words: 1499, Lines: 151, Duration: 174ms]
:: Progress: [1093/4614] :: Job [1/1] :: 157 req/sec :: Duration: [0:00:10] :: Ecorrections             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 191ms]
:: Progress: [1094/4614] :: Job [1/1] :: 157 req/sec :: Duration: [0:00:10] :: Econverse                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 221ms]
:: Progress: [1095/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: Ecorporate               [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 187ms]
:: Progress: [1096/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: Ecorba                   [Status: 200, Size: 11826, Words: 1499, Lines: 151, Duration: 194ms]
copyright-policy        [Status: 200, Size: 11837, Words: 1499, Lines: 151, Duration: 207ms]
corporation             [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 194ms]
country                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 177ms]
counters                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 184ms]
:: Progress: [1096/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: E:: Progress: [1096/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: E:: Progress: [1096/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: E:: Progress: [1096/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: E:: Progress: [1096/4614] :: Job [1/1] :: 156 req/sec :: Duration: [0:00:10] :: Ecounts                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 166ms]
:: Progress: [1102/4614] :: Job [1/1] :: 160 req/sec :: Duration: [0:00:10] :: Ecounter                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 188ms]
:: Progress: [1103/4614] :: Job [1/1] :: 165 req/sec :: Duration: [0:00:10] :: Ecoupons                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 167ms]
:: Progress: [1103/4614] :: Job [1/1] :: 165 req/sec :: Duration: [0:00:10] :: Ecoupon                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 173ms]
:: Progress: [1105/4614] :: Job [1/1] :: 168 req/sec :: Duration: [0:00:10] :: Ecoupons1                [Status: 200, Size: 11829, Words: 1499, Lines: 151, Duration: 173ms]
:: Progress: [1106/4614] :: Job [1/1] :: 167 req/sec :: Duration: [0:00:10] :: E:: Progress: [1107/4614] :: Job [1/1] :: 166 req/sec :: Duration: [0:00:10] :: Ecourses                 [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 157ms]
:: Progress: [1107/4614] :: Job [1/1] :: 166 req/sec :: Duration: [0:00:10] :: Ecourse                  [Status: 200, Size: 11827, Words: 1499, Lines: 151, Duration: 169ms]
:: Progress: [1108/4614] :: Job [1/1] :: 163 req/sec :: Duration: [0:00:10] :: Ecover                   [Status: 200, Size: 11822, Words: 1499, Lines: 151, Duration: 166ms]
:: Progress: [1109/4614] :: Job [1/1] :: 163 req/sec :: Duration: [0:00:10] :: Ecovers                  [Status: 200, Size: 11823, Words: 1499, Lines: 151, Duration: 156ms]
:: Progress: [1109/4614] :: Job [1/1] :: 163 req/sec :: Duration: [0:00:10] :: Ecpadmin                 [Status: 200, Size: 11824, Words: 1499, Lines: 151, Duration: 159ms]
:: Progress: [1110/4614] :: Job [1/1] :: 159 req/sec :: Duration: [0:00:10] :: ECPAN                    [Status: 200, Size: 11821, Words: 1499, Lines: 151, Duration: 157ms]
:: Progress: [1112/4614] :: Job [1/1] :: 159 req/sec :: Duration: [0:00:10] :: Ecp                      [Status: 200, Size: 11819, Words: 1499, Lines: 151, Duration: 172ms]
:: Progress: [1113/4614] :: Job [1/1] :: 159 req/sec :: Duration: [0:00:10] :: Ecpanel                  [Status: 200, Size: 11823, Words: 1499, Lines: 151, Duration: 158ms]
:: Progress: [1114/4614] :: Job [1/1] :: 158 req/sec :: Duration: [0:00:10] :: Ecpanel_file             [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 157ms]
:: Progress: [1115/4614] :: Job [1/1] :: 157 req/sec :: Duration: [0:00:10] :: EcPanel                  [Status: 200, Size: 11823, Words: 1499, Lines: 151, Duration: 161ms]
:: Progress: [1116/4614] :: Job [1/1] :: 157 req/sec :: Duration: [0:00:10] :: Ecpstyles                [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 191ms]
:: Progress: [1117/4614] :: Job [1/1] :: 157 req/sec :: Duration: [0:00:10] :: Ecrack                   [Status: 200, Size: 11822, Words: 1499, Lines: 151, Duration: 184ms]
:: Progress: [1118/4614] :: Job [1/1] :: 154 req/sec :: Duration: [0:00:10] :: Ecreate                  [Status: 200, Size: 11823, Words: 1499, Lines: 151, Duration: 191ms]
:: Progress: [1119/4614] :: Job [1/1] :: 163 req/sec :: Duration: [0:00:10] :: E:: Progress: [1119/4614] :: Job [1/1] :: 163 req/sec :: Duration: [0:00:10] :: Ecpp                     [Status: 200, Size: 11820, Words: 1499, Lines: 151, Duration: 205ms]
:: Progress: [1120/4614] :: Job [1/1] :: 163 req/sec :: Duration: [0:00:10] :: Ecreditcards             [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 173ms]
:: Progress: [1121/4614] :: Job [1/1] :: 163 req/sec :: Duration: [0:00:10] :: Ecrashes                 [Status: 200, Size: 11824, Words: 1499, Lines: 151, Duration: 193ms]
:: Progress: [1122/4614] :: Job [1/1] :: 165 req/sec :: Duration: [0:00:10] :: Ecps                     [Status: 200, Size: 11820, Words: 1499, Lines: 151, Duration: 206ms]
:: Progress: [1123/4614] :: Job [1/1] :: 167 req/sec :: Duration: [0:00:10] :: Ecpath                   [Status: 200, Size: 11822, Words: 1499, Lines: 151, Duration: 214ms]
:: Progress: [1124/4614] :: Job [1/1] :: 168 req/sec :: Duration: [0:00:10] :: Ecr                      [Status: 200, Size: 11819, Words: 1499, Lines: 151, Duration: 201ms]
:: Progress: [1125/4614] :: Job [1/1] :: 168 req/sec :: Duration: [0:00:10] :: Ecpw                     [Status: 200, Size: 11820, Words: 1499, Lines: 151, Duration: 205ms]
:: Progress: [1126/4614] :: Job [1/1] :: 168 req/sec :: Duration: [0:00:10] :: Ecrontab                 [Status: 200, Size: 11824, Words: 1499, Lines: 151, Duration: 180ms]
:: Progress: [1127/4614] :: Job [1/1] :: 169 req/sec :: Duration: [0:00:10] :: Ecredit                  [Status: 200, Size: 11823, Words: 1499, Lines: 151, Duration: 188ms]
:: Progress: [1128/4614] :: Job [1/1] :: 170 req/sec :: Duration: [0:00:10] :: Ecreate_account          [Status: 200, Size: 11831, Words: 1499, Lines: 151, Duration: 200ms]
:: Progress: [1129/4614] :: Job [1/1] :: 170 req/sec :: Duration: [0:00:10] :: ECreatives               [Status: 200, Size: 11826, Words: 1499, Lines: 151, Duration: 190ms]
:: Progress: [1130/4614] :: Job [1/1] :: 171 req/sec :: Duration: [0:00:10] :: Ecreateaccount           [Status: 200, Size: 11830, Words: 1499, Lines: 151, Duration: 197ms]
:: Progress: [1131/4614] :: Job [1/1] :: 171 req/sec :: Duration: [0:00:10] :: Ecrontabs                [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 188ms]
:: Progress: [1132/4614] :: Job [1/1] :: 174 req/sec :: Duration: [0:00:10] :: Ecreator                 [Status: 200, Size: 11824, Words: 1499, Lines: 151, Duration: 197ms]
:: Progress: [1133/4614] :: Job [1/1] :: 175 req/sec :: Duration: [0:00:10] :: Ecrm                     [Status: 200, Size: 11820, Words: 1499, Lines: 151, Duration: 192ms]
:: Progress: [1133/4614] :: Job [1/1] :: 176 req/sec :: Duration: [0:00:10] :: Ecrash                   [Status: 200, Size: 11822, Words: 1499, Lines: 151, Duration: 214ms]
:: Progress: [1135/4614] :: Job [1/1] :: 176 req/sec :: Duration: [0:00:10] :: Ecrossdomain.xml         [Status: 200, Size: 11832, Words: 1499, Lines: 151, Duration: 186ms]
:: Progress: [1136/4614] :: Job [1/1] :: 176 req/sec :: Duration: [0:00:10] :: Ecron                    [Status: 200, Size: 11821, Words: 1499, Lines: 151, Duration: 199ms]
:: Progress: [1137/4614] :: Job [1/1] :: 176 req/sec :: Duration: [0:00:10] :: Ecrossdomain             [Status: 200, Size: 11828, Words: 1499, Lines: 151, Duration: 197ms]
:: Progress: [1138/4614] :: Job [1/1] :: 177 req/sec :: Duration: [0:00:10] :: Ecrms                    [Status: 200, Size: 11821, Words: 1499, Lines: 151, Duration: 202ms]
:: Progress: [1139/4614] :: Job [1/1] :: 181 req/sec :: Duration: [0:00:10] :: Ecrons                   [Status: 200, Size: 11822, Words: 1499, Lines: 151, Duration: 200ms]
:: Progress: [1140/4614] :: Job [1/1] :: 181 req/sec :: Duration: [0:00:10] :: Ecronjobs                [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 202ms]
:: Progress: [1141/4614] :: Job [1/1] :: 181 req/sec :: Duration: [0:00:10] :: Ecreation                [Status: 200, Size: 11825, Words: 1499, Lines: 151, Duration: 210ms]
:: Progress: [1142/4614] :: Job [1/1] :: 181 req/sec :: Duration: [0:00:10] :: Ecredits                 [Status: 200, Size: 11824, Words: 1499, Lines: 151, Duration: 206ms]
:: Progress: [1143/4614] :: Job [1/1] :: 187 req/sec :: Duration: [0:00:1

---

**Pakar liye gaye!** Yeh jo output aap ke saamne chal raha hai na, is ko kehte hain **Wildcard Resolution** ya **False Positive Matrix**.

Aap ne terminal par ghaur kiya? `ffuf` har word (chahe woh `companies` ho, `Ecomputer` ho, ya `contact_bean`) par **`Status: 200`** de raha hai, aur sab ka size bilkul same hai: **`Size: 11830` ya `11828**`!

### 🔍 Hacker Logic: Yeh Kya Scene Hai?

Jab koi website har random word par `200 OK` dainay lagay aur response ka size bilkul barabar ho, toh iska matlab yeh hota hai ke:

1. **Custom 404 Page:** Server par aesi setting hui hai ke agar koi directory majood *na* bhi ho, toh woh `404 Not Found` error dainay ke bajaye user ko main page ya kisi custom default page par redirect kar deta hai aur status `200` bhejta hai.
2. Hamari command un saare false results ko asli samajh kar terminal par dikhaye ja rahi hai. Is wajah se hamara scan kharab ho raha hai.

---

### 🛠️ Data-Driven Rule: Is False Positive Ko Kaise Filter Karein?

Isay dhoop mein kharay ho kar brute-force karne ki zaroorat nahi, hum isay abhi ke abhi filter out karenge. `ffuf` ke paas is masle ka bohot solid hal hai jise **Size Filter (`-fs`)** kehte hain.

Chunke kharab (false) responses ka size **`11824` se le kar `11837**` ke beech mein ghoom raha hai, hum `ffuf` ko kahenge ke is size ke aas pass wale saare results ko gayab (filter) kar de!

Pehle apne terminal mein **`Ctrl + C`** daba kar is chalte huve scan ko rokein, aur phir yeh nayi filtered command chalayein:

```bash
ffuf -u https://www.iaggbs.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -H "X-BugCrowd-traffic: habib_kali" -mc 200,301,302 -fs 11820-11840

```

* **`-fs 11820-11840` Kya Karega?** Yeh is range ke saare faltu responses ko block kar dega, aur terminal par sirf wahi cheez dikhayega jo waqai real directory hogi.

---

Same error aaya phir bhi

---

#### Is command ko yahin chorte hain aur aage barhte hain. Directory brute-forcing ka concept aur is ke kachray (false positives) ko filter karne ka tareeqa aap ko samajh aa gaya hai, jo asal maqsad tha.

Jab hum `ffuf` se directories dhoond lete hain, toh reconnaissance (recon) ka agla logical step hota hai **Vulnerability Scanning** ya **Fuzzing for Specific Files/Parameters** taake hum website ke andar kamzorian dhoond sakein.

Abhi hum isi `ffuf` tool ko aik naye aur mazeed interesting tareeqay se use karenge: **File Extension Fuzzing**.

---

### 📂 Next Process: File Extensions Dhoondna (`-e` Flag)

Kabi kabi directories ke andar ahem files chhupi hoti hain jo sirf naam se nahi miltin, un ke aage un ki extension (jaise `.php`, `.txt`, `.html`, ya `.bak`) lagana zaroori hota hai. For example, agar kisi developer ne ghalti se backup file chhor di ho (`config.bak` ya `db.php`), toh woh hamein bohot bada access de sakti hai.

Hum `ffuf` ko bolenge ke wordlist ke har lafzh ke aage yeh extensions laga kar check kare.

Aap terminal par yeh naya command run karein:

```bash
ffuf -u https://www.iaggbs.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -H "X-BugCrowd-traffic: habib_kali" -e .php,.txt,.html,.bak -mc 200,301,302 -ac

```

---

### 🔬 Is Command Ki Teh Tak Jaate Hain:

Hum ne purani command mein sirf aik naya flag add kiya hai:

* **`-e .php,.txt,.html,.bak`**: Yeh `ffuf` ko batata hai ke agar wordlist mein lafzh hai `secret`, toh woh sirf `secret` check nahi karega, balki yeh charo cheezain check karega:
1. `secret.php`
2. `secret.txt`
3. `secret.html`
4. `secret.bak`

---

## Output






---

#### Terminal mein **Subdomain Enumeration** shuru karte hain. Yeh web path se bilkul alag cheez hai.

Is ka maqsad yeh hai ke hum check karein ke `iaggbs.com` ke aage kya koi aur chhupi hui websites hain? Jaise `admin.iaggbs.com`, `test.iaggbs.com`, ya `dev.iaggbs.com`. Aksar main website bohot secure hoti hai, lekin subdomains par developer purana code chhor dete hain jahan aasani se vulnerabilities mil jati hain.

Kali Linux mein is kaam ke liye aik bohot hi tez aur advance tool hai jis ka naam hai **`subfinder`**.

---

### 🚀 Naya Process: Subdomain Enumeration

Aap aik **Naya Terminal Tab ya Window** (`Ctrl + Shift + T`) kholein aur wahan yeh command run karein:

```bash
subfinder -d iaggbs.com -v

```

### 🔬 Is Command Mein Kya Ho Raha Hai?

* **`subfinder`**: Yeh tool bina website ko hit kiye (passively) dunya bhar ke internet records aur search engines se is domain ke saare subdomains nikal leta hai. Yeh bohot fast hai!
* **`-d iaggbs.com`**: Is ka matlab hai "Domain". Hum apna target domain bata rahe hain.
* **`-v`**: Verbose mode, taake hamein live screen par nazar aaye ke yeh kahan kahan dhoond raha hai.

---

## Output

┌──(habib㉿kali)-[~]
└─$ subfinder -d iaggbs.com -v

               __    _____           __         
   _______  __/ /_  / __(_)___  ____/ /__  _____
  / ___/ / / / __ \/ /_/ / __ \/ __  / _ \/ ___/
 (__  ) /_/ / /_/ / __/ / / / / /_/ /  __/ /    
/____/\__,_/_.___/_/ /_/_/ /_/\__,_/\___/_/

		projectdiscovery.io

[INF] Current subfinder version v2.14.0 (latest)
[INF] Loading provider config from /home/habib/.config/subfinder/provider-config.yaml
[DBG] Selected source(s) for this search: bevigil, c99, certspotter, dnsrepo, onyphe, redhuntlabs, anubis, crtsh, fofa, fullhunt, leakix, alienvault, driftnet, profundis, quake, reconeer, rsecloud, thc, censys, chaos, domainsproject, intelx, digitalyama, securitytrails, chinaz, shodan, urlscan, builtwith, digitorus, dnsdumpster, robtex, virustotal, bufferover, hackertarget, whoisxmlapi, windvane, submd

[submd] cpanel.iaggbs.com
[submd] dev.ifcomms.cmt.procurement.iaggbs.com
[submd] dev.procurement.iaggbs.com
[submd] ess.iaggbs.com
[submd] forum.dev.procurement.iaggbs.com
[submd] forum.procurement.iaggbs.com
[submd] iagchat.iaggbs.com
[submd] iagchat.dev.iaggbs.com
[submd] idam-nonprod-signing.iaggbs.com
[submd] idam-signing.iaggbs.com
[submd] ifcomms.cmt.procurement.iaggbs.com
[submd] link.iaggbs.com
[submd] mail.iaggbs.com
[submd] procurement.iaggbs.com
[submd] ssdd.cfs.iaggbs.com
[submd] ssdp.cfs.iaggbs.com
[submd] ssdq.cfs.iaggbs.com
[submd] ssdx.cfs.iaggbs.com
[submd] webdisk.iaggbs.com
[submd] webmail.iaggbs.com
[submd] www.iaggbs.com
[submd] www.dev.ifcomms.cmt.procurement.iaggbs.com
[submd] www.ifcomms.cmt.procurement.iaggbs.com
[hackertarget] ssdd.cfs.iaggbs.com
[hackertarget] ssdp.cfs.iaggbs.com
[hackertarget] ssdq.cfs.iaggbs.com
[hackertarget] ssdx.cfs.iaggbs.com
[hackertarget] link.iaggbs.com
[hackertarget] forum.dev.procurement.iaggbs.com
[hackertarget] forum.procurement.iaggbs.com
[crtsh] www.iaggbs.com
[crtsh] iagchat.iaggbs.com
[crtsh] forum.procurement.iaggbs.com
[crtsh] forum.dev.procurement.iaggbs.com
[crtsh] iagchat.dev.iaggbs.com
[crtsh] ssdd.cfs.iaggbs.com
[crtsh] ssdp.cfs.iaggbs.com
[crtsh] ssdq.cfs.iaggbs.com
[crtsh] ssdx.cfs.iaggbs.com
[crtsh] link.iaggbs.com
[crtsh] procurement.iaggbs.com
[crtsh] dev.procurement.iaggbs.com
[crtsh] ess.iaggbs.com
[crtsh] iag.tenderportal.iaggbs.com
[crtsh] dev.iag.tenderportal.iaggbs.com
[crtsh] ifcomms.cmt.procurement.iaggbs.com
[crtsh] www.ifcomms.cmt.procurement.iaggbs.com
[crtsh] dev.ifcomms.cmt.procurement.iaggbs.com
[crtsh] www.dev.ifcomms.cmt.procurement.iaggbs.com
[crtsh] iagchat.prod.iaggbs.com
[crtsh] xxx.ssdd.cfs.iaggbs.com
[crtsh] xxx.ssdp.cfs.iaggbs.com
[crtsh] xxx.ssdq.cfs.iaggbs.com
[crtsh] idam-nonprod-signing.iaggbs.com
[crtsh] idam-signing.iaggbs.com
[crtsh] cpanel.iaggbs.com
[crtsh] cpcalendars.iaggbs.com
[crtsh] cpcontacts.iaggbs.com
[crtsh] mail.iaggbs.com
[crtsh] webdisk.iaggbs.com
[crtsh] webmail.iaggbs.com
webmail.iaggbs.com
www.dev.ifcomms.cmt.procurement.iaggbs.com
dev.iag.tenderportal.iaggbs.com
iag.tenderportal.iaggbs.com
xxx.ssdq.cfs.iaggbs.com
iagchat.dev.iaggbs.com
cpanel.iaggbs.com
idam-signing.iaggbs.com
webdisk.iaggbs.com
ess.iaggbs.com
dev.procurement.iaggbs.com
ssdp.cfs.iaggbs.com
iagchat.iaggbs.com
procurement.iaggbs.com
dev.ifcomms.cmt.procurement.iaggbs.com
cpcalendars.iaggbs.com
cpcontacts.iaggbs.com
www.iaggbs.com
idam-nonprod-signing.iaggbs.com
mail.iaggbs.com
iagchat.prod.iaggbs.com
xxx.ssdp.cfs.iaggbs.com
ssdq.cfs.iaggbs.com
forum.procurement.iaggbs.com
xxx.ssdd.cfs.iaggbs.com
ssdd.cfs.iaggbs.com
ssdx.cfs.iaggbs.com
link.iaggbs.com
forum.dev.procurement.iaggbs.com
ifcomms.cmt.procurement.iaggbs.com
www.ifcomms.cmt.procurement.iaggbs.com
[INF] Found 31 subdomains for iaggbs.com in 21 seconds 646 milliseconds

---

#### 21 seconds mein **31 subdomains** dhoond nikale hain.

Aap ke terminal output mein agar hum ghaur karein, toh shuru mein jo bohot saara kachra (API errors) aa raha tha, usay ignore maren—woh is liye tha kyunki hum ne premium API keys configure nahi ki thin. Lekin uske bawajood, jo free sources thin (jaise `thc`, `submd`, `hackertarget`, aur `crtsh`), unhon ne kamaal kar diya.

Niche jo 31 subdomains ki list aayi hai, us mein se **kuch bohot hi high-value aur interesting targets** nazar aa rahe hain jo aik penetration tester ke liye sone ki khaan (goldmine) hote hain:

### 🔎 Ahem Targets Jo Samne Aaye Hain:

1. **Development & Testing:**
* `iagchat.dev.iaggbs.com`
* `dev.procurement.iaggbs.com`
* `forum.dev.procurement.iaggbs.com`
* `dev.iag.tenderportal.iaggbs.com`
*(Developers aksar `dev.` ya testing subdomains par security lagaana bhool jaate hain ya purana code chhor dete hain).*


2. **Portals & Port Chhupane Wali Jaghein:**
* `cpanel.iaggbs.com` (Control Panel login)
* `webmail.iaggbs.com` & `mail.iaggbs.com` (Email infrastructure)
* `iag.tenderportal.iaggbs.com` (Tender portal, jahan financial documents ya file uploads ho sakte hain).


3. **Ajeeb/Hidden Subdomains:**
* `xxx.ssdq.cfs.iaggbs.com` (Yeh triple subdomains kafi deep hain, inko check karna banta hai).



---

### 🛠️ Next Step: In Subdomains Ka Kya Karein?

Abhi hamare paas sirf subdomains ke **naatay** (names) aaye hain. Hamein nahi pata ke in 31 mein se kaun kaun se subdomains **waqai is waqt live/active** hain aur chal rahe hain, kyunki kuch purane ya dead bhi ho sakte hain.

In sab ko aik aik kar ke browser mein check karna bohot boring aur time-taking kaam hai. Toh hum kya karenge? Kali Linux mein aik aur zabardast aur fast tool use karenge jo yeh check karega ke **kaun sa subdomain live hai (HTTP 200 ya 301 de raha hai)**.

Us tool ka naam hai **`httpx`** (ya `httprobe`).

Pehle aap is subdomain ki list ko aik file mein save karlein taake hum agla process shuru kar sakein. Usi terminal mein yeh command run karein jo in subdomains ko seedha aik text file mein save kar degi:

```bash
subfinder -d iaggbs.com -o subdomains.txt

```

*(Yeh command silent chalegi aur saare subdomains ko `subdomains.txt` naam ki file mein daal degi).*

---

Ab agla step yeh hai ke hum check karein ke in 31 subdomains mein se **kaun kaun se waqai is waqt live (active) hain**, taake hum apna waqt dead links par zaya na karein. Is kaam ke liye hum **`httpx`** tool use karenge, jo bohot fast hai aur live websites ko filter out kar deta hai.

Aap usi terminal mein yeh command run karein:

```bash
httpx -l subdomains.txt -title -tech-detect -status-code -o live_subs.txt

```

---

### 🔬 Is Command Mein Kya Ho Raha?

* **`-l subdomains.txt`**: Yeh hamari banayi hui list ko input le raha hai.
* **`-title`**: Yeh har live subdomain ka web title (jaise "Login Page" ya "Dashboard") nikal kar dikhayega.
* **`-tech-detect`**: Yeh website ke peeche chalne wali technology (jaise WordPress, Apache, PHP, ya Cloudflare) dhoond nikalega.
* **`-status-code`**: Yeh batayega ke HTTP response kya hai (`200 OK`, `301 Redirect`, ya `403 Forbidden`).
* **`-o live_subs.txt`**: Yeh saare live aur kaam ke results ko aik nayi file `live_subs.txt` mein save kar dega.

---

## Output

┌──(habib㉿kali)-[~/Documents/Reconnassiance]
└─$ httpx -l subdomains.txt -title -tech-detect -status-code -o live_subs.txt
Usage: httpx [OPTIONS] URL

Error: No such option: -l

---

#### Kali Linux mein ProjectDiscovery wala `httpx` install nahi hai, balki Python wala standard `httpx` library ka CLI install hai, jo sirf aik single URL leta hai aur is tarah ke flags (`-l`, `-title`) ko nahi samajhta.

Chalein, koi masla nahi! Hum standard Linux tools aur `curl` ka aik chota sa loop bana kar khud hi apna desi "Live Subdomain Checker" chala lete hain, bina kisi naye tool ke jhanjhat ke.

Usi terminal mein yeh poori command copy-paste kar ke Enter maro:

```bash
while read sub; do curl -s -o /dev/null -w "%{http_code} %{url_effective}\n" "https://$sub" --connect-timeout 3; done < subdomains.txt | grep -E "^(200|301|302|403)" | tee live_subs.txt

```

### 🔬 Yeh Desi Command Kya Kar Rahi Hai?

1. **`while read sub; do ... done < subdomains.txt`**: Yeh `subdomains.txt` file mein se aik aik kar ke saare 31 subdomains ko uthayegi.
2. **`curl -s -o /dev/null -w "... %{url_effective}\n"`**: Yeh background mein har subdomain par request bhejegi aur screen par kachra dikhane ke bajaye sirf us ka **Status Code** aur **URL** print karegi.
3. **`--connect-timeout 3`**: Agar koi subdomain dead hai, toh yeh sirf 3 seconds wait karegi aur aage barh jayegi (taake waqt zaya na ho).
4. **`grep -E "^(200|301|302|403)"`**: Yeh sirf un subdomains ko screen par layegi jo active hain (chahe access ho ya redirection ya 403 Forbidden).
5. **`tee live_subs.txt`**: Yeh results ko terminal par bhi dikhayegi aur sath hi sath `live_subs.txt` file mein save bhi karti jayegi.

---

## Output

Hamara desi script perfect kaam kar gaya aur is ne kachra links ko filter out kar ke **3 live subdomains** dhoond nikale hain:

```text
403 https://ssdq.cfs.iaggbs.com/
403 https://ssdd.cfs.iaggbs.com/
403 https://ssdp.cfs.iaggbs.com/

```

### 🔬 In Results Ka Kya Matlab Hai? (The Hacker's Perspective)

Teeno targets par **`403 Forbidden`** status code aa raha hai. Aik aam banda sochega ke *"Yaar yeh toh block hain, yahan kuch nahi milne wala."* Lekin aik penetration tester ke liye yeh aik bohot interesting situation hoti hai:

1. **Website Live Hai:** `403` ka matlab hai ke server active hai aur hamari request ko responsive hai (agar server down hota toh code `000` ya timeout aata).
2. **Access Restricted Hai:** Server keh raha hai ke *"Aap ko is directory ya page ko dekhne ki ijaazat nahi hai."* 3. **Peeche Kuch Chhupa Hai:** Aksar `403 Forbidden` tab aata hai jab main directory listing band ho, lekin us ke andar ahem files ya administrative panels (jaise `/admin`, `/login`, `/config.php`) maujood hon jin tak direct ijaazat na ho.

---

### 🛠️ Next Process: "403 Bypass" Aur Directory Fuzzing

Ab hum in teeno mein se kisi aik target ko pakar kar us ke andar chhupi hui files dhoondne ki koshish karenge. Kyun ke `ffuf` par hum pehle hi kafi kaam kar chuke hain, ab hum Kali Linux ka sab se mashhoor aur pyara tool use karenge: **`dirb`** ya **`dirbuster`** (CLI version).

Chalein, pehle target (`ssdq.cfs.iaggbs.com`) par attack karte hain yeh dekhne ke liye ke kya is restricted portal ke andar koi khula hua rasta milta hai ya nahi.

Aap terminal par yeh command run karein:

```bash
dirb https://ssdq.cfs.iaggbs.com/ /usr/share/wordlists/dirb/common.txt -H "X-BugCrowd-traffic: habib_kali"

```

### 💡 Is Command Mein Naya Kya Hai?

* **`dirb`**: Yeh Kali Linux ka built-in directory brute-forcing tool hai. Yeh thoda simple hai aur is ka output dekhna aur samajhna kafi aasan hota hai.
* Yeh check karega ke kya `https://ssdq.cfs.iaggbs.com/` ke aage koi aisa page hai (jaise `/index.html` ya `/login`) jo `403` ke bajaye direct `200 OK` de de.



