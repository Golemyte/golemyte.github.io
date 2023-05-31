<!DOCTYPE html>
<html>
<head>
  <title>Labo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      color: black;
      background-color: #f2f2f2;
      padding: 20px;
    }
    
    h1 {
      color: #333;
      font-size: 24px;
      margin-bottom: 10px;
    }
    
    h2 {
      color: #333;
      font-size: 18px;
      margin-bottom: 10px;
    }
    
    p {
      margin-bottom: 10px;
    }
    
    a {
      color: green;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <h1>Labo 1</h1>
  <p>
    IP: [UNIQUE]<br>
    PFS1:
    <ul>
      <li>-wan em0 192.168.254.133/24</li>
      <li>-LAN em1 172.28.10.1/24</li>
    </ul>
    PFS2:
    <ul>
      <li>-wan em0 192.168.254.134/24</li>
      <li>-LAN em1 172.28.20.1/24</li>
    </ul>
    CENTOS1: 172.28.10.15/24<br>
    CENTOS2: 172.28.20.15/24<br>
    win101: 172.28.10.25<br>
    win102: 172.28.20.25
  </p>

  <h2>Labo 2: Découverte de PFSENSE</h2>
  <p>
    Création de capture de trames depuis la console de PFSENSE.<br>
    Lien YouTube: <a href="https://youtu.be/Zwnr8gRzzEo?t=1198" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=1198</a>
  </p>

  <h2>Labo 3</h2>
  <p>
    /!\ Ne pas regarder l'approche "naive" ! /!\ <br>
    VLAN: création d'une VLAN<br>
    Ajouter le VLAN via Interfaces > Assignments et puis choisir l'onglet VLANs et cliquer sur Add.<br>
    Règle de block LAN11 to LAN et inversément: 19:59<br>
    Lien YouTube: <a href="https://youtu.be/Zwnr8gRzzEo?t=1198" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=1198</a>
  </p>

  <h2>Labo 4: VPN</h2>
  <p>
    Lien Utile: <a href="https://goopensource.fr/pfsense-vpn-site-a-site-en-ipsec/#:~:text=On%20débute%20notre%20configuration%20en,du%20WAN%20de%20votre%20PFSENSE2." target="_blank">https://goopensource.fr/pfsense-vpn-site-a-site-en-ipsec/#:~:text=On%20débute%20notre%20configuration%20en,du%20WAN%20de%20votre%20PFSENSE2.</a><br>
    Vidéo YouTube: <a href="https://www.youtube.com/watch?v=Gidg8a8ovew&ab_channel=Alphorm" target="_blank">https://www.youtube.com/watch?v=Gidg8a8ovew&ab_channel=Alphorm</a><br>
    Pour P1:<br>
    - Le remote gateway correspond au WAN de l'autre machine ! (ex. PF1 vers PF2 alors WAN de PF2)<br>
    Pour P2:<br>
    - Le remote network est le LAN de PFSENSE 2 soit 172.28.20.0<br>
    Bien faire attention aux clés en P1 ! Si pas créé automatiquement, il faut refaire la même configuration de l'autre côté.<br>
    Règle de FW PFSENSE 1: 1h02'55" <a href="https://youtu.be/Zwnr8gRzzEo?t=3775" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=3775</a><br>
    Règle de FW PFSENSE 2: 1h03'24" <a href="https://youtu.be/Zwnr8gRzzEo?t=3804" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=3804</a><br>
    SSH de Centos 2 vers VLAN11: 1h05'25" <a href="https://youtu.be/Zwnr8gRzzEo?t=3925" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=3925</a><br>
    Règle autorisation d'ICMP: 1h16'37" <a href="https://youtu.be/Zwnr8gRzzEo?t=4597" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=4597</a><br>
    Ajout d'une règle qui permet d'interconnecter les "VLAN 10" également avec PFSENSE 2: 1h18'30" <a href="https://youtu.be/Zwnr8gRzzEo?t=4710" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=4710</a><br>
    Ajout d'un P2 autorisant ce trafic: 1h20' <a href="https://youtu.be/Zwnr8gRzzEo?t=4805" target="_blank">https://youtu.be/Zwnr8gRzzEo?t=4805</a><br>
    Donc step by step:<br>
    1) Ajouter une P2 dans IPsec des deux côtés (avec donc un changement de source ou de destination vers les VLAN 10)<br>
    2) Ajout de règles qui autorisent le trafic dans les deux sens dans les deux firewalls.
  </p>

  <h2>Labo 5: 1h22'15"</h2>
  <p>
    Mise en place d'un proxy:<br>
    Vérifier HAProxy dans Systeme > Package Manager > HAProxy reload.<br>
    Mettre les certificats en place dans System > Certificat > Manager CAs puis Certificat.<br>
    Mettre en place le backend:<br>
    - Service > HAProxy > Backend<br>
    - Nom: [mon_backend]<br>
    - Dans la server_list, ajouter un élément:<br>
      - Mode active, name, address [de la machine avec le site web], port [80].<br>
    Frontend:<br>
    - Nom<br>
    - External address: WAN IPV4, port 443 [si HTTPS], SSL offloading [TRUE].<br>
    Dans Default Backend, Access Control Lists and Actions:<br>
    - Access Control List:<br>
      - Nom: Value [lien du site web [ssl-254-134.labo.swilabus.xyz]]<br>
    - Actions: Use backend see below ma_config backend: mon_backend<br>
    De retour dans HAProxy:<br>
    - "Enable proxy", préciser le nombre maximal de connexions, SSL DH [2048].<br>
    Règle du FW:<br>
    - WAN: Pas IPV4TCP source: any, dest: this FW HTTPS<br>
    - LAN: Tout trafic venant de WAN vers LAN et inversément du serveur web [IPV4TCP Centos vers PFsense WAN, port HTTP].
  </p>
  </img src"wanPFSENSE1rule.png" alt="rulespfs1wan"
</body>
</html>
