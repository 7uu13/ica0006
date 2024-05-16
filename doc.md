# **Ceph & Proxmox HA Cluster Dokumentatsioon**

Sisukorra vark siia ka

# **1. Sissejuhatus**

## **1.1 Ressursid**
| Ilo             | Serverid        | Virtukas       | Pordid |
|-----------------|-----------------|----------------|--------|
| 192.168.161.107 | 192.168.161.117 | 192.168.180.57 | :8006  |
| 192.168.161.108 | 192.168.161.118 |                | :8006  |
| 192.168.161.109 | 192.168.161.119 |                | :8006  |

Masinates on kasutatud kasutaja/salasõna: student/student1234
Proxmoxi webiliidedes on kasutatud kasutaja/salasõna: root/student1234
Ceph Dashboard on kasutatud kasutaja/salasõna: student/student1234

# **2. Ettevalmistus**

- ## **2.1 Ilo konsoolide kaudu toimetamine**
    Kuna masinatel operatsioonisüsteem kui selline on puudulik, siis tuleb see paigaldada Ilo kaudu. Ilole ligipaasuga tekkis nii moningaid probleeme, kuid kui Internet Exploreil muuta TLS ja SSl sateid, said ilole holpsasti ligi.

    ![alt text](image.png)
- ## **2.2 RAID-i seadistamine**
    Cephile raidi pandud kettad ei meeldi, aga kuna meile on antud neli ketast ning peamiseks ulesandeks on korgkaideldavuse saavutamine, siis otsustasime panna kaks ketast raid 1+0-i (Mis sisuliselt tahendab seda, et kui on antud kaks ketast, rakendub RAID1 ning kui on antud 4 ketast, rakendub RAID10) ning ulejaanud kaks viskame Cephi pooli.
    RAID editorisse HP Ilo 3-es paaseb vajutades F8 booti ajal.
    ![alt text](G7.png)

# **3. Proxmox**
 [Proxmox](https://www.proxmox.com/en/downloads/proxmox-virtual-environment/iso/proxmox-ve-8-2-iso-installer) on võimas avatud lähtekoodiga platvorm virtualiseerimiseks ja konteineriseerimiseks, pakkudes kasutajasõbralikku liidest ja tugevaid funktsioone virtuaalmasinate ja konteinerite haldamiseks andmekeskuse keskkondades.

 - ## **3.1 Proxmoxi paigaldamine Ilo kaudu**

 Ilo kaudu Proxmoxi paigaldamisel oli suurimaks probleemiks kaunis 640x460 resolutsioon, kuid me ei lasknud sel end hairida. Lahtusime taktikast nimega Tab and Pray.
 ![alt text](image-1.png)

 - ## **3.2 Proxmoxi klastri seadistamine**
 Proxmoxis endis loodud node-ide klasterdamine on vaga lihtsaks tehud. Klastri saavutamiseks lahtusime (siia mingi yt link w doc)

 # **4. CEPHi seadistamine**
 Kui Proxmox klaster on töökorras, saab hakata CEPH-i süsteemi lisama. Enamus tööks vajalik on Proxmox kasutajaliidesesse sisse ehitatud. Esmalt vali server, millest saab klastri esmane juht. Kõige esimesena tuleb CEPH paigaldada just sellele serverile. (see tekst muuta ofc)

 CEPHi installimiseks ja seadistamiseks lahtusime [sellest videost](https://youtu.be/Eli3uYzgC8A?si=UxcwtEphKkAw-hzF)

 ## **5. Apache2 lxc seadistus**

- ## **5.1 Ubuntu 22.04 Lxc loomine**
Node-ile tuleb anda hostname ning juure kontole lisada ka parool

![alt text](image-2.png)

Seejarel valime vastava iso

![alt text](image-3.png)

Storage-iks tuleb valida 3 node-i uhine pool, muidu ei ole auto failover voimalik

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)

Vorguseadmetes vaga palju muudatusi ei teinud. Hiljem aga andsime node-ile static ip.

![alt text](image-7.png)

![alt text](image-8.png)

Kui vastavad satted on valitud ning oled nendega rahul, vajuta Finish nuppu.

![alt text](image-9.png)

 siia teskst, et luua apache2e jaoks lxc

 - ## **Apache2 Installatsioon ja Seadistus**

 Selle jaoks lahtusime Apache2 enda dokumentatsioonist. Selle leiad [siit](https://ubuntu.com/tutorials/install-and-configure-apache#1-overview)