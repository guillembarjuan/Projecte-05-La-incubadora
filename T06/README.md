# 🖥️ T06 – Configuració del domini

## 📝 Descripció

En aquesta tasca desplego el domini creat prèviament, definint la seva estructura interna: unitats organitzatives (OU), grups, usuaris i equips. L’objectiu és organitzar correctament els objectes del domini i comprovar-ne el funcionament en un entorn real.

---

## 🎯 Objectius

- Crear una estructura coherent d’Unitats Organitzatives (OU).
- Definir grups i relacions de pertinença.
- Crear plantilles d’usuari amb configuració predefinida.
- Aprovisionar un equip client i unir-lo al domini.
- Verificar el correcte funcionament iniciant sessió amb diferents usuaris.

---

## 🏗️ Estructura del domini

### 📂 Unitats Organitzatives (OU)

He creat una estructura organitzada separant:

- **OU Usuaris**
- **OU Grups**
- **OU Equips**

Aquesta estructura facilita la gestió, l’aplicació de polítiques (GPO) i l’organització per rols dins l’empresa.

---

## 👥 Grups creats

He definit els següents grups de seguretat:

- `gestio`
- `magatzem`
- `gerencia`
- `personal` (grup pare)

Els grups **gestio, magatzem i gerencia** són membres del grup **personal**, permetent una gestió jeràrquica i més eficient dels permisos.

---

## 👤 Plantilles d’usuari

He creat una plantilla per a cada departament:

- Plantilla Gestio
- Plantilla Magatzem
- Plantilla Gerencia

Cada plantilla inclou:
- Pertinença automàtica al grup corresponent.
- Creació de carpeta personal.
- Configuració bàsica comuna del perfil.

A partir d’aquestes plantilles he creat un usuari de prova per a cada departament.

---

## 💻 Equip client

He creat una màquina virtual amb:

- **Windows 11**
- **4 GB de RAM**
- Xarxa en mode **NAT**

L’equip, anomenat `PC1`, s’ha afegit correctament al domini dins la OU **Equips**.

---

## ✅ Comprovacions

He verificat el funcionament del domini:

- Iniciant sessió a `PC1` amb els tres usuaris de prova.
- Comprovant la creació de carpetes personals.
- Validant la pertinença correcta als grups.
- Confirmant l’autenticació correcta contra el controlador de domini.

---

## 📚 Materials de suport

- UD6.AA3 – Desplegament (Moodle 0224 SOX)

---

## 🏁 Resultat

He desplegat correctament l’estructura del domini, aplicant una organització coherent i comprovant el funcionament real amb usuaris i equips integrats al domini.
