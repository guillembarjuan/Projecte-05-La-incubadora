# Anàlisi de Vulnerabilitats amb OpenVAS

Aquesta guia explica el procés de configuració i inici de l'entorn per realitzar una anàlisi de vulnerabilitats utilitzant **OpenVAS** com a eina d'escaneig i **Metasploitable Linux** com a sistema objectiu amb vulnerabilitats conegudes.

---

## 1. Preparació de l'entorn virtual

### 1.1 Estat de les màquines virtuals a VirtualBox

![Llistat de màquines virtuals a VirtualBox](/T09/img_t09/captura1.png)

Es veuen dues màquines virtuals importades i aturades:
- **metasploitable-linux**: Sistema vulnerable amb diverses serves configurats.
- **OPENVAS-FREE-24.10.9-VirtualBox**: Eina d'escaneig de vulnerabilitats Greenbone/OpenVAS.

Amdues estan configurades per a arquitectura **x64** i amb **VirtualBox 2.6**.

---

## 2. Configuració de la màquina objectiu (Metasploitable)

### 2.1 Configuració de xarxa

![Configuració de xarxa de Metasploitable](/T09/img_t09/captura2.png)

A la configuració de xarxa de Metasploitable s'ha habilitat l'**Adaptador 1** amb les següents opcions:
- **Connectat a**: Xarxa NAT
- **Nom**: NatNetwork
- **Tipus d'adaptador**: Intel PRO/1000 MT Desktop (82540EM)
- **Mode promiscu**: Denega
- **Adreça MAC**: 08002738DAD8
- **Cable connectat**: Sí

Aquesta configuració permet que la màquina tingui accés a Internet i es comuniqui amb altres màquines en la mateixa xarxa NAT, inclosa la màquina OpenVAS.

---

## 3. Configuració de la màquina d'escaneig (OpenVAS)

### 3.1 Configuració de xarxa – Adaptador 1 (NAT)

![Configuració de xarxa de OpenVAS - Adaptador 1](/T09/img_t09/captura3.png)

L'**Adaptador 1** d'OpenVAS està configurat per a:
- **Connectat a**: Xarxa NAT
- **Nom**: NatNetwork
- **Tipus d'adaptador**: Intel PRO/1000 MT Desktop (82540EM)
- **Mode promiscu**: Permet-ho tot
- **Adreça MAC**: 080027F52341
- **Cable connectat**: Sí

Aquesta interfície permet a OpenVAS tenir connectivitat a Internet (per actualitzacions) i comunicar-se amb la màquina objectiu (Metasploitable) que comparteix la mateixa xarxa NAT.

### 3.2 Configuració de xarxa – Adaptador 2 (Només amfitrió)

![Configuració de xarxa de OpenVAS - Adaptador 2](/T09/img_t09/captura4.png)

L'**Adaptador 2** està configurat en mode **Adaptador de només l'amfitrió**:
- **Connectat a**: Adaptador de només l'amfitrió
- **Nom**: VirtualBox Host-Only Ethernet Adapter
- **Tipus d'adaptador**: Intel PRO/1000 MT Desktop (82540EM)
- **Mode promiscu**: Denega
- **Adreça MAC**: 080027712838
- **Cable connectat**: Sí

Aquesta configuració permet que l'equip físic (host) pugui accedir a la interfície web d'OpenVAS a través d'una IP en la xarxa host-only.

---

## 4. Inici de la màquina objectiu (Metasploitable)

### 4.1 Procés d'arrencada

![Inici de serveis a Metasploitable](/T09/img_t09/captura5.png)

En iniciar la màquina es carreguen diversos serveis, entre ells:
- **Tomcat**
- **Apache2**
- **Scheduler (atd)**

Apareix una advertència important: **"Warning: Never expose this VM to an untrusted network!"**, ja que aquesta màquina conté serveis deliberadament vulnerables.

Es mostra la pantalla de login amb les credencials per defecte:
- **Usuari**: msfadmin
- **Contrasenya**: msfadmin

