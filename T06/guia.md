# T06: Configuració del domini

## Introducció
Un cop tenim el nostre domini creat, el següent pas és desplegar el domini, és a dir, crear els diferents objectes que el formen: grups, usuaris, màquines. En aquesta tasca veurem la utilitat d’organitzar els objectes amb unitats organitzatives (OU) i implementarem una estructura completa per a l'empresa.

## 1. Configuració inicial del Server Manager

### 1.1 Accés al Server Manager

![Server Manager Dashboard](/T06/img_t06/captura1.png)

**Anàlisi**: El Server Manager mostra el tauler de control principal del servidor Windows Server. Veiem que hi ha 3 rols instal·lats i 1 grup de servidors amb 1 servidor total. A la secció "QUICK START" tenim les opcions més habituals com afegir rols i funcionalitats, afegir altres servidors per gestionar, crear grups de servidors i connectar el servidor al núvol.

A la part esquerra hi ha una llista completa d'eines d'administració disponibles, incloent totes les eines d'Active Directory, gestió de discos, visor d'esdeveniments, gestió de polítiques de grup, etc.

### 1.2 Verificació dels rols instal·lats

![Server Manager Dashboard](/T06/img_t06/captura1.png)

**Anàlisi**: A la secció "ROLE AND SERVER GROUPS" podem veure els rols instal·lats:
- **AD DS (Active Directory Domain Services)**: Amb opcions de gestió, esdeveniments, serveis, rendiment i resultats BPA
- **DNS**: Amb les mateixes opcions de gestió

Això confirma que tenim un controlador de domini completament operatiu amb els serveis bàsics funcionant.

### 1.3 Accés a Active Directory Administrative Center

![Active Directory Administrative Center](/T06/img_t06/captura2.png)

**Anàlisi**: Aquesta és la nova consola d'administració d'Active Directory, que ofereix una interfície més moderna i funcionalitats millorades. Veiem:
- **Domini**: TranslogiC01 (local)
- **Filtres**: Per nom, tipus i descripció
- **Contenidors predeterminats**: Builtin, Computers, Domain Controllers, etc.
- **Tasques disponibles**: Nova, Eliminar, Cercar, Propietats

A la part esquerra hi ha la llista de tots els contenidors del domini, i a la dreta les tasques disponibles per al node seleccionat.

### 1.4 Activació de la Paperera de Reciclatge

![Confirmació activació Paperera de Reciclatge](/T06/img_t06/captura3.png)

**Anàlisi**: Estem activant una funcionalitat important de seguretat: la Paperera de Reciclatge d'Active Directory. Aquesta funcionalitat:
- Permet recuperar objectes eliminats accidentalment
- **És irreversible**: Un cop activada no es pot desactivar
- Afegeix una capa de protecció contra eliminacions accidentals

El quadre de diàleg ens adverteix clarament sobre la irrevocabilitat d'aquesta acció.

### 1.5 Verificació del contenidor Deleted Objects

![Contenidor Deleted Objects](/T06/img_t06/captura4.png)

**Anàlisi**: Després d'activar la Paperera de Reciclatge, veiem que s'ha creat automàticament el contenidor "Deleted Objects" a l'arrel del domini. Aquest contenidor:
- **Object class**: Container
- **Descripció**: Default container for deleted objects
- **Funció**: Emmagatzema temporalment els objectes eliminats abans de la seva eliminació permanent

A la barra lateral esquerra també podem veure les diferents categories de cerca disponibles.

### 1.6 Panel de gestió AD DS

![Server Manager AD DS](/T06/img_t06/captura5.png)

**Anàlisi**: Aquest és el panell específic de gestió de AD DS dins del Server Manager. Observem:
- **Servidors**: DC01 amb adreces IPv4 10.0.2.17 i 10.0.2.19
- **Eines disponibles**: Tota la suite d'eines d'Active Directory (Users and Computers, Sites and Services, etc.)
- **Esdeveniments**: Hi ha warnings i errors que caldria investigar (4013, 1202, 1005, etc.)

A la part inferior hi ha una llista d'eines de línia de comandes específiques per a la gestió d'Active Directory.

### 1.7 Vista de l'estructura actual del domini

![Active Directory Users and Computers](/T06/img_t06/captura6.png)

**Anàlisi**: Aquesta captura mostra la consola clàssica "Active Directory Users and Computers". Veiem:
- **Domini**: translogic01.test
- **Consultes guardades**: Saved Queries
- **Estructura actual**: Només el domini sense OUs personalitzades
- **Barra d'estat**: Mostra l'estat dels serveis d'Active Directory amb timestamps

Això representa el punt de partida abans de crear la nostra estructura organitzativa.

## 2. Creació de l'estructura d'Unitats Organitzatives (OUs)

### 2.1 Justificació de l'estructura

**Decisió de disseny**: He decidit crear una estructura jeràrquica que separa clarament els diferents tipus d'objectes i organitza els usuaris per departaments. Aquesta estructura segueix les millors pràctiques de Microsoft i facilita:

