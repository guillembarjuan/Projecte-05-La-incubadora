# 📁 Projecte 05 – La incubadora

Benvingut al cinquè projecte del curs de **Sistemes Microinformàtics i Xarxes (SMX)**.  
Arriba el moment de deixar de treballar només com a estudiants i començar a treballar com a professionals que construeixen una proposta completa. La classe es converteix en una **incubadora d’empreses** on, durant 4 setmanes, hem dissenyat una startup IT des de zero i l’hem portada fins a una presentació final (Demo Day / Shark Tank) davant d’un comitè d’inversió.

> *“No es tracta de fer una idea ‘xula’. Es tracta de construir una empresa amb un problema real, un client que existeixi, una solució clara, uns números coherents i un equip que pugui defensar-la.”*

Aquest projecte té una doble capa: construir una empresa (PI RA1 i RA2) i construir el nostre perfil professional (IPO RA4). Hem après a detectar problemes reals, definir un client B2B, dissenyar una solució tècnica integrada (local, xarxa, hardware, programari, web, chatbot), estudiar la viabilitat econòmica i defensar-ho tot amb un pitch professional.

---

## 📌 Índex

1. [Descripció del projecte](#-descripció-del-projecte)
2. [Metodologia de treball](#-metodologia-de-treball)
3. [Tasques realitzades](#-tasques-realitzades)
4. [Productes finals](#-productes-finals)
5. [Estructura del repositori](#-estructura-del-repositori)
6. [Tecnologies i eines](#-tecnologies-i-eines)
7. [Aprenentatges clau](#-aprenentatges-clau)
8. [Competències treballades](#-competències-treballades)
9. [Enllaços d’interès](#-enllaços-dinterès)
10. [Autor](#-autor)

---

## 📋 Descripció del projecte

**La incubadora** és una simulació seriosa i guiada on cada equip ha creat una empresa tecnològica B2B. Hem passat per totes les fases d’una startup real:

- **Setmana 1:** Detectar un problema real i definir un client real (no inventat).
- **Setmana 2:** Convertir-ho en una proposta d’empresa amb estratègia (qui som, què fem, com competim).
- **Setmana 3:** Prototip + viabilitat (fer-lo tangible i demostrar que els números no són fantasia).
- **Setmana 4:** Validació, refinament i pitch (defensar-ho com si ens juguéssim el futur professional).

Hem treballat totes les àrees d’una consultora IT: des de la infraestructura física (local real a Mataró, disseny 2D/3D) fins a la xarxa (configurada amb Packet Tracer o similar), passant pel pressupost (Excel), la identitat corporativa (logo, colors), la presència digital (web amb Octopus i Figma), un chatbot basat en Gemini (GEM + NotebookLM), l’estudi de mercat (competidors reals) i el pla de negoci (ingressos, costos, punt d’equilibri).

A més, hem integrat el **Green IT** com a eix transversal, oferint estudis de sostenibilitat als clients.

---

## 🧭 Metodologia de treball

- **GitHub Classroom:** repositoris privats per a cada alumne, treball en local amb git i sincronització remota.
- **Design Thinking:** aplicat a la fase de creativitat per detectar problemes reals i generar solucions.
- **IA com a accelerador:** ús de Gemini per proposar continguts, contrastar idees i crear materials, però sempre amb criteri humà.

---

## ✅ Tasques realitzades

A continuació es mostren les principals tasques desenvolupades, extretes del document d’instruccions:

| ID | Tasca | Descripció | Tipus |
|----|-------|-------------|-------|
| T00 | Presentació del projecte i dinàmica de Design Thinking | Creació del repositori a GitHub Classroom, Planner i primera dinàmica de creativitat. | Grup |
| T01 | Disseny de la Solució Tècnica Integrada | Elaboració de tots els entregables de l’empresa: local real (fitxa + imatges 2D/3D), xarxa (diagrama + configuració), pressupost (Excel), identitat corporativa (brand board), web (Octopus + Figma), chatbot (GEM + NotebookLM), estudi de mercat, pla de negoci i viabilitat. | Grup |
| T02 | Control de versions. Treballant amb git | Treball en local amb git, commits, sincronització amb repositori remot de GitHub Classroom. | Individual |
| T03 | Serveis de transferència de fitxers | Estudi i configuració de servidors FTP i sFTP (mode actiu/passiu, chroot, seguretat). | Individual |
| T04 | Instal·lació Windows Server 2025 | Creació d’una VM amb Windows Server 2025, configuració inicial i guia d’instal·lació. | Individual |
| T05 | Instal·lació del domini | Promoció del servidor a controlador de domini, creació d’un domini nou (translogicXX.test) i generació d’script PowerShell. | Individual |
| T06 | Configuració del domini | Creació d’unitats organitzatives (OU), grups de seguretat, plantilles d’usuaris, agregació d’un client Windows 11 al domini. | Individual |
| T07 | Acadèmia feta amb Moodle | Instal·lació completa de Moodle, personalització, creació de categories, cursos, usuaris, rols, activitats (fòrums, glossaris, qüestionaris, xats, lliçons, tasques) i còpia de seguretat. | Individual |
| T08 | Seguretat: protegint-nos contra el malware | Estudi de mecanismes de defensa (antivirus, eines d’anàlisi, proteccions integrades) i observació de programari maliciós en entorn controlat. | Individual |
| T09 | Seguretat: les vulnerabilitats dels sistemes | Anàlisi de vulnerabilitats, aplicació de pegats, bones pràctiques de hardening. | Individual |
| T10 | Introducció al concepte Green IT | Definició de Green IT, exemples reals, bones pràctiques aplicables a la nostra empresa, disseny de política i indicadors. | Parelles |

---

## 🏁 Productes finals

Els productes avaluables del projecte són tres. Cada un està documentat dins la seva carpeta corresponent al repositori.

| Codi | Nom del producte | Enllaç a la carpeta |
|------|------------------|---------------------|
| **P01** | Control de versions. GitHub Classroom i git | [`Producte01`](./Producte01) |
| **P02** | Llicenciament Windows Server 2025 | [`Producte02`](./Producte02) |
| **P03** | Presentació empresa amb visió Green IT | [`Producte03`](./Producte03) |

Cada carpeta conté el seu propi `README.md` amb la descripció detallada, els càlculs, les justificacions i, en el cas del P03, el guió, el suport visual i l’evidència d’assaig (àudio o vídeo).

---

## 📁 Estructura del repositori

El repositori està organitzat de la següent manera (segons la imatge proporcionada):

```
Projecte-05-La-Incubadora/
│
├── README.md                    # Aquest fitxer
│
├── Producte01/                  # P01 – Control de versions (git + GitHub Classroom)
├── Producte02/                  # P02 – Llicenciament Windows Server 2025
├── Producte03/                  # P03 – Presentació empresa amb visió Green IT
│
├── T01/                         # Disseny de la Solució Tècnica Integrada (totes les parts)
├── T02/                         # Control de versions (git)
├── T03/                         # Serveis de transferència de fitxers (FTP/sFTP)
├── T04/                         # Instal·lació Windows Server 2025
├── T05/                         # Instal·lació del domini
├── T06/                         # Configuració del domini
├── T07/                         # Acadèmia Moodle
├── T08/                         # Seguretat: malware
├── T09/                         # Seguretat: vulnerabilitats
└── T10/                         # Green IT
```

Tota la documentació tècnica està redactada en **Markdown**, amb imatges a subcarpetes `img` i text alternatiu per a l’accessibilitat. Els arxius Excel de pressupostos i els fitxers de configuració de xarxa (Packet Tracer, scripts) també es troben a les carpetes corresponents.

---

## 🛠️ Tecnologies i eines utilitzades

- **Metodologia àgil:** Kanban amb Microsoft Planner, Design Thinking.
- **Control de versions:** Git, GitHub Classroom (repositoris privats).
- **Sistemes operatius:** Windows Server 2025, Windows 11, Linux (Ubuntu Server, Zorin OS).
- **Serveis de xarxa:** DHCP, DNS, FTP/sFTP, Active Directory.
- **Virtualització:** VirtualBox, OVA.
- **Disseny i prototipat:** Figma (web), Octopus.do (sitemap), Tinkercad (3D), Canva (branding), IA generativa d’imatges (Gemini, etc.).
- **Backend i automatització:** Moodle, WordPress, GEM (Gemini) + NotebookLM.
- **Seguretat:** Antivirus, eines de desinfecció, anàlisi de vulnerabilitats, hardening.
- **Sostenibilitat:** Green IT, criteris ASG, economia circular.
- **Eines d’ofimàtica:** Excel (pressupostos, viabilitat), Google Slides (presentacions).

---

## 💡 Aprenentatges clau

- **Emprenedoria real:** passar d’una idea a una empresa B2B completa, amb problemes reals, clients reals i números coherents.
- **Integració tècnica:** connectar el local físic (ubicació, m2, cost), la xarxa (VLANs, DHCP, NAT, SSID), el maquinari (5 PCs, NAS, switch, AP), el programari (SO, cloud, eines de gestió) i la presència digital (web, chatbot).
- **Control de versions professional:** treballar amb git en local, commits amb missatges clars, sincronització amb repositoris privats de GitHub Classroom.
- **Llicenciament de Windows Server:** calcular costos segons el model per nucli, comparar Standard vs Datacenter, triar CALs (User vs Device) i presentar-ho al client.
- **Presentació i pitch:** preparar un guió estructurat en 11 blocs, crear un suport visual atractiu (sense llegir-lo) i assajar abans de la presentació final (amb evidència d’assaig).
- **Green IT com a eix diferencial:** oferir estudis de sostenibilitat, decisions concretes d’eficiència energètica, virtualització i reducció de residus.
- **Validació amb IA:** construir un chatbot (GEM) que respongui preguntes complexes d’inversors utilitzant un NotebookLM amb totes les fonts del projecte.

---

## 🧰 Competències treballades

- **Emprenedoria i innovació:** identificar problemes reals, validar solucions, dissenyar models de negoci (RA4 de 1710).
- **Infraestructura i xarxes:** dissenyar i configurar xarxes locals (VLAN, DHCP, NAT), servidors Windows i Linux, serveis de transferència de fitxers.
- **Seguretat:** protegir sistemes contra malware, analitzar vulnerabilitats, aplicar bones pràctiques de hardening.
- **Aplicacions web:** instal·lar i gestionar Moodle (cursos, usuaris, rols, activitats, còpies de seguretat).
- **Sostenibilitat:** aplicar criteris Green IT i economia circular al sector tecnològic (RA4 i RA5 de 1708).
- **Control de versions i documentació:** treballar amb git, GitHub Classroom i Markdown.
- **Comunicació professional:** elaborar presentacions, guions, assajos i defensar el projecte davant d’inversors.

---

## 🔗 Enllaços d’interès

- 👤 **Perfil de GitHub:** [github.com/guillembarjuan](https://github.com/guillembarjuan)
- 📘 **Guia de GitHub Classroom:** [https://github.com/SMX2n/guia-github-classroom](https://github.com/SMX2n/guia-github-classroom)
- 📘 **Guia de Control de Versions (git):** [https://github.com/SMX2n/ControlVersions](https://github.com/SMX2n/ControlVersions)
- 📂 **Carpeta P01 (git i GitHub Classroom):** [`./Producte01`](./Producte01)
- 📂 **Carpeta P02 (Llicenciament Windows Server):** [`./Producte02`](./Producte02)
- 📂 **Carpeta P03 (Presentació Green IT):** [`./Producte03`](./Producte03)

---

## 👤 Autor

**Guillem Barjuan Alonso** – CFGM SMX  
Curs 2025-2026

---

*Aquest projecte demostra que a mitjan segon curs ja no toca només aprendre coses: toca començar a semblar professional. La incubadora ens ha permès construir evidències reals del nostre valor, des de la detecció d’un problema real fins a la defensa davant d’inversors, passant per totes les capes tècniques i de negoci. Al final, no només hem creat una empresa: hem construït el nostre propi perfil professional.*