### 4.2 Obtenció de la IP assignada

![Terminal de Metasploitable amb la comanda ip a](/T09/img_t09/captura6.png)

Després d'iniciar sessió, s'executa la comanda `ip a` per veure la configuració de xarxa:

- **eth0**: té assignada la IP `10.0.2.19/24` en la xarxa NAT.
- **Adreça MAC**: 08:00:27:38:d4:b8

Aquesta IP (`10.0.2.19`) serà l'objectiu de l'escaneig de vulnerabilitats.

---

## 5. Inici de la màquina d'escaneig (OpenVAS)

### 5.1 Pantalla d'inicialització

![Pantalla d'inici d'OpenVAS](/T09/img_t09/captura7.png)

En arrencar OpenVAS, es mostra una pantalla de login a la consola amb el missatge:

**"The web interface is available at: http://10.0.2.20"**

Aquesta IP (`10.0.2.20`) és l'adreça assignada a l'adaptador NAT (eth0) des d'on OpenVAS realitzarà l'escaneig a la màquina objectiu (`10.0.2.19`).

Les credencials per defecte per a la consola són:
- **Usuari**: admin
- **Contrasenya**: admin

### 5.2 Assistents de configuració inicial

![Assistent de configuració inicial](/T09/img_t09/captura8.png)

