# P01 – Control de versions. GitHub Classroom i git

## 📌 Descripció del producte

Fins ara havíem treballat amb GitHub directament des de la web: creant repositoris públics, pujant fitxers mitjançant la interfície web i documentant els projectes. Aquest sistema, però, té limitacions importants: és lent per gestionar carpetes i imatges, no aprofita la potència del control de versions en local i, a més, els repositoris públics exposen el nostre treball a qualsevol persona.

En aquest producte hem fet un **salt de qualitat** en l’ús de GitHub: hem après a treballar amb **git en local**, versionar els canvis (commits), sincronitzar amb repositoris remots i utilitzar **GitHub Classroom** per disposar de repositoris privats dins d’una organització educativa. Això ens permet treballar de la mateixa manera que es fa en una empresa real, on el codi i la documentació són confidencials i només accessibles per a l’equip autoritzat.

---

## 🎯 Objectius específics

- Entendre el flux de treball professional amb **git**: treballar en local (working directory), afegir canvis a l’àrea de staging (`git add`), fer commits (`git commit`) i sincronitzar amb el repositori remot (`git push` / `git pull`).
- Utilitzar **GitHub Classroom** per crear un repositori privat associat a una organització. Cada alumne rep un *fork* automàtic del repositori base, que és privat i només visible per l’alumne i el professorat.
- Aprendre a clonar el repositori remot a l’ordinador local, treballar amb els fitxers, versionar els canvis i pujar-los de nou al remot.
- Prendre consciència de la importància de tenir **repositoris privats** per protegir la propietat intel·lectual del treball realitzat.
- Preparar l’entorn perquè, en acabar el projecte, puguem fer públic el repositori i afegir-lo al nostre portafoli professional (fent un fork al compte personal).

---

## 🛠️ Flux de treball seguit

### 1. Accés a GitHub Classroom

El professorat va proporcionar un enllaç de **GitHub Classroom** per a l’activitat. En acceptar-lo, es va crear automàticament un **repositori privat** dins de l’organització de la classe. Aquest repositori és un fork del repositori base que conté l’estructura inicial del projecte.

### 2. Clonació del repositori a l’ordinador local

Des de la línia de comandes (o des de VS Code), vam clonar el repositori remot al nostre equip:

```bash
git clone https://github.com/organitzacio/nom-repositori.git
```

### 3. Treball en local i versionat

Vam crear, modificar i eliminar fitxers i carpetes a l’ordinador. A mesura que avançàvem, vam anar fent commits amb missatges descriptius:

```bash
git add .
git commit -m "Descripció dels canvis realitzats"
```

### 4. Sincronització amb el repositori remot

Per pujar els canvis al repositori privat de GitHub Classroom:

```bash
git push origin main
```

També vam aprendre a baixar canvis d’altres companys (en treballs col·laboratius) mitjançant `git pull`.

### 5. Conversió a públic (per al portafoli)

Un cop finalitzat el projecte i aprovat pel professorat, vam canviar la visibilitat del repositori a **pública** (des de la configuració de GitHub) o vam fer un **fork** al compte personal per tal d’incloure el projecte al nostre portafoli de GitHub.

---

## 📁 Contingut lliurat

- **Repositori privat** creat a GitHub Classroom, amb l’estructura de carpetes i fitxers del projecte.
- **Historial de commits** coherent i amb missatges clars que reflecteixen l’evolució del treball.
- **Repositori local** sincronitzat amb el remot.
- **README.md** explicatiu (aquest mateix fitxer) dins de la carpeta `Producte01`.

---

## 🔗 Enllaços d’interès

- 📘 **Guia de GitHub Classroom:** [https://github.com/SMX2n/guia-github-classroom](https://github.com/SMX2n/guia-github-classroom)
- 📘 **Guia de Control de Versions (git):** [https://github.com/SMX2n/ControlVersions](https://github.com/SMX2n/ControlVersions)
- 🔗 **Repositori del projecte a GitHub Classroom** (privat, accessible només per a mi i el professorat): enllaç intern proporcionat a l’aula

---

## 💡 Aprenentatges clau

- **Diferència entre treballar només a la web i treballar amb git en local:** la web és pràctica per a canvis petits, però el flux local amb git és molt més potent per gestionar projectes complexos, carpetes i imatges, i permet un control granular de cada canvi.
- **Importància dels repositoris privats:** protegir el treball abans de fer-lo públic evita que altres es puguin apropiar del codi o la documentació sense permís. A les empreses, els repositoris interns sempre són privats.
- **Flux bàsic de git:** `clone`, `add`, `commit`, `push`, `pull`. Aquest és el mateix flux que s’utilitza diàriament en entorns professionals.
- **GitHub Classroom com a eina educativa:** permet al professorat distribuir repositoris base i fer un seguiment individualitzat del treball de cada alumne sense que es puguin copiar entre ells.
- **Preparació del portafoli:** un cop el projecte està acabat i validat, es pot fer públic i afegir-lo al perfil de GitHub per mostrar-lo a futurs ocupadors.

---

## 👤 Autor

**Guillem Barjuan Alonso** – CFGM SMX  
Projecte 05 – Control de versions i GitHub Classroom  
Data de realització: segon trimestre del curs 2025-2026

---

*Aquest producte representa el punt d’inflexió en la nostra manera de treballar amb GitHub: deixem enrere l’edició web i adoptem el flux professional amb git local, repositoris privats i GitHub Classroom. És el mateix mètode que fan servir els equips de desenvolupament de tot el món.*
