
Skip to content
This repository

    Pull requests
    Issues
    Marketplace
    Explore

    @kristel-

1
0

    0

kristel-/Regulaaravaldised
Code
Issues 0
Pull requests 0
Projects 0
Wiki
Settings
Regulaaravaldised/Regulaaravaldiste-õppematerjal
28ccdaf 26 seconds ago
@kristel- kristel- loengumaterjal
170 lines (136 sloc) 12.8 KB
# Regulaaravaldised
### *Kristel Uiboaed*
#### 29. september 2017

Regulaaravaldis (ingl *regular expression*) on erilises keeles üleskirjutatud valem, mis kirjeldab teatavat sõnede klassi. Regulaaravaldisest võib mõelda kui kontrolleeskirjast, mida rakendatakse (mingile) sõnele. Sõne kas vastab regulaaravaldisele või mitte.

Regulaararvaldisest võib mõelda ka kui teatud tüüpi keelest, millel on oma reeglid. Selles keeles kirjutamiseks ja sellest arusaamiseks tuleb need reeglid ära õppida. Mõnikord võib avaldise tähendus märkide järjekorra muutmisel täielikult muutuda. Mõnikord on aga võimalik sama asja väljendada väga erineval viisil. Mõnikord sõltub tähendus kontekstist.

## Mõisted
- **Literaalne sümbol** *(literal)*. Esinevad vaatlusaluses tekstis esitatud kujul, st esindavad regulaaravaldises iseennast.
- **Metasümbolid** *(metacharacter)*. Esindavad regulaaravaldises midagi muud (mitte iseennast).
- **Otsitav sõne** *(target string, search string)*. Sümbolitejärjend, millele regulaaravaldis peaks vastama, teatud mõttes otsingu märksõna.
- **Otsing, regulaaravaldis** *(search expression)*. Regulaaravaldis või sümbolitejärjend, mida kasutame otsitava sõne leidmiseks.
- **Varjestamine** *(escaping)*. Metasümboli muutmine literaalseks. Metasümboli saab muuta literaalseks, \\-märgiga, st erisümbolilt võetakse ära tema eritähendus ning peale varjestamist esindab see sümbol iseennast ehk on literaalne.
- Suuri ja väikseid tähti loetakse erinevateks sümboliteks, st et *a* ja *A* ei ole sama asi.

## Lihtsad otsingud
*Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes).*

- A: Ja dekanaat töötab **A**kadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes).
- aa: Ja dekan**aa**t töötab Akadeemia tee 3 ruumis 339 (uue r**aa**matukogu poolses küljes).
- 3: Ja dekanaat töötab Akadeemia tee **3** ruumis **33**9 (uue raamatukogu poolses küljes).
- 33: Ja dekanaat töötab Akadeemia tee 3 ruumis **33**9 (uue raamatukogu poolses küljes).
- u p: Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukog**u p**oolses küljes).
- 339 (uue: Ja dekanaat töötab Akadeemia tee 3 ruumis **339 (uue** raamatukogu poolses küljes).
- raamat: Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue **raama**tukogu poolses küljes).
- m: Ja dekanaat töötab Akadee**m**ia tee 3 ruu**m**is 339 (uue raa**m**atukogu poolses küljes).
- \\.: Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes)**.**

