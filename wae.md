# WAE — Web Aplikazioen Ezarpena — TungTunning

> **Enpresa:** TungTunning (tuning tailerra) · **Taldea:** 3. taldea
> **Edukia:** WordPress (enpresaren web-ataria) eta GLPI (gertakari/txartel-sistema).
> **Azpiegitura:** web-zerbitzaria `192.168.10.21` (`www.tuning.eus`), XAMPP/Apache + MySQL/MariaDB gainean.
> **Araua:** egin, dokumentatu eta justifikatu; dokumentazioak benetako konfigurazioarekin bat etorri behar du.

---

## 1. Sarrera

TungTunning enpresak bi web-aplikazio ditu, biak web-zerbitzari berean (`192.168.10.21`, `www.tuning.eus`), XAMPP ingurunean (Apache + MySQL/MariaDB):

- **WordPress** — enpresaren web-ataria / barne-ataria (CMS).
- **GLPI** — gertakarien eta txartelen (ticket) kudeaketa-sistema.

Datu-basea MySQL/MariaDB da (GLPIk `glpi_user` erabiltzailea du; ikus *Datu-baseak* dokumentua).

---

## 2. WordPress

### 2.1. Erabilera eta CMSaren funtzionalitateak

WordPress CMSa aukeratu da enpresaren weba sortzeko. Dokumentatu behar da **webak izango duen erabileraren eta CMSaren funtzionalitateen arteko lotura**: adibidez, zerbitzuen aurkezpena, kontaktua, berriak/bloga, eta edukia modu errazean eguneratzeko aukera teknikaririk gabe.

### 2.2. Instalazioaren parametroak

Dokumentatu beharreko instalazio-parametroak:
- Web-zerbitzaria: Apache (XAMPP), `192.168.10.21` / `www.tuning.eus`.
- Datu-basea: MySQL/MariaDB, datu-base propioa WordPressentzat.
- Administrazio-URLa: `http://www.tuning.eus/wp-admin`.

<!-- Argazkia: WordPressen instalazioa / `wp-admin` panela, enpresaren domeinua barran. -->
![](irudiak/wae-01-argazkia.png)


### 2.3. Erabiltzaileak eta pribilegioak

Gutxienez **bi erabiltzaile** sortu behar dira, logikaz, eta bakoitzaren pribilegioak azaldu. Adibidez:

| Erabiltzailea | Rola | Pribilegioak |
|---------------|------|--------------|
| admin (IT) | Administratzailea | Kontrol osoa (plugin, itxura, erabiltzaileak) |
| editorea (Marketina) | Editorea | Edukia sortu eta argitaratu, baina ez konfiguraziorik aldatu |

<!-- Argazkia: erabiltzaileen zerrenda, bakoitza bere rolarekin. -->
![](irudiak/wae-02-argazkia.png)


### 2.4. Txantiloiak (plantillak)

Oinarrizkoak ez diren **hainbat txantiloi** probatu behar dira, probak argazkiekin dokumentatuz. Ondoren, azken diseinua haietako batekin egin eta **aukeraketa justifikatu** (zergatik txantiloi hori: diseinua, erantzukortasuna, pertsonalizazio-aukerak...).

<!-- Argazkia: probatutako txantiloiak (hainbat kaptura). -->
![](irudiak/wae-03-argazkia.png)

<!-- Argazkia: hautatutako azken txantiloia aplikatuta. -->
![](irudiak/wae-04-argazkia.png)


### 2.5. Diseinua eta CSS pertsonalizazioa

Diseinu logikoa eta pertsonalizatua egin behar da, **txantiloiaren CSSan aldaketak** eginez (koloreak, tipografia, logoa...). Dokumentatu diseinua, zergatia eta egindako CSS aldaketak.

<!-- Argazkia: CSS aldaketak (kodea) eta emaitza bisuala (aurretik/ondoren). -->
![](irudiak/wae-05-argazkia.png)


---

## 3. GLPI

### 3.1. Instalazioaren parametroak

GLPI web-zerbitzari berean instalatu da (Apache + MySQL/MariaDB). Datu-basean `glpi_user` erabiltzailea erabiltzen du. Dokumentatu: instalazio-URLa (`http://www.tuning.eus/glpi`), datu-basearen konexio-parametroak eta instalazio-pausoak.

<!-- Argazkia: GLPIren instalazioa / hasierako panela. -->
![](irudiak/wae-06-argazkia.png)


### 3.2. Erabiltzaileak eta rolak

Hainbat erabiltzaile sortu behar dira, **gutxienez bi rol desberdinekin** (adib. `super-admin` IT sailarentzat eta `technician`/`self-service` beste sailentzat).

<!-- Argazkia: erabiltzaileak beren rolekin. -->
![](irudiak/wae-07-argazkia.png)


### 3.3. Enpresako ekipoak erregistratuta

Enpresako ekipoak GLPIn erregistratu behar dira (inbentarioa): ordenagailuak, inprimagailuak, sareko gailuak... TungTunningeko ekipamendua (ikus *Hardwarea* dokumentua) kargatu daiteke.

<!-- Argazkia: erregistratutako ekipoen inbentarioa. -->
![](irudiak/wae-08-argazkia.png)


### 3.4. Txartelak (tickets)

Gertakari batzuk (tickets) sortu behar dira, sistemaren funtzionamendua erakusteko: adibidez, erabiltzaile batek arazo bat jakinarazten du eta IT sailak kudeatzen du.

<!-- Argazkia: sortutako txartelak eta haien egoera/esleipena. -->
![](irudiak/wae-09-argazkia.png)


---

## 4. Laburpena — egin beharrekoa / egindakoa

- [ ] WordPress: erabilera↔CMS lotura dokumentatua
- [ ] WordPress: 2+ erabiltzaile rolekin
- [ ] WordPress: txantiloi-probak + azken aukeraketa justifikatua
- [ ] WordPress: CSS pertsonalizazioa dokumentatua
- [ ] GLPI: instalazio-parametroak
- [ ] GLPI: 2+ rol
- [ ] GLPI: ekipoak erregistratuta
- [ ] GLPI: txartelak sortuta

> **Oharra:** atal hau benetako konfigurazioarekin osatu behar da. Argazkiak hartu zure WordPress eta GLPI instalazioetatik eta txertatu adierazitako lekuetan (`irudiak/wae/` karpetan).

---

*TungTunning · 3. taldea · WAE*
