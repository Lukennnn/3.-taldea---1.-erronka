---
permalink: /
title: Hasiera
---

<section class="hero">
  <p class="hero-kicker">1. Erronka · 3. taldea</p>
  <h1>Tung<span>Tunning</span></h1>
  <p>Bilboko tuning tailer baten informatika-azpiegitura diseinatu eta muntatu dugu: Windows Server domeinua, sare-zerbitzuak, birtualizazioa, pfSense suebakia, web aplikazioak, datu-baseak eta azpiegitura osoaren aurrekontua.</p>
  <div class="chips">
    <span class="chip hot">3taldea.lan</span>
    <span class="chip">Windows Server 2019</span>
    <span class="chip">Proxmox</span>
    <span class="chip">pfSense</span>
    <span class="chip">WordPress</span>
    <span class="chip">GLPI</span>
    <span class="chip">Jitsi Meet</span>
    <span class="chip">CUPS</span>
  </div>
</section>

<section class="home-section">
  <div class="facts">
    <div class="fact"><small>Sarea</small><strong>192.168.10.0/24</strong></div>
    <div class="fact"><small>Domeinua</small><strong>3taldea.lan</strong></div>
    <div class="fact"><small>Atebidea</small><strong>192.168.10.254</strong></div>
    <div class="fact"><small>DNS / DHCP</small><strong>192.168.10.1</strong></div>
  </div>
</section>

<section class="home-section">
  <h2>Dokumentazioa</h2>
  <div class="cards">
    <a class="card" href="{{ '/1-wae.html' | relative_url }}"><span class="card-code">WAE</span><span class="card-title">Web Aplikazioak</span><span class="card-desc">WordPress enpresa-ataria eta GLPI txartel- eta inbentario-sistema.</span></a>
    <a class="card" href="{{ '/2-sistema-eragileak.html' | relative_url }}"><span class="card-code">SEA</span><span class="card-title">Sistema Eragileak</span><span class="card-desc">Active Directory, OUak, GPOak, karpeta partekatuak eta inprimaketa.</span></a>
    <a class="card" href="{{ '/3-sare-zerbitzuak.html' | relative_url }}"><span class="card-code">SZI</span><span class="card-title">Sare Zerbitzuak</span><span class="card-desc">DNS eremuak, DHCP eta Jitsi Meet audio eta bideo zerbitzua.</span></a>
    <a class="card" href="{{ '/4-sistema-banatuak.html' | relative_url }}"><span class="card-code">SB</span><span class="card-title">Sistema Banatuak</span><span class="card-desc">Birtualizazioa, makina birtualak, edukiontziak eta erabilgarritasun handia.</span></a>
    <a class="card" href="{{ '/5-datu-baseak.html' | relative_url }}"><span class="card-code">DB</span><span class="card-title">Datu-baseak</span><span class="card-desc">MySQL/MariaDB eta MongoDB: instalazioa, erabiltzaileak eta baimenak.</span></a>
    <a class="card" href="{{ '/6-segurtasuna.html' | relative_url }}"><span class="card-code">SEG</span><span class="card-title">Segurtasuna</span><span class="card-desc">pfSense, LAN/WAN/DMZ, pasahitz-politika, kontingentzia-plana, IDS eta VPN.</span></a>
    <a class="card" href="{{ '/7-hardware.html' | relative_url }}"><span class="card-code">HW</span><span class="card-title">Hardwarea</span><span class="card-desc">Lanpostuen ekipamendua, aurrekontua, osagaiak eta tailerraren planoa.</span></a>
    <a class="card" href="{{ '/8-jasangarritasuna.html' | relative_url }}"><span class="card-code">IRAU</span><span class="card-title">Jasangarritasuna</span><span class="card-desc">ESG plana: ingurumena, gizartea eta gobernantza, GJHekin lotuta.</span></a>
  </div>
</section>

<section class="home-section">
  <h2>Sarearen eskema</h2>
  <div class="diagram"><img src="{{ '/irudiak/sare-eskema.svg' | relative_url }}" alt="TungTunning sarearen eskema: Internet, router, Proxmox zerbitzaria, pfSense eta zerbitzuak"></div>
</section>

<section class="home-section">
  <h2>Azpiegitura laburki</h2>
  <table>
    <thead><tr><th>Makina</th><th>Sistema</th><th>Funtzioa</th><th>IP helbidea</th></tr></thead>
    <tbody>
      <tr><td>SERVER_ERRONKA</td><td>Windows Server 2019</td><td>AD DS, DNS, DHCP, fitxategiak eta inprimaketa</td><td><code>192.168.10.1</code></td></tr>
      <tr><td>JITSI_ERRONKA</td><td>Ubuntu 24.04</td><td>Jitsi Meet (jitsi.tuning.eus)</td><td><code>192.168.10.5</code></td></tr>
      <tr><td>CUPS_ERRONKA</td><td>Ubuntu 20.04</td><td>Inprimaketa-zerbitzaria (CUPS)</td><td><code>192.168.10.67</code></td></tr>
      <tr><td>WINDOWS_ERRONKA_BEZ1</td><td>Windows 11</td><td>Bezero Windows</td><td><code>192.168.10.101</code></td></tr>
      <tr><td>WINDOWS_ERRONKA_BEZ2</td><td>Windows 11</td><td>Bezeroa, domeinuan sartua (DHCP)</td><td><code>192.168.10.161</code></td></tr>
      <tr><td>BEZEROA_ERRONKA_UBUNTU</td><td>Ubuntu 20.04</td><td>Bezero Linux (DHCP)</td><td><code>192.168.10.100</code></td></tr>
      <tr><td>pfSense SISA</td><td>pfSense</td><td>Router / suebakia</td><td><code>192.168.10.254</code></td></tr>
    </tbody>
  </table>
</section>

<section class="home-section">
  <h2>Taldea</h2>
  <div class="team">
    <div class="member"><span class="avatar">A</span><span><b>Asier Larrañaga</b><small>3. taldea</small></span></div>
    <div class="member"><span class="avatar">E</span><span><b>Enol Naveran</b><small>3. taldea</small></span></div>
    <div class="member"><span class="avatar">L</span><span><b>Luken Pagaldai</b><small>3. taldea</small></span></div>
  </div>
</section>