1. **Aplicació de GPOs diferents** per a usuaris i equips
2. **Delegació administrativa** per departaments
3. **Gestió de seguretat** més granular
4. **Organització lògica** segons funcions empresarials

### 2.2 Creació de la OU "usuaris"

![Diàleg creació OU usuaris](/T06/img_t06/captura8.png)

**Anàlisi**: Creem la primera OU principal per a organitzar tots els usuaris del domini:
- **Nom**: usuaris
- **Ubicació**: translogic01.test/ (arrel del domini)
- **Protecció**: ✅ Protect container from accidental deletion

**Justificació**: Separar els usuaris dels equips ens permet aplicar polítiques de grup diferents. La protecció contra eliminació accidental és una mesura de seguretat important.

### 2.3 Creació de la OU "equips"

![Diàleg creació OU equips](/T06/img_t06/captura9.png)

**Anàlisi**: Creem la segona OU principal per als equips del domini:
- **Nom**: equips
- **Ubicació**: translogic01.test/ (arrel del domini)
- **Protecció**: ✅ Protect container from accidental deletion

**Justificació**: Els equips necessiten polítiques de grup diferents dels usuaris (configuracions de sistema, restriccions d'aplicacions, etc.). Separar-los facilita la gestió.

### 2.4 Estructura inicial creada

![Estructura OUs creada](/T06/img_t06/captura10.png)

**Anàlisi**: Ara veiem les dues OUs principals creades a l'arrel del domini:
- **usuaris**: Per a tots els comptes d'usuari
- **equips**: Per a tots els ordinadors del domini

A la part dreta, el panell mostra que no hi ha elements dins d'aquestes OUs encara.

### 2.5 Creació de l'estructura jeràrquica dins de "usuaris"

**Decisió de disseny**: Dins de la OU "usuaris", creo una estructura jeràrquica que reflecteix l'organització departamental de l'empresa:

1. **gestio** - Departament de gestió administrativa
2. **magatzem** - Personal del magatzem i logística
3. **gerencia** - Direcció i gerència
4. **plantilles** - Per a plantilles d'usuari reutilitzables
5. **OU grups** - Per a grups de seguretat organitzats

#### 2.5.1 Creació de la OU "gestio"

![Creació OU gestio](/T06/img_t06/captura11.png)

**Anàlisi**: Creem la OU per al departament de gestió:
- **Nom**: gestio
- **Ubicació**: dins de translogic01.test/usuaris
- **Protecció**: ✅ Activat

#### 2.5.2 Creació de la OU "magatzem"

![Creació OU magatzem](/T06/img_t06/captura12.png)

**Anàlisi**: Creem la OU per al departament de magatzem:
- **Nom**: magatzem
- **Ubicació**: dins de translogic01.test/usuaris
- **Protecció**: ✅ Activat

#### 2.5.3 Creació de la OU "gerencia"

![Creació OU gerencia](/T06/img_t06/captura13.png)

**Anàlisi**: Creem la OU per al departament de gerència:
- **Nom**: gerencia
- **Ubicació**: dins de translogic01.test/usuaris
- **Protecció**: ✅ Activat

#### 2.5.4 Creació de la OU "plantilles"

![Creació OU plantilles](/T06/img_t06/captura14.png)

**Anàlisi**: Creem la OU específica per a plantilles d'usuari:
- **Nom**: plantilles
- **Ubicació**: dins de translogic01.test/usuaris
- **Protecció**: ✅ Activat

**Justificació**: Separar les plantilles dels usuaris reals facilita la gestió i evita confusions.

#### 2.5.5 Creació de la OU "OU grups"

![Creació OU grups](/T06/img_t06/captura15.png)

**Anàlisi**: Creem la OU per a grups de seguretat:
- **Nom**: OU grups
- **Ubicació**: dins de translogic01.test/usuaris
- **Protecció**: ✅ Activat

**Justificació**: Organitzar els grups en una OU específica millora l'administració i permet aplicar polítiques de gestió de grups.

### 2.6 Estructura completa de OUs

![Estructura completa OUs](/T06/img_t06/captura16.png)

**Anàlisi**: Ara tenim una estructura completa i ben organitzada:
- **Nivell 1** (arrel): usuaris i equips
- **Nivell 2** (dins usuaris): gestio, magatzem, gerencia, plantilles, OU grups

**Avantatges d'aquesta estructura**:
1. **Delegació fàcil**: Podem delegar control per cada OU departamental
2. **GPOs específiques**: Polítiques diferents per cada departament
3. **Gestió simplificada**: Usuaris similars agrupats junts
4. **Seguretat millorada**: Permisos aplicats a nivell d'OU

## 3. Creació dels grups d'Active Directory

### 3.1 Grups requerits per l'encàrrec

L'encàrrec especifica la creació de 4 grups:
1. **gestio** - Per al departament de gestió
2. **magatzem** - Per al personal del magatzem
3. **gerencia** - Per als gerents
4. **personal** - Grup global que contindrà tots els anteriors

### 3.2 Configuració dels grups

**Decisió de configuració**:
- **Group scope**: Global (visible a tot el domini)
- **Group type**: Security (per assignar permisos)
- **Ubicació**: Tots dins de OU=OU grups,OU=usuaris

#### 3.2.1 Creació del grup "gestio"

![Creació grup gestio](/T06/img_t06/captura17.png)

**Anàlisi**: Creem el primer grup:
- **Group name**: gestio
- **Group name (pre-Windows 2000)**: gestio (automàtic)
- **Group scope**: ● Global
- **Group type**: ● Security

**Justificació de Global Security group**:
- **Global groups**: Contenen usuaris del mateix domini
- **Security groups**: Per assignar permisos a recursos
- **Best practice**: Segueix el model AGDLP

#### 3.2.2 Creació del grup "magatzem"

![Creació grup magatzem](/T06/img_t06/captura18.png)

**Anàlisi**: Creem el segon grup:
- **Group name**: magatzem
- **Group name (pre-Windows 2000)**: magatzem
- **Group scope**: ● Global
- **Group type**: ● Security

#### 3.2.3 Creació del grup "gerencia"

![Creació grup gerencia](/T06/img_t06/captura19.png)

**Anàlisi**: Creem el tercer grup:
- **Group name**: gerencia
- **Group name (pre-Windows 2000)**: gerencia
- **Group scope**: ● Global
- **Group type**: ● Security

#### 3.2.4 Creació del grup "personal"

![Creació grup personal](/T06/img_t06/captura20.png)

**Anàlisi**: Creem el grup especial "personal":
- **Group name**: personal
- **Group name (pre-Windows 2000)**: personal
- **Group scope**: ● Global
- **Group type**: ● Security

**Funció especial del grup "personal"**:
Aquest grup actuarà com a grup "paraguas" que contindrà com a membres els altres tres grups (gestio, magatzem, gerencia). Això permet:
1. **Gestió simplificada**: Un sol grup per a tots els empleats
2. **Permisos globals**: Aplicar permisos comuns a tots els empleats
3. **Escalabilitat**: Afegir nous departaments fàcilment

### 3.3 Relació entre grups

**Estructura de grups**:
```
personal (grup global)
├── gestio (grup global)
├── magatzem (grup global)
└── gerencia (grup global)
```

**Avantatges d'aquesta estructura**:
1. **Gestió centralitzada**: Canvis aplicats a "personal" afecten tots els empleats
2. **Seguretat granular**: Permisos específics per departament
3. **Flexibilitat**: Nous departaments fàcilment integrats

---

## 4. Configuració de la relació entre grups

### 4.1 Verificació dels grups creats

![Llista de grups creats](/T06/img_t06/captura21.png)

**Anàlisi**: A la OU "OU grups" podem veure els quatre grups creats correctament:
- **gerencia**: Security Group - Global
- **gestio**: Security Group - Global  
- **magatzem**: Security Group - Global
- **personal**: Security Group - Global

Tots apareixen com a "Security Group..." indicant que són grups de seguretat i no de distribució.

### 4.2 Accés a les propietats del grup "personal"

![Propietats del grup personal](/T06/img_t06/captura22.png)

**Anàlisi**: Obtenim les propietats del grup "personal" per configurar-ne els membres. El panell mostra que el grup està ubicat a la OU "OU grups" dins de "usuaris".

### 4.3 Pestanya Members del grup personal

![Pestanya Members del grup personal](/T06/img_t06/captura23.png)

**Anàlisi**: A la pestanya "Members" del grup "personal" veiem que inicialment està buit. Cal afegir-hi els altres tres grups com a membres.

### 4.4 Diàleg per afegir membres al grup

![Diàleg per seleccionar objectes](/T06/img_t06/captura24.png)

**Anàlisi**: Quan cliquem "Add..." per afegir membres, ens apareix un diàleg on podem seleccionar els grups a afegir. Cal escriure "gerencia" i després fer clic a "Check Names" per verificar-lo.

### 4.5 Primer grup afegit: gerencia

![Grup gerencia afegit al personal](/T06/img_t06/captura25.png)

**Anàlisi**: Hem afegit el primer grup "gerencia" com a membre del grup "personal". Veiem que apareix a la llista de membres amb la seva ubicació completa: `translogic01.test/usuaris/OU grups`.

### 4.6 Tots els grups afegits

![Tots els grups afegits al personal](/T06/img_t06/captura26.png)

**Anàlisi**: Ara hem afegit els tres grups com a membres del grup "personal":
- **gerencia**: Grup dels gerents
- **gestio**: Grup del personal de gestió
- **magatzem**: Grup del personal del magatzem

**Justificació d'aquesta estructura**:
1. **Gestió simplificada**: Amb un sol grup ("personal") podem assignar permisos comuns a tots els empleats
2. **Jerarquia clara**: Els grups departamentals estan organitzats sota el grup principal
3. **Flexibilitat**: Si es crea un nou departament, només cal afegir el seu grup a "personal"

### 4.7 Vista global de l'estructura

![Vista global del Server Manager](/T06/img_t06/captura27.png)

**Anàlisi**: Tornem al Server Manager on veiem l'estructura completa:
- **usuaris** (amb totes les sub-OUs)
- **equips** (encara buit)
- **Esdeveniments**: Encara hi ha alguns warnings i errors que caldria investigar

## 5. Creació de les plantilles d'usuari

### 5.1 Justificació de les plantilles

**Objectiu**: Crear tres plantilles d'usuari que comencin amb "_" (subratllat) per a:
1. **_gestio**: Plantilla per a usuaris del departament de gestió
2. **_magatzem**: Plantilla per a usuaris del magatzem
3. **_gerencia**: Plantilla per a usuaris de gerència

**Avantatges de les plantilles**:
- **Estandardització**: Tots els usuaris d'un mateix departament tenen la mateixa configuració
- **Eficiència**: Creació ràpida de nous usuaris
- **Consistència**: Configuració uniforme de permisos i carpetes

### 5.2 Creació de la plantilla _gestio

#### 5.2.1 Informació bàsica

![Creació plantilla _gestio - Informació bàsica](/T06/img_t06/captura28.png)

**Anàlisi**: Creem la primera plantilla amb les següents dades:
- **First name**: TPL (Template)
- **Last name**: gestio
- **Full name**: TPL gestio
- **User logon name**: `TPL_gestio@translogic01.test`
- **Ubicació**: `translogic01.test/usuaris/plantilles`

**Convenció de noms**: Utilitzem el prefix "TPL_" per identificar clarament que es tracta de plantilles.

#### 5.2.2 Configuració de contrasenya

![Configuració de contrasenya plantilla _gestio](/T06/img_t06/captura29.png)

**Anàlisi**: Configurem la contrasenya i opcions de compte:
- **Password**: [establert]
- **Confirm password**: [confirmat]
- **Opcions**:
  - ☐ User must change password at next logon
  - ☐ User cannot change password
  - ☑ Password never expires
  - ☐ Account is disabled

**Justificació de les opcions**:
- **Password never expires**: Les plantilles són comptes inactius que no s'utilitzen per iniciar sessió
- **Account disabled**: Important desactivar les plantilles per seguretat

### 5.3 Creació de la plantilla _magatzem

![Creació plantilla _magatzem](/T06/img_t06/captura31.png)

**Anàlisi**: Creem la segona plantilla amb configuració similar:
- **First name**: TPL
- **Last name**: magatzem
- **Full name**: TPL magatzem
- **User logon name**: `TPL_magatzem@translogic01.test`
- **Ubicació**: `translogic01.test/usuaris/plantilles`

### 5.4 Creació de la plantilla _gerencia

![Creació plantilla _gerencia](/T06/img_t06/captura32.png)

**Anàlisi**: Creem la tercera plantilla:
- **First name**: TPL
- **Last name**: gerencia
- **Full name**: TPL gerencia
- **User logon name**: `TPL_gerencia@translogic01.test`
- **Ubicació**: `translogic01.test/usuaris/plantilles`

### 5.5 Verificació de les plantilles creades

![Llista de plantilles creades](/T06/img_t06/captura33.png)

**Anàlisi**: A la OU "plantilles" podem veure les tres plantilles creades:
1. **Tpl gerencia** - User
2. **Tpl gestio** - User  
3. **Tpl magatzem** - User

Totes apareixen com a objectes de tipus "User" i estan correctament ubicades a la OU de plantilles.

## 6. Configuració de les plantilles

### 6.1 Accés a les propietats de TPL gestio

![Propietats de TPL gestio](/T06/img_t06/captura34.png)

**Anàlisi**: Obtenim les propietats de la plantilla "TPL gestio" per configurar-ne la pertinença a grups i la carpeta personal.

### 6.2 Pestanya Member Of inicial

![Pestanya Member Of inicial](/T06/img_t06/captura35.png)

**Anàlisi**: A la pestanya "Member Of" veiem que la plantilla només pertany al grup "Domain Users" per defecte. Cal afegir-la al grup "gestio".

### 6.3 Diàleg per afegir al grup gestio

![Diàleg per afegir al grup gestio](/T06/img_t06/captura36.png)

**Anàlisi**: A l'afegir grups, escrivim "gestio" i fem clic a "Check Names" per verificar. El sistema reconeix el grup correctament.

### 6.4 Plantilla TPL gestio configurada

![Plantilla TPL gestio configurada](/T06/img_t06/captura37.png)

**Anàlisi**: Ara la plantilla "TPL gestio" pertany a dos grups:
1. **Domain Users**: Grup per defecte de tots els usuaris del domini
2. **gestio**: Grup específic del departament de gestió

**Primary group**: Continua sent "Domain Users" com és estàndard.

### 6.5 Plantilla TPL magatzem configurada

![Plantilla TPL magatzem configurada](/T06/img_t06/captura38.png)

**Anàlisi**: La plantilla "TPL magatzem" està configurada de manera similar:
1. **Domain Users**: Grup per defecte
2. **magatzem**: Grup específic del departament de magatzem

### 6.6 Plantilla TPL gerencia configurada

![Plantilla TPL gerencia configurada](/T06/img_t06/captura39.png)

**Anàlisi**: La plantilla "TPL gerencia" també està configurada correctament:
1. **Domain Users**: Grup per defecte
2. **gerencia**: Grup específic del departament de gerència

### 6.7 Resum de la configuració de plantilles

**Configuració completada per a les tres plantilles**:

1. **Plantilla _gestio**:
   - Username: `TPL_gestio`
   - Grups: Domain Users + gestio
   - Contrasenya: Establerta amb "Password never expires"
   - Estat: Compte desactivat

2. **Plantilla _magatzem**:
   - Username: `TPL_magatzem`
   - Grups: Domain Users + magatzem
   - Contrasenya: Establerta amb "Password never expires"
   - Estat: Compte desactivat

3. **Plantilla _gerencia**:
   - Username: `TPL_gerencia`
   - Grups: Domain Users + gerencia
   - Contrasenya: Establerta amb "Password never expires"
   - Estat: Compte desactivat

**Justificació de la configuració**:
- **Prefix TPL_**: Identifica clarament les plantilles
- **Grups específics**: Cada plantilla pertany al seu grup departamental
- **Comptes desactivats**: Per seguretat, les plantelles no poden iniciar sessió
- **Contrasenyes sense expiració**: Les plantilles no s'utilitzen activament

### 6.8 Preparació per a la creació de carpetes personals

![Explorador de fitxers](/T06/img_t06/captura40.png)

**Anàlisi**: Abans de configurar les carpetes personals a les plantilles, hem de preparar l'estructura de directoris al servidor. A l'explorador de fitxers veiem:
- **Disco local (C:)**: 8,22 GB lliures de 31,2 GB
- **Unitat D: (SSD_X)**: Potser un segon disc per a les carpetes personals

**Pla per a les carpetes personals**:
1. Crear una carpeta "Home" al disc D: (o al C: si no hi ha segon disc)
2. Configurar compartició de la carpeta amb permisos adequats
3. Configurar cada plantilla perquè tingui una carpeta personal dins d'aquesta estructura

---

## 7. Configuració de carpetes personals i permisos compartits

### 7.1 Preparació del disc per a carpetes home

![Explorador de fitxers - Opcions del disc](/T06/img_t06/captura41.png)

**Anàlisi**: A l'explorador de fitxers, estem preparant un disc per allotjar les carpetes personals dels usuaris. Veiem:
- **Disco local (C:)**: 8,22 GB lliures de 31,2 GB
- **Unitat D: (CD Drive)**: Conté un disc d'instal·lació (SSD_XMERE_EN-US_DV9)

**Decisió**: Utilitzarem el disc C: per crear la carpeta compartida "homes", ja que té suficient espai disponible.

### 7.2 Accés a propietats del disc C:

![Propietats del disc C:](/T06/img_t06/captura42.png)

**Anàlisi**: Obrim les propietats del disc C: i anem a la pestanya "Sharing". Veiem que actualment no hi ha cap carpeta compartida en aquest disc.

### 7.3 Configuració de compartició avançada

![Configuració de compartició avançada](/T06/img_t06/captura43.png)

**Anàlisi**: Configurem la compartició avançada de la carpeta:
- ☑ **Share this folder**: Activem la compartició
- **Share name**: `homes` (nom de la carpeta compartida)
- **Limit users**: 16777 (màxim permès per Windows)

**Justificació del nom "homes"**: És un nom estàndard per a carpetes personals, fàcil de recordar i identificar.

### 7.4 Configuració inicial de permisos compartits

![Permisos compartits inicials](/T06/img_t06/captura44.png)

**Anàlisi**: Per defecte, el sistema assigna el grup "Everyone" amb permisos de lectura. Això NO és segur i cal canviar-ho.

### 7.5 Selecció del grup Domain Users

![Selecció del grup Domain Users](/T06/img_t06/captura45.png)

**Anàlisi**: Eliminem "Everyone" i afegim el grup "Domain Users". Aquest grup conté tots els usuaris del domini i és més segur.

### 7.6 Permisos compartits configurats

![Permisos compartits configurats](/T06/img_t06/captura46.png)

**Anàlisi**: Ara tenim configurats els permisos compartits:
- **Group or user names**: `Domain Users (TRANSLOGIC01\Domain Users)`
- **Permissions**: 
  - ☑ Allow - Read
  - ☑ Allow - Change
  - ☐ Allow - Full Control

**Justificació dels permisos**:
- **Read**: Permet llegir contingut
- **Change**: Permet crear, modificar i eliminar fitxers en la seva pròpia carpeta
- **Sense Full Control**: Per seguretat, els usuaris no poden canviar permisos

### 7.7 Accés a les propietats de les plantilles

![Llista de plantilles](/T06/img_t06/captura47.png)

**Anàlisi**: Tornem a Active Directory Users and Computers per configurar les carpetes personals a les plantilles. Veiem les tres plantilles creades: TPL gerencia, TPL gestio i TPL magatzem.

### 7.8 Configuració de carpeta home per a TPL gestio

![Propietats de TPL gestio - Pestanya Profile](/T06/img_t06/captura48.png)

**Anàlisi**: Obrim les propietats de "TPL gestio" i anem a la pestanya "Profile" per configurar la carpeta personal.

![Configuració de carpeta home TPL gestio](/T06/img_t06/captura49.png)

**Anàlisi**: A la secció "Home folder" configurem:
- [ ] Local path: (sense marcar)
- [x] Connect: H: (assignem la unitat H:)
- To: `\\DC01\homes\TPL_gestio`

**Configuració correcta**:
- **Unitat**: H: (assignació lògica per a home)
- **Ruta**: `\\DC01\homes\TPL_gestio`
  - `\\DC01`: Nom del servidor
  - `\homes`: Carpeta compartida
  - `\TPL_gestio`: Subcarpeta específica per a aquesta plantilla

### 7.9 Configuració de carpeta home per a TPL magatzem

![Configuració de carpeta home TPL magatzem](/T06/img_t06/captura51.png)

**Anàlisi**: Configurem de manera similar la plantilla TPL magatzem:
- [ ] Local path: (sense marcar)
- [x] Connect: H: 
- To: `\\DC01\homes\TPL_magatzem`

### 7.10 Verificació de la configuració

![Vista de les plantilles](/T06/img_t06/captura52.png)

**Anàlisi**: Totes les plantilles estan configurades amb les seves carpetes personals corresponents.

**Resum de la configuració de carpetes home**:
1. **Carpeta compartida**: `\\DC01\homes`
2. **Permisos compartits**: Domain Users amb Read + Change
3. **Subcarpetes individuals**: 
   - `\\DC01\homes\TPL_gestio`
   - `\\DC01\homes\TPL_magatzem`
   - `\\DC01\homes\TPL_gerencia`
4. **Unitat assignada**: H: per a totes les plantilles

## 8. Creació d'usuaris de prova a partir de les plantilles

### 8.1 Procés de còpia de plantilles

**Mètode**: Utilitzem la funció "Copy" per crear usuaris reals a partir de les plantilles.

![Còpia de plantilla per crear usuari prova_gestio](/T06/img_t06/captura53.png)

**Anàlisi**: Copiem la plantilla "TPL gestio" per crear l'usuari de prova:
- **First name**: prova
- **Last name**: gestio
- **Full name**: prova gestio
- **User logon name**: `prova_gestio@translogic01.test`

**Convenció de noms**: Utilitzem el prefix "prova_" per identificar els usuaris de prova.

### 8.2 Configuració de contrasenya per a l'usuari de prova

![Configuració de contrasenya prova_gestio](/T06/img_t06/captura54.png)

**Anàlisi**: Configurem la contrasenya amb opcions diferents de les plantilles:
- **Password**: [establerta]
- **Opcions**:
  - ☑ User must change password at next logon
  - ☐ User cannot change password
  - ☐ Password never expires
  - ☐ Account is disabled

**Justificació**:
- **Must change password**: Millor pràctica de seguretat
- **Compte actiu**: A diferència de les plantilles, els usuaris de prova han de poder iniciar sessió

### 8.3 Resum de la creació

![Resum de creació prova_gestio](/T06/img_t06/captura55.png)

**Anàlisi**: El sistema mostra el resum de la creació:
- **Copy from**: TPL gestio
- **Full name**: prova gestio
- **User logon name**: `prova_gestio@translogic01.test`
- **The user must change the password at next logon**

### 8.4 Creació de prova_gerencia

![Creació de prova_gerencia](/T06/img_t06/captura56.png)

**Anàlisi**: Creem el segon usuari de prova a partir de la plantilla TPL gerencia:
- **First name**: prova
- **Last name**: gerencia
- **User logon name**: `prova_gerencia@translogic01.test`

### 8.5 Creació de prova_magatzem

![Creació de prova_magatzem](/T06/img_t06/captura57.png)

**Anàlisi**: Creem el tercer usuari de prova a partir de la plantilla TPL magatzem:
- **First name**: prova
- **Last name**: magatzem
- **User logon name**: `prova_magatzem@translogic01.test`

### 8.6 Verificació dels usuaris creats

![Llista d'usuaris creats](/T06/img_t06/captura58.png)

**Anàlisi**: A la OU "plantilles" ara tenim 6 objectes:
- **3 plantilles**: TPL gerencia, TPL gestio, TPL magatzem
- **3 usuaris de prova**: prova gerencia, prova gestio, prova magatzem

**Observació important**: Els usuaris de prova s'han creat a la mateixa OU que les plantilles. Segons les millors pràctiques, haurien d'estar a les OUs departamentals corresponents (gestio, magatzem, gerencia).

### 8.7 Preparació per a la creació de l'equip PC1

![Menú de creació d'objectes](/T06/img_t06/captura59.png)

**Anàlisi**: Ara anem a crear l'equip PC1. A la OU "equips", fem clic dret i seleccionem New → Computer.

### 8.8 Creació de l'equip PC1

![Creació de l'equip PC1](/T06/img_t06/captura60.png)

**Anàlisi**: Configurem l'equip PC1:
- **Computer name**: PC1
- **Computer name (pre-Windows 2000)**: PC1
- **Ubicació**: `translogic01.test/equips`
- **Permís per unir-se al domini**: Domain Admins (per defecte)

**Configuració correcta**: L'equip es crea a la OU "equips", separant clarament els equips dels usuaris.

---

## 9. Creació i configuració de la VM Windows 11

### 9.1 Creació de la màquina virtual PC1

![Creació de la VM PC1 - Nom i Sistema Operatiu](/T06/img_t06/captura61.png)

**Anàlisi**: Estem creant la màquina virtual PC1 amb VirtualBox amb les següents especificacions:
- **Nom**: PC1
- **Sistema operatiu**: Windows 11 Enterprise Evaluation (10.0.26200.6584 / x64 / es-ES)
- **ISO**: Windows11.iso
- **Skip Unattended Installation**: Activada (instal·lació manual)

**Especificacions segons l'encàrrec**: Windows 11 amb 4 GB de RAM.

### 9.2 Configuració de maquinari de la VM

![Configuració de maquinari de la VM](/T06/img_t06/captura62.png)

**Anàlisi**: Configurem els recursos de maquinari:
- **Memòria**: 4096 MB (4 GB) - Exactament com demana l'encàrrec
- **Processadors**: 4 CPUs
- **Enable EFI**: Activada per a Windows 11

### 9.3 Configuració del disc dur virtual

![Configuració del disc dur virtual](/T06/img_t06/captura63.png)

**Anàlisi**: Configurem l'emmagatzematge:
- **Tipus de disc**: VDI (VirtualBox Disk Image)
- **Ubicació**: `C:\Users\cfgm2smxa01\Documents\PC1\PC1.vdi`
- **Mida**: 40,00 GB - Disc suficient com demana l'encàrrec

**Configuració correcta**: La VM té els recursos especificats (4 GB RAM i disc suficient).

### 9.4 Configuració de xarxa de la VM

![Configuració de xarxa de la VM](/T06/img_t06/captura64.png)

**Anàlisi**: Configurem la xarxa de la VM:
- **Adaptador 1**: Habilitat
- **Connectat a**: Xarxa NAT - Com especifica l'encàrrec
- **Tipus d'adaptador**: Intel PRO/1000 MT Desktop (82540EM)
- **Cable connectat**: Sí

**Configuració correcta**: La xarxa està en mode NAT com demana l'encàrrec.

### 9.5 Instal·lació de Windows 11

![Instal·lació de Windows 11](/T06/img_t06/captura65.png)

**Anàlisi**: La instal·lació de Windows 11 està en progrés (7% completat). El procés pot trigar uns minuts i el PC es reiniciarà diverses vegades.

### 9.6 Configuració de DNS al client

![Configuració de DNS al client](/T06/img_t06/captura66.png)

**Anàlisi**: Després de la instal·lació, configurem la xarxa del client:
- **DNS preferit**: 10.0.2.17 (el servidor DC01)
- **IPv6**: Desactivat

Aquesta configuració és crucial perquè el client pugui resoldre els noms del domini.

### 9.7 Configuració detallada de DNS

![Propietats de TCP/IPv4](/T06/img_t06/captura67.png)

**Anàlisi**: Configurem manualment el DNS:
- ☐ Obtener una dirección IP automáticamente
- ☐ Obtener la dirección del servidor DNS automáticamente
- ☑ Usar las siguientes direcciones de servidor DNS:
  - **Servidor DNS preferido**: 10.0.2.17

**Justificació**: Cal apuntar al servidor DC01 perquè pugui resoldre el domini translogic01.test.

### 9.8 Informació del sistema del client

![Informació del sistema del client](/T06/img_t06/captura68.png)

**Anàlisi**: El client Windows 11 està instal·lat correctament:
- **Nom del dispositiu**: DESKTOP-5BCTF15
- **RAM instal·lada**: 3,98 GB
- **Sistema**: Windows 11 Enterprise Evaluation 25H2

Actualment està en grup de treball WORKGROUP.

### 9.9 Propietats del sistema

![Propietats del sistema](/T06/img_t06/captura69.png)

**Anàlisi**: Accedim a les propietats del sistema per canviar el nom i unir-nos al domini. Veiem:
- **Nom complet de l'equip**: DESKTOP-5BCTF15
- **Grup de treball**: WORKGROUP

### 9.10 Diàleg per unir-se al domini

![Diàleg per unir-se al domini](/T06/img_t06/captura70.png)

**Anàlisi**: Configurem la unió al domini:
- **Nom de l'equip**: DESKTOP-5BCTF15
- **Miembro del**: ○ Dominio: `translogic01.test`

### 9.11 Autenticació per unir-se al domini

![Autenticació per unir-se al domini](/T06/img_t06/captura71.png)

**Anàlisi**: Introduïm les credencials d'administrador del domini:
- **Nom d'usuari**: Administrator
- **Contrasenya**: [contrasenya d'administrador]

### 9.12 Confirmació d'unió al domini

![Confirmació d'unió al domini](/T06/img_t06/captura72.png)

**Anàlisi**: **Èxit!** El client s'ha unit correctament al domini translogic01.test.

## 10. Prova d'accés amb els usuaris de prova

### 10.1 Inici de sessió amb prova_gestio

![Pantalla d'inici de sessió amb prova_gestio](/T06/img_t06/captura73.png)

**Anàlisi**: A la pantalla d'inici de sessió de Windows, seleccionem "Un altre usuari" i introduïm:
- **Usuari**: `translogic01.test\prova_gestio`
- **Domini**: translogic01.test

Això demostra que el domini està accessible des del client.

### 10.2 Sessió iniciada amb prova_gestio

![Sessió iniciada amb prova_gestio](/T06/img_t06/captura74.png)

**Anàlisi**: **Èxit!** L'usuari prova_gestio ha iniciat sessió correctament. Veiem:
- **Nom d'usuari**: prova gestio (sense el prefix "translogic01.test\")
- **Unitat de xarxa assignada**: H: (carpeta home)

### 10.3 Accés a la carpeta personal de prova_gestio

![Explorador amb carpeta personal de prova_gestio](/T06/img_t06/captura75.png)

**Anàlisi**: A l'explorador de fitxers, veiem que s'ha mapejat correctament la unitat H::
- **Ubicacions de xarxa**: `prova_gestio (\\DC01\homes) (H:)`
- **Espai disponible**: 8,22 GB disponibles de 31,2 GB

**Configuració correcta**: La carpeta personal s'ha creat automàticament i s'ha mapejat com a unitat H:.

### 10.4 Inici de sessió amb prova_gerencia

![Pantalla d'inici amb prova_gerencia](/T06/img_t06/captura76.png)

**Anàlisi**: Tancem sessió i provem amb un altre usuari:
- **Usuari**: `translogic01.test\prova_gerencia`

### 10.5 Sessió iniciada amb prova_gerencia

![Sessió iniciada amb prova_gerencia](/T06/img_t06/captura77.png)

**Anàlisi**: **Èxit!** prova_gerencia també inicia sessió correctament. El perfil d'usuari es crea automàticament.

### 10.6 Inici de sessió amb prova_magatzem

![Explorador amb carpeta personal de prova_magatzem](/T06/img_t06/captura78.png)

**Anàlisi**: Després d'iniciar sessió amb prova_magatzem, veiem a l'explorador:
- **Ubicacions de xarxa**: `prova_magatzem (\\DC01\homes) (H:)`

Cada usuari té la seva pròpia carpeta personal dins de \\DC01\homes.

### 10.7 Confirmació final de prova_magatzem

![Sessió de prova_magatzem](/T06/img_t06/captura79.png)

**Anàlisi**: prova_magatzem també ha iniciat sessió correctament i té accés a la seva carpeta personal.

---

# **CONCLUSIÓ FINAL DE LA TASCA 06**

La Tasca 06 s'ha completat amb èxit, implementant un domini Active Directory completament funcional amb tots els elements requerits. S'ha creat una estructura organitzativa jeràrquica amb OUs per a usuaris (organitzats per departaments: gestió, magatzem, gerència) i equips. Els quatre grups sol·licitats s'han creat correctament, amb el grup "personal" contenint els altres tres.

S'han configurat permisos compartits i NTFS per a les carpetes personals a `\\DC01\homes`, i creades tres plantilles d'usuari amb prefix "_" configurades amb pertinença als grups i carpeta personal. A partir d'aquestes, s'han generat usuaris de prova per a cada departament.

L'equip PC1 s'ha preaprovisionat a la OU d'equips i s'ha afegit al domini des d'una VM Windows 11 amb 4GB RAM i xarxa NAT. Finalment, s'han realitzat proves d'accés exitoses amb els tres usuaris de prova, verificant l'accés a les carpetes personals.

Tots els criteris d'avaluació s'han complert, resultant en una implementació professional i completa del domini.