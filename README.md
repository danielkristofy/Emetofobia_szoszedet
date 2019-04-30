# Emetofóbiás szűrő szószedet Firefox Advanced Profanity Filter addon-hoz
Az itt található leírást/videót valamint szószedetet egy emetofóbiás barátom számára, és az ő visszajelzései alapján készítettem – a végcél az volt, hogy egy böngészőbe beépülő kiegészítőn keresztül – ki-bekapcsolható módon, amikor különösebben szüksége van rá - ki lehessen szűrni a számára kellemetlen szavakat, azok ne, vagy máshogy, nem zavaró módon jelenjenek meg böngészés közben.
Egy alapvetően káromkodásokat kiszűrő, de szerkeszthető szószedetű kiegészítőt alakítottam át a célra: végeredményében annyit tesz, hogy egyrészt az emetofóbia számára kockázatosabb kifejezéseket kiszűri (a helyükre érthetetlen karaktersorokat rak), másrészt a kényes szavakat csak véletlenül tartalmazó, de úgyamúgy más tartalmú szavak helyére olyan szinonimákat rak, amik értelmükben közelítik az eredetit, de biztonságosabb módon. (pl „mennyiszer”).
Ez utóbbiból néha furcsa, tekervényes mondatok lesznek, de az eddigi teszteléseink során nem igazán találtunk olyan kivételt, ahol ez érthetetlenné tette volna az eredeti szöveget – végső soron viszont az egész modul gyorsan kikapcsolható.

Minden esetben a cserélt szavakat [ ]-között jelzi.

Csak Firefox böngészővel (de annak mind az asztali, mind a mobil változatával) teszteltem, de ha valaki egy hasonló (RegEx képes), egyéb böngészőre fejlesztett cenzúra-kiegészítőre szeretné átültetni, az némi hozzáértéssel a jelen szószedet alapján valószínűleg nem túl nagy munka. 
Chrome változatot is találtam ugyan ettől a fejlesztőtől, de ugyan ennek a listának a beillesztésekor hibát dob ki, amit valószínűleg nem túl bonyolult orvosolni, de némi utánajárás szükséges.
## Telepítése, használata
A szükséges firefox plugin és a szószedet telepítése megtalálható az alábbi videón is:

* Első lépés az egész alapjául szolgáló Firefox kiegészítő telepítése az alábbi linkről: https://addons.mozilla.org/hu/firefox/addon/advanced_profanity_filter/
* Ezután a kiegészítő szószedet beállításaihoz kell eljutni (add-ons / advanced profanity filter / options / config), majd kipipálva megjeleníteni az inline editort-t.
* Ennek a szövegmezőjébe kell beilleszteni az ezen a lapon, fent található Szószedet.txt teljes tartalmát – a file elején és végén található sok üres sor arra szolgál, hogy se beillesztés előtt, se után ne kelljen a tényleges szószedetet látni (a file-ra rámenve, raw-t kiválasztva már a teljes szöveg görgetés nélkül egyben kijelölhető, a fent csatolt videóban jól látszik)
* Ezek után import / ok / ok, és elvileg működik is a cenzúrázás, amit a felső ikonsorból egy csúszkával ki-be lehet kapcsolni.
* A „Test” menüpont szövegmezőjében ki lehet próbálni az egészet, de hogy ne kelljen ténylegesen olyan szavakon tesztelni, bekerült egy plusz szűrendő kifejezés: „cenzúraverzióteszt”-re a szószedet aktuális verziószámát írja ki.
* A kiszűrt, lecserélt szavakat [ ] közé rakja

Bejelentkezett / szinkronizáló Firefox-fiók esetén (bár elképzelhető hogy az addont külön szükséges telepíteni mobilra is) legutóbbi információim szerint az asztali gépen importált szószedet mobilon is frissül, de mivel ez erősen Firefox és az alapjául szolgáló (amúgy rendszeresen frissülő) cenzúra addon függvénye is, ezért ez nem feltétlenül garantált. Végső esetben az egész import folyamatot meg kell ismételni mobilon is, de a lépései teljesen megegyeznek az asztali változatéval. 

## Módosítás, fejlesztés, egyéb infók azoknak, akik nem csak használnák, de fejlesztenék is a szószedetet
* A szószedet természetesen szabadon felhasználható, módosítható, testre szabható – némi RegEx ismeret szükséges hozzá.
* Új szavak hozzáadása, vagy a meglévők szerkesztése az alábbi, nem túl bonyolult sorok szerkesztésével, vagy a megfelelő helyre történő beillesztésével történhet:
```
"lecserélendő szó": {
	      "matchMethod": 4,
	      "repeat": false,
	      "sub": "helyettesítő szó"
	    },
```
* Amennyiben valaki érdemben hozzátesz a listához, örömmel és köszönettel veszem, ha githubon is feltölti.
* A szószedet maga próbál a RegEx és a magyar nyelvtan útvesztőjéből valami értelmeset kihozni: pár kiszűrendő szótő után külön definiálja a kivételeket, amik helyére szinonimákat helyeztem be. Sajnos maga a lista jelen formájában nincs szépen sorrendbe rakva, a fejlesztés közben inkább toldozott-foltozott sorrendben kerültek be a szavak, különösen, hogy sokszor ékezetes és ékezet nélküli változatokkal is szerepelnek, de az ékezet nélküli változatoknál teljesen más kivételeket kellett visszahozni.
* A kivételeket a magyar webkorpusz (http://mokk.bme.hu/resources/webcorpus/) 100.000 leggyakrabban előforduló magyar szavának listájából raktam össze, relative jó szűrésnek tartom, de elméletben lehetséges lenne a teljes (589.000.000+ szavas) szűrt szószedet feldolgozása is, bár nem praktikus, mégpedig:
* A szószedet szerkesztésénél nem árt figyelni arra, hogy minél hosszabb, annál lassabban fut le, extrém esetekben elég szignifikáns késést okozva a lapok betöltésében – a kivételek, valamint ékezetes és ékezet nélküli változataik hozzáadását ezért is limitáltam le ahogy csak tudtam.