# Segurtasuna — TungTunning

> **Enpresa:** TungTunning (tuning tailerra) · **Taldea:** 3. taldea
> **Edukia:** sarbide fisikoa, kontingentzia-plana, pasahitz-politika, sarearen diseinua, suebakia, HTTPS, IDS eta VPN.
> **Araua:** egin, dokumentatu eta justifikatu; dokumentazioak benetako konfigurazioarekin bat etorri behar du.

---

## 1. Sarearen diseinua (LAN / WAN / DMZ)

TungTunningen sarea `192.168.10.0/24` azpisarean dago, **pfSense** suebakiaren atzean.

```
Sarea (LAN):  192.168.10.0/24
Gateway/FW:   pfSense  —  LAN 192.168.10.254  /  WAN 192.168.123.1/22
DNS/DHCP/AD:  192.168.10.1 (Windows Server)
```

| Gunea | Deskribapena | Adibideak |
|-------|--------------|-----------|
| **WAN** | Kanpo-sarea (Internet) | pfSense WAN `192.168.123.1/22` |
| **LAN** | Barne-sarea (lanpostuak, zerbitzaria) | Windows Server `.1`, bezeroak `.100`–`.161` |
| **DMZ** *(gomendioa)* | Kanporako zerbitzuak isolatzeko | Web `.21`, Jitsi `.5` |

**Justifikazioa:** pfSensek LAN eta WAN banatzen ditu, eta barne-zerbitzuak babesten. Kanpora begira dauden zerbitzuak (web, Jitsi) **DMZ** batean jartzea gomendatzen da, LANetik isolatzeko: erasotzaile batek zerbitzu publiko bat hausten badu, ez du barne-sarera sarbide zuzenik izango.

<!-- Argazkia: sarearen diseinua (LAN/WAN/DMZ), izen, IP eta zerbitzuekin. -->
![](irudiak/seg-01-argazkia.png)


---

## 2. Suebakia (pfSense)

Sareko suebakia **pfSense** da (`192.168.10.254`), router eta firewall lanak egiten dituena.

- **Kokapena:** LAN eta WAN artean, sarbide-puntu nagusian.
- **LAN DHCP desaktibatuta:** DHCP zerbitzua Windows Serverrek ematen du (gatazkak saihesteko).
- **Arau-irizpideak:** beharrezko atakak soilik ireki (printzipioa: dena ukatu, behar dena baimendu).

Dokumentatu beharreko arau nagusiak (atakak):

| Zerbitzua | Ataka | Protokoloa |
|-----------|-------|------------|
| DNS | 53 | UDP/TCP |
| DHCP | 67/68 | UDP |
| HTTP/HTTPS (web) | 80/443 | TCP |
| Jitsi (web + media) | 443 / 10000 | TCP / UDP |
| Inprimaketa (IPP) | 631 | TCP |

<!-- Argazkia: pfSenseko suebaki-arauak (izena, IP, atakak), % 100 zuzen eta funtzionamenduan. -->
![](irudiak/seg-02-argazkia.png)


---

## 3. HTTPS