## Regulaaravaldistes kasutatavad sümbolid
| Sümbol | Tähistab  |
|--|--|
|**.**|  punkt: suvaline üks sümbol |
|**^**| (katus): rea algus, nurksulgude sees esimese märgina eitus.      Katusemärgi saab klaviatuurilt kombinatsiooniga `Shift + AltGr + ä`. |
|**$**|  (dollar): rea lõpp  |
|**\\**|  tagurpidi kaldkriips: teeb talle järgneva metasümboli literaalseks sümboliks|
|**\***|tärn: suvaline arv, sh 0 temast vasakule jäävat sümbolit (null kuni lõpmatu arv kordusi)|
|**\+** | pluss: eelnev sümbol kordub üks või enam korda: aa+ = *aa*, *aaa*, *aaaaa*, mitte *a*
|**?** | küsimärk: eelnev sümbol kordub null või üks kord: aa? = *a*, *aa*, mitte *aaa*
|**{n,m}** | looksulud: mitu eelnevat sümbolit (nt **ai{2}** leiab *aii*; ai{2,4} leiab |*aii*, *aiii* ja *aiiii*)
|**{n,}** | leiab vähemalt n eelnevat sümbolit
|**{,n}** |leiab kuni n eelnevat sümbolit 
|**{n}** | leiab n eelnevat sümbolit
|**[...]** | Klass: üks [ ] vahel olevatest sümbolitest. Nurksulgude sees on erimärgid tavalises tähenduses. Nii leiab [akm] kas *a*, *k* või *m*. NB! Nurksulgudes saab niimoodi otsida vaid üksikuid sümboleid, *a* või *k* või *m*, aga mitte järjendit *akm*. Ka kompleksseid märke, nt **\\w** ja **\\S** (põhjalikumalt hiljem), võib kasutada nurksulgude vahel. Kui nurksulgude vahel on vaja kasutada sidekriipsu (literaalsena) või lõpetavat nurksulgu, siis tuleb see panna esimeseks märgiks sulgude sees, või peab talle eelnema tagurpidi kaldkriips. Nii leiab **[]]** näiteks lõpetava nurksulu. **[0123456789]** (sobib iga number).|
|**[\^abc]**|Nurksulgudes on võimalik ka eitada, st mingid sümbolid otsingust välja arvata. Selleks tuleb **^** panna esimeseks märgiks sulgude sisse. (Kui **^** ei ole esimene märk, siis kasutatakse teda (literaalsena) nagu iga teist märki.) Nii näiteks leiab **A[^5]** järjendid *A4*, *A3*, *A2*, *A1*, *Aa*, kuid mitte *A5*. **[^^]** leiab kõik peale **^**. õimalik luua ka "negatiivseid" märgiklasse, kus sobib **“kõik, välja arvatud”**. Selleks tuleb klassi algusse asetada katus **^** **[^abc]** tähendab, et sobib iga märk, välja arvatud *a, b* või *c*.  **[^ ]** tähendab, et sobib kõik peale tühiku.**[^ ]\*** tähendab, et otsitakse kõiki sümboleid ükskõik kui palju, kuid mitte tühikuid.|
| **\--** |tähistab vahemikku|
| **\|** | Toru tähenduses **või**. Regulaaravaldis: **mina\|meie** otsib nii mina kui ka meie. NB! Pane tähele erinevust **[minameie]** ja **mina\|meie** vahel.
|**[a-z]<br>[A-Z]<br>[0-9]**|Kuna tähtedel ja numbritel on loogiline järjekord, võib neid vahemikke määrates ka lühendada: **[a-c]** on sama, mis **[abc]** ja **[0-9]** on sama, mis **[0123456789]**.Selliseid konstruktsioone võib kombineerida näiteks **[a-fynot1-38]** (selle vastab *a, b, c, d, e, f, y, n, o, t,* *1, 2, 3* või *8*). Et suur- ja väiketähti käsitletakse erinevatena, siis tuleb tõstutundetu märgiklassi loomiseks, mis leiaks näiteks *a, b, A* ja *B* kindlasti kirjutada **[aAbB]**.Aga kõik tähed? Milline tähestik? **[a-zA-Z] [a-üA-Ü]**[www.cl.ut.ee](www.cl.ut.ee) kasutajaliideses **[a-z]**, aga täpitähti esitavad olemid jäävad neist klassidest ikkagi välja.|
| **[:alpha:]** | tähistab tähestiku tähti
| **[:upper:]** | suurtähti
| **[:lower:]** | väiketähti
| **[:digit:]** | numbreid
| **[:punct:]** | kirjavahemärke

