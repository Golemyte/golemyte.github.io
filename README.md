<!DOCTYPE html>
<html>
<head>
  <title>Testing</title>
  <style>
    body {
      background-color: black;
      color: gray;
    }
  </style>
</head>
<body>
  <h1>Testing</h1>
  <p> Labo 1

IP : [UNIQUE]
PFS1:-wan em0 192.168.254.133/24
     -LAN em1 172.28.10.1/24
PFS2:-wan em0 192.168.254.134/24
     - LAN em1 172.28.20.1/24


CENTOS1 : 172.28.10.15/24
CENTOS2 : 172.28.20.15/24

win101 : 172.28.10.25
win102 : 172.28.20.25





labo 2 : découverte de PFSENSE
création de capture de trammes depuis la console de pfsense.


Labo 3. 
/!\ ne pas regarder l'approche "naive" ! /!\

VLAN
création d'une VLAN :
Ajouter le VLAN via Interfaces > Assignments et puis choisir l’onglet VLANs et cliquer sur Add.
règle de block LAN11 to LAN et inversément: 19:59
https://youtu.be/Zwnr8gRzzEo?t=1198

window : modifier le port vlan:
net properties> configure> VLAN ID

labo4 
VPN
https://goopensource.fr/pfsense-vpn-site-a-site-en-ipsec/#:~:text=On%20débute%20notre%20configuration%20en,du%20WAN%20de%20votre%20PFSENSE2.
https://www.youtube.com/watch?v=Gidg8a8ovew&ab_channel=Alphorm

pour P1
le remote gateway correspond au WAN de l'autre machine !
(ex pf1 vers PF2 alors WANde PF2)
pour P2: le remote network est 
le LAN de PFSENSE 2 soit 172.28.20.0

bien faire gaffe au clé en P1 ! si pas créé automatiquement, il faut refaire la même config  de l'autre côté.

règle de FW pfsense 1 :1h02'55" https://youtu.be/Zwnr8gRzzEo?t=3775
règle de FW pfsense 2 :1h03'24" https://youtu.be/Zwnr8gRzzEo?t=3804

ssh de centos 2 vers VLAN11 : 1h05'25" https://youtu.be/Zwnr8gRzzEo?t=3925
(donc win10-1 qui contacte centos2 via SSH hein)

règle autorisation d'ICMP : 1h16'37" https://youtu.be/Zwnr8gRzzEo?t=4597

ajout d'une règle qui permet d'interconnecter les "vlan 10" également avec pfsense2 : 1h18'30" https://youtu.be/Zwnr8gRzzEo?t=4710

ajout d"un p2 autorisant ce trafic : 1h20 : https://youtu.be/Zwnr8gRzzEo?t=4805
donc step by step : 
1)ajouer une P2 dasn ipsec des deux côté (avec ducoup un changement de src ou de dest vers les vlan10)
2)ajout de rules qui autorise le trafic dans les deux sans dans les deux FW.

Labo 5: 1h22'15"


</p>
</body>
</html>