- **Jitsi:** `https://jitsi.tuning.eus` HTTPS bidez dabil, **ziurtagiri autosinatuarekin** (nabigatzaileak "Ez da segurua" erakusten du; barne-erabilerarako onargarria).
- **Web-zerbitzaria:** HTTPS gaitzea gomendatzen da ziurtagiri batekin (barne-CA edo Let's Encrypt), komunikazioak zifratzeko.

**Justifikazioa:** HTTPSk bezeroaren eta zerbitzariaren arteko trafikoa zifratzen du, kredentzialak eta datuak bidean atzitzea saihestuz.

<!-- Argazkia: HTTPS giltzarrapoa nabigatzailean (Jitsi/web). -->
![](irudiak/seg-03-argazkia.png)


---

## 4. Sarbide fisikoa

Instalazioak gune hauetan banatzen dira, sarbide-maila ezberdinekin:

| Gunea | Sarbide-maila | Nork |
|-------|---------------|------|
| Harrera / Bezeroari arreta | Publikoa | Bezeroak eta langileak |
| Tailerra | Mugatua | Tailerreko langileak + IT |
| Bulegoak (Admin/Logistika) | Mugatua | Dagokion saila + IT |
| Ekipo-gela (zerbitzaria) | Murriztua | **IT soilik** |

**Kontrol-sistemak:** gune mugatu/murriztuetan **hurbiltze-txartel (RFID)** edo **PIN teklatua**. Sarbideak erregistratuta.

**Biometria — erabakia:** lehen fasean **ez da biometriarik instalatuko**. Enpresa txikia da eta txartel + PIN konbinazioak (dakizuna + duzuna) nahikoa segurtasun ematen du ekipo-gelarako. Biometria baten kostua (irakurgailuak, softwarea, mantentzea) ez dago justifikatuta egungo tamainarako.

**Neurri osagarriak:** ekipo-gela giltzapean, su-itzalgailua gertu, SAI (UPS), CCTV sarreran, lanpostuen blokeo automatikoa (GPO bidez).

<!-- Planoa: sarbide-kontroleko puntuak (txartel/PIN), kamerak, larrialdietako irteerak eta su-itzalgailuak. -->
![](irudiak/seg-04-planoa.png)


---

## 5. Pasahitz-politika

Pasahitz guztiek bete beharreko gutxienekoak:

| Irizpidea | Eskakizuna |
|-----------|-----------|
| Gutxieneko luzera | 12 karaktere (administratzaileentzat 14) |
| Letra larriak / xeheak | Gutxienez bana |
| Zenbakiak | Gutxienez bat |
| Karaktere bereziak | Gutxienez bat |
| Debekatuta | Erabiltzaile-izena, enpresa-izena, data pertsonalak, hiztegiko hitzak |

**Kudeaketa-arauak:** 90 eguneko iraungitzea (administratzaileak 60), azken 5 pasahitzak ez berrerabili, 5 saiakera oker ondoren blokeoa, pasahitzak ez partekatu/idatzi.

**Ezarpena:** politika hau **Active Directoryko GPO baten bidez** teknikoki aplikatzen da (konplexutasuna, luzera, historia eta blokeoa automatikoki), giza akatsen mende utzi gabe.

**Justifikazioa:** luzerari garrantzia (NIST/INCIBE gomendioak), aukeren espazioa handitzea, lapurtutako pasahitzen baliozkotasun-leihoa mugatzea eta indar gordineko erasoak geldiaraztea.

<!-- Argazkia: pasahitz-politikaren GPOa (Default Domain Policy → Password Policy). -->
![](irudiak/seg-05-argazkia.png)


---

## 6. Kontingentzia-plana

### 6.1. Aktibo kritikoak

| Aktiboa | Garrantzia |
|---------|-----------|
| Windows Server (AD/DNS/DHCP) | Kritikoa — zerbitzu guztien oinarria |
| Fitxategi partekatuak | Kritikoa — sailetako datuak |
| Datu-baseak (MySQL/MongoDB) | Kritikoa — datu pertsonalak (DBEO) |
| Backup-ak | Kritikoa — berreskurapenaren oinarria |
| pfSense / sareko ekipoak | Altua — konektibitatea |

### 6.2. Arrisku-kasuak eta neurriak

- **Zerbitzariaren matxura:** RAID diskoetan, SAI (UPS), backup-etatik berreskuratzea.
- **Datuen galera:** backup-politika (3-2-1 araua: 3 kopia, 2 euskarri, 1 kanpoan), aldizkako berreskuratze-probak.
- **Malware/ransomware:** antibirusa, eguneratzeak, lineaz kanpoko backup-ak, erabiltzaileen prestakuntza.
- **Baimenik gabeko sarbidea:** NTFS baimenak, pasahitz sendoak, suebakia, log-en jarraipena.
- **Elikadura-etena:** SAI (UPS), itzaltze kontrolatua, ordena egokian berrabiaraztea (lehenik AD/DNS).

### 6.3. Backup-politika

| Maiztasuna | Mota | Ordua |
|-----------|------|-------|
| Egunero (astelehen-ostiral) | Inkrementala | 22:00 |
| Astean behin (larunbata) | Osoa | 02:00 |
| Hilean behin | Isolatua (off-site / cloud) | Azken igandean |

Atxikipena: eguneroko kopiak 30 egun, asteko kopiak 3 hilabete.

<!-- Argazkia (gomendioa): aktiboen azterketa PILAR edo INCIBEren tresnarekin (txostena erantsi). -->
![](irudiak/seg-06-argazkia.png)


---

## 7. IDS (intrusioak detektatzeko sistema)

Intrusioak detektatzeko, **Snort** edo **Suricata** instalatzea gomendatzen da (pfSensek Snort/Suricata paketeak onartzen ditu).

- **Kokapena:** sarearen sarrera-puntuan (pfSensen), trafiko guztia aztertzeko.
- **Funtzioa:** patroi ezagunak (sinadurak) detektatu eta alertak sortu.

<!-- Argazkia: IDS softwarea instalatuta eta funtzionamenduan (alertak), justifikazioarekin. -->
![](irudiak/seg-07-argazkia.png)


---

## 8. VPN (urruneko sarbidea)

Urrunetik konektatzeko, pfSensek **OpenVPN** edo **WireGuard** onartzen ditu.

**Aukeren analisia:**
- **OpenVPN:** oso hedatua, segurua, bateragarritasun handia.
- **WireGuard:** modernoa, azkarra, konfigurazio sinpleagoa.

**Erabakia eta justifikazioa:** barne-sarera modu seguruan sartzeko, VPN bat ezartzea gomendatzen da pfSensen, trafikoa zifratuz Internet bidez. Horrela IT sailak urrunetik kudea dezake sarea, zerbitzuak Internetera zuzenean ireki gabe.

<!-- Argazkia: VPNaren konfigurazioa pfSensen eta konexio-froga. -->
![](irudiak/seg-08-argazkia.png)


---

## 9. Laburpena

- [x] Sarearen diseinua (LAN/WAN, pfSense)
- [x] Suebakia (pfSense) — arauak dokumentatu beharrekoak
- [x] HTTPS (Jitsi autosinatua)
- [x] Sarbide fisikoaren politika (biometria justifikatuta baztertua)
- [x] Pasahitz-politika (GPO bidez)
- [x] Kontingentzia-plana + backup-politika
- [ ] DMZ zehaztea (gomendioa)
- [ ] IDS (Snort/Suricata) instalatu eta frogatu
- [ ] VPN ezarri eta frogatu
- [ ] Aktiboen azterketa PILAR/INCIBE tresnarekin

---

*TungTunning · 3. taldea · Segurtasuna*