Eeeldefineeritud klassid ei kehti [www.cl.ut.ee](www.cl.ut.ee) kasutajaliideses, aga nt enamasti programmeerimiskeeltes olemas.

## Kvantorid. Mis on erinevus?
- \+ ja {1,}
- ? ja {0,1} ja {,1}

## Kvantorid ja lihtsad metasümbolid otsingus

*Ja dekanaat töötab Akadeemia tee 3 ruumis 339 (uue raamatukogu poolses küljes).*

*Ära sellegipoolest lase end sellest heidutada, AB-veregrupiga inimesega koos ei hakka sul kunagi igav, nad on alati valmis lõbutsema.*

- \.
- ^J
- ^ä
- \$
- l+
- a?
- na?
- [ms]ina
- mina|sina



## Mis nüüd?
*"Some people, when confronted with a problem, think \'I know I'll use regular expressions.\' Now they have two problems."* 

— Jamie Zawinski/Fredrik Lundh?

## Ülesanded
- Milline regulaaravaldis vastab tervele reale, ükskõik mida ja ükskõik millisel hulgal ta sisaldab?
- Milline regulaaravaldis vastab reale,
	- mis sisaldab ainult tühikuid?
	- mis ei sisalda ühtegi tühikut (aga ükskõik mida muud ükskõik kui palju)?
	- milles on mõni number?
	- milles pole ühtegi numbrit?

## Komplekssed märgid
Koosnevad tagurpidi kaldkriipsust (**\\**) ja ühest alltoodud märkidest. Kui \\ järel ei ole üht allpooltoodud märkidest, siis otsitakse \\-le järgnevat märki ennast. Nii näiteks leitakse \\$ vasteks dollarimärk.
|  |  |
|--|--|
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

Sõna defineeritakse kui tähtede-numbrite ja allkriipsude jada, nii et sõna lõppu tähistab tühik või märk, mis ei kuulu tähtede, numbrite ega allkriipsu hulka. Kuna täpitähed ja "susisevad" tähed kasutajaliideses www.cl.ut.ee sisaldavad ampersandi (&) ja semikoolonit (;), siis ei kuulu nad selle definitsiooni kohaselt sõna hulka, nagu ka sidekriips.


## Milleks mulle kõik see?
- Sest nad on igal pool (otsingumootorid, salasõna kontroll, andmebaaside otsingud jne)
- Teksti kiire töötlus (tee palju keerulisi asendusi ühe korraga)
- Täpsed tekstiotsingud
- Tekstidega töötamisel täiesti asendamatu abivahend
- Failitöötlus (nimeta ümber sada faili ühe korraga)
- Üsna universaalne töövahend (programmeerimiskeeled, andmebaasid toetavad)
- **Võimaldavad automatiseerida korduvaid tüütuid ülesndeid**

## "Ahned" (*greedy*) ja "laisad" (*lazy*) päringud
Kvantorid on vaikimisi "ahned", st et regulaaravaldisele vastab maksimaalne sobiv üksus. Enamasti pole see aga soovitud tulemus. Ahne päringu saab laisaks muuta ?-ga. Näiteks:

*Kuna rahast meeldib kõigile rääkida , siis püüangi järgnevalt seletada veebilansi müüdi olemust tavalise pere rahakoti mudeliga .*

Kuidas otsiksid sellest lausest *r*-ga algavaid sõnu?
- Mida otsib "**r.\***"?
- Aga " **r.\*?** "?

##  Kuidas otsida sellest tekstist ainult kõiki lauseid?
\<p\> \<s\> Võib-olla on aga praegusaja vanemaist teismelistest eakamad põlvkonnad juba lootusetult kadunud , et niisugusest " keelest ” aru saada ? <\/s> \<s\> Sallivust ja mõistmist , et kõik ei ole ega peagi olema ühesugused , pole siin maailmanurgas just kaua kuulutatud . <\/s> \<s\> Seda teemat käsitleti sovetlikus ühiskonnas peamiselt hea – halva skaalal : siledad , ühetaolised ja ohutud on " meiega ” . <\/s> \<s\> On head ja " normaalsed " . <\/s> \<s\> Teistsuguseid meil peaaegu ei olegi , või kui , siis on nad vaenlased või muidu väärdunud . <\/s> <\/p>

