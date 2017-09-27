# Regulaaravaldised

Õppematerjalid kursuse Arvuti kasutamine keeleuurimisel (FLEE.08.103) jaoks.

## Regulaaravaldistes kasutatavad sümbolid
| Sümbol | Tähistab  |
|--|--|
|**.**|  punkt: suvaline üks sümbol |
|**^**| katus: rea algus, nurksulgude sees esimese märgina eitus.      Katusemärgi saab klaviatuurilt kombinatsiooniga `Shift + AltGr + ä`. |
|**$**| dollar: rea lõpp  |
|**\\**|  tagurpidi kaldkriips: teeb talle järgneva metasümboli literaalseks sümboliks|
|**\***|tärn: suvaline arv, sh 0 temast vasakule jäävat sümbolit (null kuni lõpmatu arv kordusi)|
|**\+** | pluss: eelnev sümbol kordub üks või enam korda: aa+ = *aa*, *aaa*, *aaaaa*, mitte *a*
|**?** | küsimärk: eelnev sümbol kordub null või üks kord: aa? = *a*, *aa*, mitte *aaa*
|**{n,m}** | looksulud: mitu eelnevat sümbolit (nt **ai{2}** leiab *aii*; ai{2,4} leiab *aii*, *aiii* ja *aiiii*)
|**{n,}** | leiab vähemalt n eelnevat sümbolit
|**{,n}** |leiab kuni n eelnevat sümbolit 
|**{n}** | leiab n eelnevat sümbolit
|**[...]** | Klass: üks [ ] vahel olevatest sümbolitest. Nurksulgude sees on erimärgid tavalises tähenduses. Nii leiab [akm] kas *a*, *k* või *m*. NB! Nurksulgudes saab niimoodi otsida vaid üksikuid sümboleid, *a* või *k* või *m*, aga mitte järjendit *akm*. Ka kompleksseid märke, nt **\\w** ja **\\S** (põhjalikumalt hiljem), võib kasutada nurksulgude vahel. Kui nurksulgude vahel on vaja kasutada sidekriipsu (literaalsena) või lõpetavat nurksulgu, siis tuleb see panna esimeseks märgiks sulgude sees, või peab talle eelnema tagurpidi kaldkriips. Nii leiab **[]]** näiteks lõpetava nurksulu. **[0123456789]** (sobib iga number).|
|**[\^abc]**|Nurksulgudes on võimalik ka eitada, st mingid sümbolid otsingust välja arvata. Selleks tuleb **^** panna esimeseks märgiks sulgude sisse. (Kui **^** ei ole esimene märk, siis kasutatakse teda (literaalsena) nagu iga teist märki.) Nii näiteks leiab **A[^5]** järjendid *A4*, *A3*, *A2*, *A1*, *Aa*, kuid mitte *A5*. **[^^]** leiab kõik peale **^**. Võimalik luua ka "negatiivseid" märgiklasse, kus sobib **“kõik, välja arvatud”**. Selleks tuleb klassi algusse asetada katus **^** **[^abc]** tähendab, et sobib iga märk, välja arvatud *a, b* või *c*.  **[^ ]** tähendab, et sobib kõik peale tühiku.**[^ ]\*** tähendab, et otsitakse kõiki sümboleid ükskõik kui palju, kuid mitte tühikuid.|
| **\-** |tähistab vahemikku|
| **\|** | Toru tähenduses **või**. Regulaaravaldis: **mina\|meie** otsib nii mina kui ka meie. NB! Pane tähele erinevust **[minameie]** ja **mina\|meie** vahel.
|**[a-z]<br>[A-Z]<br>[0-9]**|Kuna tähtedel ja numbritel on loogiline järjekord, võib neid vahemikke määrates ka lühendada: **[a-c]** on sama, mis **[abc]** ja **[0-9]** on sama, mis **[0123456789]**. Selliseid konstruktsioone võib kombineerida näiteks **[a-fynot1-38]** (selle vastab *a, b, c, d, e, f, y, n, o, t,* *1, 2, 3* või *8*). Et suur- ja väiketähti käsitletakse erinevatena, siis tuleb tõstutundetu märgiklassi loomiseks, mis leiaks näiteks *a, b, A* ja *B* kindlasti kirjutada **[aAbB]**. Aga kõik tähed? Milline tähestik? **[a-zA-Z] [a-üA-Ü]**. [Kirjakeele korpuse](www.cl.ut.ee) kasutajaliideses **[a-z]**, aga täpitähti esitavad olemid jäävad neist klassidest ikkagi välja.|
| **[:alpha:]** | tähestiku tähed
| **[:upper:]** | suurtähed
| **[:lower:]** | väiketähed
| **[:digit:]** | numbrid
| **[:punct:]** | kirjavahemärgid
| **\\A** | Leiab rea alguse (sama mis **^**).
| **\\b** | Leiab sõna alguse ja lõpu.
| **\\t** | või **\\011** tabulaator
|**\\n** | või **\\012** nn *newline*, Unixi/Linuxi reavahetus ja sageli selline ka tavalistes tekstiredaktorites.
| **\\r** | või **\\015** nn Windowsi reavahetus NB! Windowsi tekstifailides on rea lõpus **\\r\\n** Oluline teada, kui kasutad tulevikus tekstitöötlemiseks skripte: **\\r\\f** *form feed* (uus lehekülg; leheküljevahetus)
|**\\v** | *vertical tab*, nn vertikaalne kriips
|**\\d** | Leiab iga numbri. Samaväärne väljendiga **[0-9]**.
|**\\D** | Leiab iga mittenumbri. Samaväärne väljendiga **[^0-9]**.
|**\\s** | Leiab iga "valge vahe". Samaväärne **[ \\t\\n\\r\\f\\v]**.
|**\\S** | Leiab iga mitte-"valge vahe". Samaväärne **[^ \\t\\n\\r\\f\\v]**.
|**\\w** | Leiab iga tähe, numbri või allkriipsu. Samaväärne klassiga **[a-zA-Z0-9_]** kasutajaliideses, AGA ei otsi html-täpitähti; samaväärne klassiga **[a-üA-Ü0-9_]**.
|**\\W** | Leiab iga mitte-tähe, -numbri või -allkriipsu. Samaväärne väljendiga **[\\^a-zA-Z0-9_]** kasutajaliideses. Vt ka eelmist märkust.
|**\\Z** | Leiab rea lõpu. Samaväärne **$**-ga.
