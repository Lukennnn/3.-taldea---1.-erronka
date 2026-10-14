# Sistema Banatuak — TungTunning

> **Enpresa:** TungTunning (tuning tailerra) · **Taldea:** 3. taldea
> **Edukia:** sistema banatuaren beharra, birtualizazioa eta erabilgarritasun handia.
> **Araua:** egin, dokumentatu eta justifikatu; dokumentazioak benetako konfigurazioarekin bat etorri behar du.

---

## 1. Sistema banatuaren beharra (justifikazioa)

TungTunning enpresak zerbitzu bat baino gehiago behar ditu martxan aldi berean: domeinua (AD/DNS/DHCP), fitxategiak, inprimaketa, web-aplikazioak (WordPress, GLPI), datu-baseak eta bideo-deiak (Jitsi). Zerbitzu horiek guztiak **makina fisiko bakarrean** jartzeak arriskuak ditu:

- **Hutsegite-puntu bakarra (SPOF):** makina erortzen bada, dena erortzen da.
- **Baliabideen lehia:** zerbitzu guztiek hardware bera partekatzen dute.
- **Mantentze-zailtasuna:** zerbitzu bat eguneratzeak besteei eragin diezaieke.

Horregatik, **sistema banatu bat** erabiltzen da: zerbitzuak **makina birtual (VM) desberdinetan** banatuta daude, bakoitza isolatuta. Horrela, zerbitzu bat berrabiarazi edo eguneratu daiteke besteak ukitu gabe, eta karga banatuta dago.

---

## 2. Birtualizazio-tresna

TungTunningeko azpiegitura **IsardVDI** gainean dago (nabigatzailetik atzitzen diren mahaigain birtualak). Tresna horrek makina birtual guztiak kudeatzen ditu.

### Birtualizatutako makinak

| Makina (VM) | SE | IP | Zerbitzua |
|-------------|-----|-----|-----------|
| SERVER_ERRONKA | Windows Server 2019 | 192.168.10.1 | AD, DNS, DHCP, fitxategiak, inprimaketa |
| WINDOWS_ERRONKA_BEZ1 | Windows 11 | 192.168.10.101 | Bezeroa |
| WINDOWS_ERRONKA_BEZ2 | Windows 11 | 192.168.10.161 | Bezeroa (domeinuan) |
| CUPS_ERRONKA | Ubuntu 20.04 | 192.168.10.67 | Inprimaketa (CUPS) |
| BEZEROA_ERRONKA_UBUNTU | Ubuntu 20.04 | 192.168.10.100 | Bezero Linux |
| JITSI_ERRONKA | Ubuntu 24.04 | 192.168.10.5 | Jitsi (bideo-deiak) |
| pfSense SISA | pfSense | 192.168.10.254 | Router / suebakia |

**Sareak:** makina guztiak `192.168.10.0/24` sare berean daude, pfSense atebidearen atzean.

<!-- Argazkia: IsardVDI panela makina birtual guztiekin (izena, SE, IP, egoera). -->
![](irudiak/sb-01-argazkia.png)


---

## 3. Zerbitzuen banaketa: VM eta edukiontziak

Errubrikak zerbitzu bat **makina birtual batean** eta beste bat **edukiontzi (container) batean** egotea eskatzen du.

### 3.1. Makina birtualeko zerbitzua (eginda)

Zerbitzuak VM independenteetan daude (ikus goiko taula). Adibidez, **Jitsi** bere Ubuntu 24.04 makina birtualean dago (`192.168.10.5`), gainerako zerbitzuetatik isolatuta.

### 3.2. Edukiontziko zerbitzua (proposamena / egiteko)

Edukiontzi bat gehitzeko, **Docker** erabil daiteke VM baten barruan, zerbitzu bat edukiontzi gisa abiarazteko. Adibide errazak:

```bash
# Docker instalatu (Ubuntu)
sudo apt update && sudo apt install docker.io -y
sudo systemctl enable --now docker

# Adibidez, web-zerbitzu bat edukiontzian
sudo docker run -d --name web-nginx -p 8080:80 nginx
```

Horrela, zerbitzu bera **birtualizazio bidez** (VM) eta **edukiontzi bidez** (Docker) alderatu daiteke: edukiontzia arinagoa da (ez du SE oso bat), VM-a isolatuagoa.

<!-- Argazkia: edukiontzia martxan (`docker ps`) eta zerbitzua funtzionatzen. -->
![](irudiak/sb-02-argazkia.png)


---

## 4. Erabilgarritasun handia (High Availability)

Zerbitzuen erabilgarritasuna bermatzeko neurriak:

- **Birtualizazioa:** VM bat erortzen bada, beste makinek lanean jarraitzen dute.
- **Backup-ak:** VMen irudiak eta datuak aldizka kopiatzea (ikus *Segurtasuna* dokumentua: eguneroko inkrementala, asteko osoa).
- **SAI (UPS):** elikadura-etenaren aurrean, itzaltze kontrolatua.
- **Snapshot-ak:** aldaketa handi bat egin aurretik, VMaren egoera gordetzea, arazorik egonez gero atzera egiteko.

> **Oharra:** benetako erabilgarritasun handia (klusterrak, erredundantzia osoa) azpiegitura handiagoa eskatzen du. Enpresa honen tamainarako, birtualizazioa + backup-ak + snapshot-ak dira neurri egokiak eta justifikatuak.

---

## 5. Laburpena

- [x] Sistema banatuaren beharra justifikatua
- [x] Birtualizazio-tresna (IsardVDI) eta makinak dokumentatuta
- [x] Zerbitzua VM independentean (adib. Jitsi)
- [ ] Zerbitzua edukiontzian (Docker) — egiteko
- [x] Erabilgarritasun-neurriak (backup, SAI, snapshot)

---

*TungTunning · 3. taldea · Sistema Banatuak*
