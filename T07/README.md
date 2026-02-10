# 🎓 T07 – Acadèmia feta amb Moodle

## 📝 Descripció

En aquesta pràctica instal·lo, configuro i gestiono una plataforma Moodle com si es tractés d’un encàrrec real per a una organització.

El client és **Escola Júlia**, un centre d’ensenyament secundari que necessita un portal d’aprenentatge online per facilitar la comunicació i el treball entre professorat i alumnat.

L’objectiu és demostrar que soc capaç de desplegar Moodle completament: des de la instal·lació inicial fins a la configuració avançada de cursos, rols, activitats, blocs i còpies de seguretat.

⚠️ L’avaluació es fa en directe, defensant cada part i demostrant que tot funciona correctament.

---

# 🧩 Part 1 – Instal·lació i configuració inicial

En aquesta primera fase:

- Instal·lo Moodle al servidor web.
- Creo la base de dades `moodle` (MySQL Improved).
- Configuro l’usuari administrador (`admin`).
- Estableixo el català com a idioma per defecte.
- Personalitzo el lloc amb:
  - Nom complet: **Escola d’Ensenyament Secundari Júlia**
  - Nom curt: **Escola Júlia**
  - Descripció institucional.
- Configuro la pàgina principal perquè mostri categories un cop autenticat l’usuari.
- Instal·lo un tema nou diferent al predeterminat.
- Personalitzo favicon i logo.

🎯 Resultat: Moodle adaptat a la identitat del centre.

---

# 👥 Part 2 – Usuaris, rols i cursos

En aquesta fase gestiono l’estructura acadèmica:

- Creo les categories:
  - 1er ESO
  - 2on ESO
  - 3er ESO
  - 4rt ESO

- Creo els comptes del professorat.
- Assigno rols (creador de cursos, professor, professor no-editor).
- Modifico permisos del rol creador de cursos.
- Creo tres cursos a 1er ESO:
  - **Matemàtiques 1**
  - **Taulell d’anuncis 1**
  - **Informàtica 1**

Configuro cada curs segons requisits específics:
- Idioma
- Format (temes, social, setmanal)
- Visibilitat
- Límits de fitxers
- Grups
- Rols personalitzats
- Automatriculació i accés de convidats

També activo l’autenticació basada en correu electrònic i comprovo el procés de registre d’un alumne.

🎯 Resultat: Plataforma funcional amb estructura acadèmica completa.

---

# 📚 Part 3 – Recursos i activitats del curs

Treballant com a professor de **Matemàtiques 1**:

- Organitzo els temes amb títols i resums.
- Afegeixo etiqueta inicial amb imatge.
- Configuro:
  - Fòrum
  - Glossari amb entrades i imatge
  - Xat programat
  - Enquesta
  - Enllaç extern (XTEC)
  - Pàgina amb criteris d’avaluació (taula amb ponderacions)

Reordeno els elements segons l’ordre establert.

🎯 Resultat: Curs estructurat, visualment coherent i amb eines de comunicació actives.

---

# 🧠 Part 4 – Activitats d’aprenentatge i avaluació

Amplio el tema **Nombres** amb:

- Etiquetes amb imatges (Apunts, Exercicis pràctics, Exercicis d’avaluació)
- Consulta amb càlcul matemàtic
- Lliçó sobre nombres racionals amb:
  - 4 pàgines de contingut
  - 4 preguntes Verdader/Fals
  - Sistema de puntuació i intents configurats

- Qüestionari temporitzat amb:
  - 5 preguntes variades
  - Barrejades
  - Penalització per intents extra
  - Retroacció global

- Tasca de text en línia
- Tasca de pujada de fitxer amb data límit

🎯 Resultat: Sistema complet d’aprenentatge i avaluació configurat professionalment.

---

# 🧩 Part 5 – Blocs, plugins i còpia de seguretat

Com a administrador:

- Afegeixo i configuro blocs:
  - Calendari
  - Esdeveniments pròxims
  - Usuaris en línia
  - Els meus cursos
  - Comentaris
  - Entrada aleatòria del glossari
  - Canal RSS
  - Bloc Text amb enllaços externs

- Afegeixo gadgets amb JavaScript.
- Creo 3 insígnies (badges) personalitzades amb seguiment de compleció.
- Creo activitats que permeten obtenir insígnies.
- Realitzo una còpia de seguretat del curs.
- Restauro la còpia en un nou curs (**MAT_BCKP**) per verificar el correcte funcionament.

🎯 Resultat: Curs completament personalitzat, ampliat amb plugins i amb sistema de backup verificat.

---

# 🏁 Conclusió

En aquesta pràctica he desplegat Moodle des de zero, configurant-lo com si fos un projecte real per a un centre educatiu.

He demostrat capacitat per:

- Instal·lar i personalitzar una plataforma LMS
- Gestionar usuaris i rols
- Crear i configurar cursos
- Afegir activitats i sistemes d’avaluació
- Implementar blocs i plugins
- Gestionar còpies de seguretat

Aquest projecte simula un encàrrec professional real i reflecteix la meva capacitat de desplegar i administrar Moodle de manera completa i estructurada.