En accedir a la interfície web (des de l'equip host via la IP host-only), es mostra un **Setup Wizard** que pregunta si es vol completar la configuració inicial.

Aquest assistent guiarà en la configuració bàsica de l'aparell Greenbone.

---

## 6. Configuració inicial d'OpenVAS via web

### 6.1 Creació de l'usuari administrador

![Creació d'usuari administrador](/T09/img_t09/captura10.png)

Dins del setup wizard, el primer pas és crear un **usuari administrador global** per a la interfície web.

En aquest exemple es configura:
- **Account name**: usauri
- **Account password**: (introduït)
- **Account password confirmation**: (introduït)

Aquest usuari s'utilitzarà per accedir a la interfície web d'OpenVAS i gestionar escanejats.

### 6.2 Gestió de la llicència de Greenbone Feed

![Gestió de la llicència del feed](/T09/img_t09/captura11.png)

OpenVAS demana una **clau de subscripció per al Greenbone Enterprise Feed**. Es pot:
- **Introduir una clau** (si es té una llicència).
- **Ometre (Skip)** i utilitzar el **Greenbone Community Feed**.

El feed comunitari té menys actualitzacions que l'empresarial, però és suficient per a l'aprenentatge i proves inicials.

### 6.3 Comprovació de l'estat del feed

![Comprovació de l'estat del feed](/T09/img_t09/captura12.png)

Es mostra un avís de **Selfcheck** que indica que el feed té més de 10 dies. És recomanable actualitzar-lo des del menú **Feed** per obtenir les dades de vulnerabilitats més recents.

---

## 7. Navegació per la interfície d'OpenVAS

### 7.1 Menú principal

![Menú principal d'OpenVAS](/T09/img_t09/captura13.png)

El menú principal ofereix quatre opcions:
1. **Setup**: Configurar l'aparell Greenbone.
2. **Maintenance**: Accions de manteniment.
3. **Advanced**: Gestió avançada.
4. **About**: Informació sobre l'aparell.

### 7.2 Menú de configuració (Setup)

![Menú de configuració](/T09/img_t09/captura14.png)

Dins de **Setup** hi ha diverses categories:
- **User**: Gestió d'usuaris i contrasenyes.
- **Network**: Configuració de xarxa.
- **Services**: Serveis remots disponibles.
- **Feed**: Gestió del feed de Greenbone.
- **Keyboard**: Selecció de distribució de teclat.
- **Time**: Temps de manteniment.

### 7.3 Configuració de xarxa

![Menú de xarxa](/T09/img_t09/captura15.png)

A la secció **Network** es poden configurar:
- **Interfaces**: Configurar les interfícies de xarxa.
- **DNS**: Servidors de noms de domini.
- **Global Gateway**: Configuració de gateway per IPv4 i IPv6.
- **MAC**: Visualització d'adreces MAC.
- **IP**: Visualització d'adreces IP.

### 7.4 Selecció d'interfície a configurar

![Selecció d'interfície](/T09/img_t09/captura16.png)

Es tria quina interfície configurar:
- **Configure Interface eth0**
- **Configure Interface eth1**

### 7.5 Configuració d'eth0 (NAT)

![Configuració d'eth0](/T09/img_t09/captura17.png)

L'**eth0** està configurat amb:
- **IPv4**: enabled
- **DHCP**: enabled (obté IP automàticament de la xarxa NAT)
- **IPv6**: disabled

Aquesta és la interfície que comunica amb la màquina objectiu i Internet.

### 7.6 Configuració d'eth1 (Host-Only)

![Configuració d'eth1](/T09/img_t09/captura18.png)

![Detall de configuració d'eth1](/T09/img_t09/captura19.png)

L'**eth1** també té **DHCP habilitat per IPv4**, però en aquest cas obté una IP de la xarxa host-only per permetre l'accés des de l'equip físic.

### 7.7 Visualització d'adreces IP assignades

![Adreces IP assignades](/T09/img_t09/captura20.png)

Es mostren les IPs assignades a cada interfície:
- **eth0**: `10.0.2.20/24` (xarxa NAT, per escaneig)
- **eth1**: `192.168.56.119/24` (xarxa host-only, per accés web)

Ara ja tenim l'entorn preparat:
- Màquina objectiu: `10.0.2.19`
- Màquina d'escaneig: `10.0.2.20`
- Accés web des de l'equip físic: `192.168.56.119`

En la propera part es continuarà amb l'accés a la interfície web, la creació del target i l'execució de l'escaneig de vulnerabilitats.

Aquesta segona part de la guia cobreix l'accés a la interfície web d'OpenVAS, la creació del target d'escaneig, l'execució de l'anàlisi i la visualització inicial dels resultats.

---

## 8. Accés a la interfície web d'OpenVAS

### 8.1 Advertència de seguretat del certificat

![Advertència de certificat no segur](/T09/img_t09/captura21.png)

En accedir a `https://192.168.56.119/login` (la IP de la interfície host-only d'OpenVAS), el navegador mostra una advertència de **"No segur"** degut al certificat autosignat utilitzat per OpenVAS. Això és normal en entorns de prova i es pot ignorar per continuar.

### 8.2 Inici de sessió a OpenVAS

![Inici de sessió a OpenVAS](/T09/img_t09/captura22.png)

A la pantalla de login s'introdueixen les credencials de l'usuari administrador creat anteriorment durant el setup wizard:
- **Username**: usuari
- **Password**: (la contrasenya configurada)

Això permet accedir a la interfície web completa d'OpenVAS.

---

## 9. Dashboard inicial d'OpenVAS

![Dashboard inicial d'OpenVAS](/T09/img_t09/captura23.png)

Un cop autenticats, es mostra el **dashboard principal** que inclou:
- **NVTs by Severity Class**: Es veu que OpenVAS té 170,109 NVTs (Network Vulnerability Tests) carregats, distribuïts per severitat:
  - Log: 66,602
  - Low: 33,127
  - Medium: 5,242
  - High: 61,219
  - Critical: 0
- **Tasks by Severity Class**: Encara no hi ha tasques d'escaneig creades (Total: 0).
- **CVEs by Creation Time**: Gràfic de CVEs detectats al llarg del temps.

Aquesta pantalla confirma que OpenVAS està operatiu i té la base de dades de vulnerabilitats carregada.

---

## 10. Configuració de l'escaneig

### 10.1 Creació del Host

![Creació del Host](/T09/img_t09/captura24.png)

Abans de crear un target, s'afegeix el host a escanejar:
- **IP Address**: `10.0.2.19` (la màquina Metasploitable)
- **Comment**: linux

Això defineix l'objectiu de l'escaneig.

### 10.2 Creació del Target

![Creació del Target](/T09/img_t09/captura25.png)

Es crea un nou **Target** anomenat **"vulnerable linux"** amb les següents configuracions:
- **Hosts**: S'afegeix manualment la IP `10.0.2.19`
- **Port List**: "All IANA assigned TCP" (escaneja tots els ports TCP coneguts)
- **Alive Test**: "Use Scan Config Default"
- **Allow simultaneous scanning via multiple IPs**: No

El target agrupa els hosts a escanejar i les opcions d'escaneig.

### 10.3 Configuració de credencials SSH

![Creació de credencials SSH](/T09/img_t09/captura26.png)

Per realitzar un escaneig autenticat (més profund), es creen credencials SSH:
- **Name**: ssh
- **Type**: Username + Password
- **Username**: msfadmin
- **Password**: msfadmin (la contrasenya de Metasploitable)

Aquestes credencials permetran a OpenVAS accedir al sistema via SSH per detectar vulnerabilitats que requereixen autenticació.

### 10.4 Vista del target configurat

![Target configurat](/T09/img_t09/captura27.png)

El target **"vulnerable linux"** està configurat amb:
- **Hosts**: `10.0.2.19`
- **Port List**: All IANA assigned TCP
- **Credentials**: Prova ssh on Port 22

Ja està preparat per a l'escaneig.

---

## 11. Execució i resultats de l'escaneig

### 11.1 Informe inicial de l'escaneig

![Informe inicial](/T09/img_t09/captura28.png)

Després d'executar l'escaneig, es mostra el primer informe amb:
- **Data**: Tue, Jan 27, 2026 6:50 PM
- **Task**: vulnerable linux
- **Severity**: 0.0 (Log) - Aquest és el nivell general de la tasca

A la part superior es veu un gràfic de **"Reports by Severity Class"** que mostra un únic informe.

### 11.2 Vista detallada dels resultats

![Resultats detallats](/T09/img_t09/captura29.png)

A la vista de **Reports** es pot veure més detall:
- **Reports by Severity Class**: Ara mostra resultats de nivell **Medium** i **High**
- **Reports with High Results**: Gràfic que mostra resultats d'alta severitat
- L'informe té un **42%** de progrés (encara s'està executant)

### 11.3 Vista de tasques

![Vista de tasques](/T09/img_t09/captura30.png)

A la secció **Tasks** es veu la tasca **"vulnerable linux"** amb:
- **Status**: Done (completada)
- **Last Report**: 27/01/2026 18:50
- **Severity**: Representada en un gràfic

---

## 12. Vulnerabilitats detectades

### 12.1 Llistat de vulnerabilitats crítiques

![Vulnerabilitats crítiques](/T09/img_t09/captura31.png)

A la secció **Vulnerabilities** es mostren les primeres vulnerabilitats detectades, totes de nivell **Critical (10.0)**:
1. **The regex service is running** (80% QoD - Qualitat de Detecció)
2. **TWiki < 4.2.4 Multiple XSS / Command Execution Vulnerabilities** (80% QoD)
3. **rlogin Passwordless Login** (80% QoD)
4. **Distributed Ruby (dRuby/DRb) Multiple RCE Vulnerabilities** (99% QoD)
5. **Possible Backdoor: Ingreslock** (99% QoD)
6. **PHP < 5.3.13, 5.4.x < 5.4.3 Multiple Vulnerabilities** (9.8 Critical, 95% QoD)

Totes afecten al host `10.0.2.19`.

### 12.2 Més vulnerabilitats detectades

![Més vulnerabilitats](/T09/img_t09/captura32.png)

Es mostren vulnerabilitats addicionals:
- **vsfpd Compromised Source Packages Backdoor Vulnerability** (9.8 Critical, 99% QoD) als ports 6200 i 21
- **MySQL / MariaDB Default Credentials** (9.8 Critical, 95% QoD) al port 3306
- **PHP vulnerabilities** al port 80

Cada entrada mostra el port afectat i la qualitat de detecció.

### 12.3 Vista completa de vulnerabilitats

![Vista completa de vulnerabilitats](/T09/img_t09/captura33.png)

A la vista de **Vulnerabilities** es veu que hi ha un total de **124 vulnerabilitats** detectades, distribuïdes per severitat. El llistat inclou:
- **rlogin Passwordless Login** (10.0 Critical)
- **Possible Backdoor: Ingreslock** (10.0 Critical)
- **The regex service is running** (10.0 Critical)
- **Distributed Ruby vulnerabilities** (10.0 Critical)
- **TWiki vulnerabilities** (10.0 Critical)
- **OS End of Life Detection** (10.0 Critical)

Cada entrada mostra la data de detecció, severitat, QoD i nombre d'hosts afectats.

### 12.4 Informe final de l'escaneig

![Informe final](/T09/img_t09/captura34.png)

L'informe complet mostra els detalls de l'escaneig:
- **Task**: vulnerable linux
- **Durada**: 0:34 hores (34 minuts)
- **Hosts scanned**: 1
- **Ports**: 18 de 23 ports trobats
- **Applications**: 19 de 19 detectades
- **Operating Systems**: 1 detectat
- **CVEs**: 33 vulnerabilitats amb CVE assignat

### 12.5 Detalls per vulnerabilitat

![Detalls per vulnerabilitat](/T09/img_t09/captura35.png)

Es mostren vulnerabilitats amb els seus ports específics:
- **Distributed Ruby RCE** al port 8787/tcp
- **OS EOL Detection** al port 513/tcp
- **rlogin Passwordless Login** (no especifica port)
- **Possible Backdoor: Ingreslock** al port 1524/tcp
- **TWiki vulnerabilities** al port 80/tcp
- **MySQL Default Credentials** al port 3306/tcp
- **PHP vulnerabilities** al port 80/tcp

### 12.6 Exemple detallat d'una vulnerabilitat

![Detall de la vulnerabilitat Ingreslock](/T09/img_t09/captura36.png)

Es mostra la descripció detallada de la vulnerabilitat **"Possible Backdoor: Ingreslock"**:
- **Resum**: S'ha detectat un backdoor al host remot
- **Resultat de detecció**: El servei respon a la comanda 'id:' amb `uid=0(root) gid=0(root)`
- **Impacte**: Els atacants poden executar comandes arbitràries com a root
- **Solució**: Es recomana una neteja completa del sistema infectat
- **Mètode de detecció**: OID 1.3.6.1.4.1.25623.1.0.103549

Aquesta vulnerabilitat és particularment perillosa ja que permet accés root complet al sistema.

---

En aquest punt, l'escaneig s'ha completat amb èxit i s'han detectat **124 vulnerabilitats** a la màquina Metasploitable, incloent múltiples vulnerabilitats crítiques amb puntuació CVSS de 10.0. A la propera part es podrien analitzar en detall les vulnerabilitats més significatives i proposar mesures de mitigació.


## Conclusió final

Aquesta activitat ha complert amb l'objectiu de demostrar **l'aplicació pràctica dels mecanismes de seguretat activa** mitjançant l'escaneig de vulnerabilitats. Ha evidenciat com sistemes mal configurats o sense manteniment poden acumular **múltiples vulnerabilitats greus** que comprometen completament la seva seguretat.

El procés ha mostrat que la **vigilància contínua** i les **actualitzacions periòdiques** són components essencials d'una postura de seguretat proactiva, alineant-se tant amb el resultat d'aprenentatge RA3 com amb el criteri d'avaluació CA3.3.

La combinació d'eines com OpenVAS amb processos de gestió de vulnerabilitats ben definits constitueix una estratègia fonamental per a **protegir sistemes informàtics** en un ambient de amenaces cada vegada més sofisticades.