## Rühmad ja tagasiviitamine
Tavaliste sulgudega saab moodustada ka rühmi, millele on võimalik n-ö tagasi viidata või avaldist korrata. Sellisel juhul pole sulud osa otsitavast avaldisest, vaid tähistavad mingi vahemiku algus- ja lõpp-positsiooni näiteks **(@[\^ ]\*)**. Tagasiviitamiseks on võimalik koostada ka rohkem gruppe ja tagasi viidatakse sel juhul esinemisjärjekorras: \\1, \\2.

## Tagasiviitamise harjutus

  $\qquad$ *tere, tere, vana kere*

- Kuidas leida selle näite eeskujul juhtumid, kus sõna *tere* esineb kaks korda järjest?
- Kuidas samast näitest teha otsing kahe grupiga, nii et leitaks nii tere kui ka talle järgnev koma ja tühik?
- Kuidas tagasiviitamist ja rühmi kasutades vahetada sõnade *vana* ja *kere* järjekord?

Vastused juhuslikus järjekorras: (vana) (kere) ja \\2 \\1; (tere)(, )\\1\\2; (tere), \\1

![enter image description here](https://i.imgur.com/5oEOzcS.png)
![https://xkcd.com/208/](regular_expressions.png)

## Lisamaterjale
- Rohkem näiteid ja rakendusvõimalusi leiab näiteks korpuslingvistika kursuse [kodulehelt](korpuslingvistika.ut.ee).
- [Demystifying RegEx with Practical Examples](https://www.sitepoint.com/demystifying-regex-with-practical-examples/)
- [Here's what ICT should really teach kids: how to do regular expressions](https://www.theguardian.com/technology/2012/dec/04/ict-teach-kids-regular-expressions)
-  [Väga head lihtsad harjutused alustuseks](https://regexone.com/)
- Mõned selgitavad videod.
	- [https://www.youtube.com/watch?v=hwDhO1GLb_4](https://www.youtube.com/watch?v=hwDhO1GLb_4)
	- [https://www.youtube.com/watch?v=RGLldper5II](https://www.youtube.com/watch?v=RGLldper5II)
	- [https://www.youtube.com/watch?v=DRR9fOXkfRE](https://www.youtube.com/watch?v=DRR9fOXkfRE)
- [Kirjakeele korpuste kontekstis](http://www.cl.ut.ee/korpused/kasutajaliides/erispikker#reg)
- [Näiteid, viiteid, õpetusi](http://www.regular-expressions.info/)
- [Regulaaravalidsi valmiskujul](http://regexlib.com/?AspxAutoDetectCookieSupport=1)
- Testi oma avaldist
	- [http://regexr.com/](http://regexr.com/)
	- [http://www.regexpal.com/](http://www.regexpal.com/)
- [Sissejuhatav ülevaade](http://www.zytrax.com/tech/web/regex.htm)
- Regulaaravaldiste spikreid: [1](http://www.cheatography.com/davechild/cheat-sheets/regular-expressions/), [2](http://regexlib.com/CheatSheet.aspx), [3](http://www.rexegg.com/regex-quickstart.html)
- [Mõnest edasijõudnumast teemast](http://www.smashingmagazine.com/2009/05/introduction-to-advanced-regular-expressions/)
- Kaks eestikeelset testi korpuslingvistika kursuselt: [natuke lihstam](https://www.onlinequizcreator.com/regulaaravaldised-1/quiz-204859) ja [natuke raskem test](https://www.onlinequizcreator.com/regulaaravaldised-2/quiz-204634). Testid on koostanud Eleri Aedmaa.
