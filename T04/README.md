# 🪟 T04: Instal·lació de Windows Server 2025

## 📄 Descripció de la Tasca

En aquesta tasca treballo en un projecte encarregat per **TransLògic S.A.**, després del nostre assessorament previ. L’objectiu és preparar el **desplegament de servidors Windows Server 2025** mitjançant una instal·lació de prova en màquines virtuals.

Aquesta instal·lació no només em serveix per aprendre i practicar els procediments correctes, sinó també per **crear una guia d’instal·lació base** que posteriorment s’utilitzarà en la implantació real dels sistemes del client. La documentació generada ha de ser clara, reutilitzable i seguir bones pràctiques professionals.

---

## 🎯 Objectius

- Crear una màquina virtual amb la configuració indicada.
- Instal·lar **Windows Server 2025 en mode gràfic (GUI)**.
- Configurar correctament idioma, teclat, nom de l’equip i xarxa.
- Actualitzar el sistema operatiu i deixar-lo preparat per a futures tasques.
- Comparar els requisits de la màquina virtual amb els **requisits oficials de Microsoft**.
- Documentar tot el procés en format **Markdown**, amb captures de pantalla i observacions.

---

## 🧱 Configuració de la Màquina Virtual

La màquina virtual creada té la següent configuració:

- **Memòria RAM:** 8 GB  
- **Processadors:** 2 CPU  
- **Discos:**
  - Disc principal: 32 GB (instal·lació del SO)
  - Disc secundari: 10 GB
- **Xarxa:**
  - Interfície 1: NAT
  - Interfície 2: Host-Only
- **Sistema operatiu:** Windows Server 2025 (GUI)

Aquesta configuració està pensada per simular un entorn realista de servidor i facilitar futures ampliacions (domini, rols, serveis, etc.).

---

## 🧪 Comparació amb els Requisits de Microsoft

Un cop definida la màquina virtual, comparo la configuració amb els **requisits mínims oficials de Microsoft per a Windows Server 2025**.

- La quantitat de **RAM (8 GB)** és superior al mínim requerit.
- Els **2 processadors** compleixen amb escreix les necessitats bàsiques del sistema.
- El **disc principal de 32 GB** compleix el mínim exigit per a la instal·lació.
- La configuració de xarxa amb dues interfícies és coherent amb entorns professionals.

👉 **Conclusió:** la configuració de la màquina virtual és **coherent i adequada** per a una instal·lació de Windows Server 2025 i per a un entorn de proves.

---

## ⚙️ Procediment d’Instal·lació

Durant la instal·lació de Windows Server 2025 segueixo els passos següents, documentats amb captures de pantalla:

1. Creació de la màquina virtual amb els paràmetres definits.
2. Inici del procés d’instal·lació de Windows Server 2025.
3. Selecció del **mode GUI**.
4. Idioma del sistema en **anglès (US)**.
5. Configuració regional i **teclat en espanyol**.
6. Selecció del disc principal (32 GB) per a la instal·lació.
7. Finalització de la instal·lació i primer inici del sistema.
8. Configuració inicial del sistema.

En cada pas afegeixo observacions sobre possibles errors, decisions preses i bones pràctiques.

---

## 🖥️ Configuració Post-instal·lació

Un cop el sistema està instal·lat:

- Canvio el **nom de l’equip** a:
DCxx

(on `xx` correspon al meu número de llista).
- Realitzo totes les **actualitzacions del sistema**.
- Un cop actualitzat, **pauso les actualitzacions** el màxim temps possible per garantir estabilitat durant les pràctiques.

---

## 📸 Documentació

La guia inclou:

- Captures de pantalla de:
- Creació de la màquina virtual
- Procés d’instal·lació
- Configuració inicial del sistema
- Canvi de nom de l’equip
- Estat de les actualitzacions
- Observacions personals sobre cada fase del procés.
- Explicacions clares pensades perquè qualsevol tècnic pugui repetir la instal·lació sense dificultats.

Tot el contingut està documentat en **format Markdown**, seguint criteris de claredat i ordre.

---

## ✅ Resultat Final

Amb aquesta tasca he obtingut:

- Una **instal·lació funcional de Windows Server 2025** en entorn virtual.
- Una configuració coherent amb els requisits oficials de Microsoft.
- Una **guia d’instal·lació base**, reutilitzable per a futurs desplegaments.
- Una documentació clara i professional, pensada per a entorns reals de producció.

Aquesta tasca estableix les bases per a la posterior configuració de rols i serveis del servidor.

---

## 📚 Materials i Recursos

- **UD.6. AA2. Instal·lació Windows Server 2025**  
Moodle 0224 — Sistemes Operatius en Xarxa
- **Requisitos de hardware para Windows Server**  
Microsoft Learn