# P02 – Llicenciament Windows Server 2025

## 📌 Descripció del producte

Aquest producte consisteix en l’**anàlisi i càlcul del llicenciament de Windows Server 2025** per a l’empresa client **TransLògic S.A.**, una empresa de logística regional que vol renovar la seva infraestructura de servidors. El client disposa d’un servidor físic amb 2 processadors (24 nuclis en total) i necessita virtualitzar 12 màquines virtuals amb Windows Server (Controlador de Domini, Servidor de Fitxers, Servidor d’Impressores, SQL Server i 8 VMs de suport).

L’encàrrec inclou:
- Analitzar el model de llicenciament per nucli (core) de Windows Server 2025.
- Calcular el cost total per a les edicions **Standard** i **Datacenter**.
- Determinar quin tipus de **CAL** (Client Access License) – *User* o *Device* – és més econòmic per a l’empresa (45 empleats, 30 treballadors d’oficina amb PC+portàtil, 15 mossos de magatzem que comparteixen 5 tauletes).
- Justificar la decisió final basant-se en costos, escalabilitat futura i funcionalitats avançades (Storage Spaces Direct, SDN, etc.).
- Elaborar una **presentació professional** (5-10 minuts) per al gerent de TransLògic, explicant la solució de manera clara i adaptada a un perfil no tècnic.

---

## 🎯 Objectius específics

- Comprendre el model de llicenciament per nucli de Windows Server 2025 (mínim 8 nuclis per processador, mínim 16 nuclis per servidor).
- Calcular el nombre de llicències de nucleis necessàries per al servidor físic del client.
- Comparar les edicions **Standard** (permet 2 VMs per llicència completa) vs **Datacenter** (VMs il·limitades) en termes de cost i funcionalitats.
- Avaluar les opcions de CAL: **User CAL** (per a cada usuari, independent del dispositiu) vs **Device CAL** (per a cada dispositiu que accedeix al servidor).
- Justificar la recomanació amb criteris econòmics i tècnics, considerant el creixement futur.
- Presentar la proposta al client amb llenguatge entenedor i suport visual.

---

## 🧮 Anàlisi realitzat

### 1. Requeriments del client

| Concepte | Dades |
|----------|-------|
| Processadors (físics) | 1 servidor amb 2 CPUs |
| Nuclis per CPU | 12 |
| Total nuclis | 24 |
| Màquines virtuals (VMs) | 12 (Windows Server) |
| Empleats | 45 |
| Treballadors d’oficina | 30 (cadascun té PC + portàtil) |
| Mossos de magatzem | 15 (comparteixen 5 tauletes) |

### 2. Càlcul de llicències de Windows Server

Segons el model de Microsoft:
- Cada processador requereix llicència per a tots els seus nuclis.
- Mínim 8 nuclis per processador i 16 nuclis per servidor.
- Les llicències es venen en paquets de 2 nuclis (Core Licenses).

**Total nuclis a llicenciar:** 24 nuclis → 12 paquets de 2 nuclis.

#### Opció Standard
- Cada llicència completa (16 nuclis) cobreix fins a 2 VMs.
- Per a 12 VMs, calen **6 llicències completes** (2 VMs × 6 = 12 VMs).
- Total paquets de 2 nuclis: 6 llicències × 8 paquets (perquè 16 nuclis = 8 paquets) = **48 paquets de 2 nuclis**.
- **Cost estimat** (preu orientatiu, consultar llista oficial): 48 × preu per paquet.

#### Opció Datacenter
- Una llicència completa (16 nuclis) cobreix VMs il·limitades.
- Per a 24 nuclis, cal **1 llicència completa** (16 nuclis) + **8 nuclis addicionals** (4 paquets de 2 nuclis).
- Total paquets de 2 nuclis: 8 (dels 16) + 4 (dels 8 addicionals) = **12 paquets de 2 nuclis**.
- **Cost estimat**: 12 × preu per paquet (però el preu per paquet de Datacenter és superior al de Standard).

**Conclusió parcial:** Datacenter requereix menys paquets (12 vs 48), però cada paquet és més car. Cal fer el càlcul amb els preus oficials per determinar l’opció més econòmica per al volum actual.

### 3. Càlcul de CALs

- **Windows Server CAL** (necessària per a cada usuari o dispositiu que accedeix als serveis del servidor).
- **User CAL**: 45 empleats = 45 User CAL.
- **Device CAL**:  
  - 30 treballadors d’oficina: cadascú té PC + portàtil → 60 dispositius.  
  - 15 mossos de magatzem: comparteixen 5 tauletes → 5 dispositius.  
  - Total dispositius: **65 Device CAL**.

*Anàlisi:* 65 Device CAL són més que 45 User CAL. A més, els empleats d’oficina usen dos dispositius cadascun, però només un usuari. **User CAL** és més econòmic en aquest escenari.

### 4. Funcionalitats addicionals

- **Standard**: funcionalitats bàsiques de virtualització.
- **Datacenter**: inclou Storage Spaces Direct (SDN) per a alta disponibilitat i virtualització de xarxes. Si el client vol escalar o tenir tolerància a fallades avançada, Datacenter pot ser justificable malgrat el cost inicial més elevat.

---

## 🎤 Presentació al client

Es va elaborar una **presentació en format digital** (PowerPoint / Google Slides) amb els següents apartats:

1. **Context del client** – necessitat de renovar la infraestructura.
2. **Model de llicenciament per nucli** – explicació senzilla per a un perfil no tècnic.
3. **Càlcul de llicències** – comparativa de costos entre Standard i Datacenter (amb preus reals o estimats).
4. **Càlcul de CALs** – justificació de per què s’escull User CAL.
5. **Recomanació final** – opció triada i motius (cost, escalabilitat, funcionalitats).
6. **Torn de preguntes** – preparació per respondre dubtes del gerent.

🔗 **Enllaç a la presentació:** (pendent d’inserir per part de l’alumne)

---

## 📁 Contingut lliurat

- **Informe tècnic** (en Markdown) amb els càlculs detallats i la justificació.
- **Presentació digital** (enllaç a Google Slides, PowerPoint o PDF) per defensar davant del client.
- **README.md** dins de la carpeta `Producte02` (aquest fitxer).

---

## 💡 Aprenentatges clau

- **Model de llicenciament per nucli**: entendre com es comptabilitzen els nuclis físics i com es tradueixen en paquets de llicències.
- **Diferència entre edicions Standard i Datacenter**: no només en cost, sinó en funcionalitats (Storage Spaces Direct, SDN, tolerància a fallades).
- **Càlcul de CALs**: aplicar la lògica de User vs Device segons el perfil de l’empresa (treballadors amb múltiples dispositius vs dispositius compartits).
- **Comunicació amb el client**: adaptar el llenguatge tècnic a un públic no expert, utilitzant exemples i metàfores.
- **Presa de decisions justificada**: basar la recomanació en dades objectives (costos reals, necessitats de futur) i no només en preferències.

---

## 👤 Autor

**Guillem Barjuan Alonso** – CFGM SMX  
Projecte 05 – Llicenciament Windows Server 2025  
Data de realització: segon trimestre del curs 2025-2026

---

*Aquest producte demostra que un consultor IT no només ha de saber de tecnologia, sinó també de models de llicenciament, costos i comunicació amb el client. La millor solució tècnica pot no ser viable si no s’ajusta al pressupost o no s’explica correctament.*
