Aquí tens l'informe complet en **format Markdown**, estructurat pas a pas amb totes les captures que m'has proporcionat.

---

# Informe Tècnic: Infraestructura de Fitxers Segura per a FoodLogistic

## 1. Resum de Configuració

| Carpeta | Camí UNC | Grup amb accés | Mètode de creació |
| :--- | :--- | :--- | :--- |
| **Public** | `\\FoodLogistic\Public` | `Domain Users` | Explorador de fitxers |
| **Operacions** | `\\FoodLogistic\Operacions` | `Transport` | Server Manager (FSSM) |
| **Direcció$** | `\\FoodLogistic\Direccio$` | `Direccio` | PowerShell |

---

## 2. Evidències de Configuració

### 2.1. Fita 1: Preparació i Seguretat de Grups (Active Directory)

Es crea l'estructura d'Unitats Organitzatives (OUs) dins del domini `foodlogistic.test` per organitzar els usuaris i grups de FoodLogistic.

![Estructura d'OUs dins d'Active Directory](IMG/1.png)

Es crea el grup de seguretat `Administracio` dins de la OU `Grups`.

![Creació del grup Administracio](IMG/2.png)

Es crea el grup de seguretat `Transport`.

![Creació del grup Transport](IMG/3.png)

Es crea el grup de seguretat `Direccio`.

![Creació del grup Direccio](IMG/4.png)

### 2.2. Fita 2: Implementació de Recursos Compartits

#### A. Carpeta Public (Mètode: Explorador de fitxers)

Es crea la carpeta `C:\Public` des de l'Explorador de fitxers.

![Carpeta Public creada al disc C:](IMG/5.png)

S'assignen permisos NTFS al grup `Domain Users` amb **Modificar**.

![Permisos NTFS de Public - Afegir Domain Users](IMG/6.png)

Es comparteix la carpeta amb permisos SMB de **Lectura** per a `Everyone`.

![Permisos SMB de Public - Lectura per a Everyone](IMG/7.png)

#### B. Carpeta Operacions (Mètode: Server Manager - FSSM)

Es crea la carpeta `C:\Operacions` al servidor.

![Carpeta Operacions creada](IMG/8.png)

S'obre l'assistent **New Share** al **File and Storage Services**.

![Assistent New Share - Perfil SMB Share - Quick](IMG/9.png)

Se selecciona el volum `C:` com a ubicació del recurs.

![Selecció del volum C:](IMG/10.png)

S'especifica el nom del recurs `Operacions` i la ruta local `C:\Shares\Operacions`.

![Nom del recurs i ruta local](IMG/11.png)

S'activa **Access-Based Enumeration** perquè els usuaris només vegin les carpetes a les quals tenen accés.

![Habilitar Access-Based Enumeration](IMG/12.png)

S'assignen permisos NTFS al grup `Transport` amb **Full Control**.

![Afegir grup Transport amb Full Control](IMG/13.png)

Vista final dels permisos NTFS assignats a `Transport`.

![Permisos NTFS confirmats per a Transport](IMG/14.png)

Resum de la configuració abans de crear el recurs.

![Resum de configuració del recurs Operacions](IMG/15.png)

#### C. Carpeta Direcció$ (Mètode: PowerShell)

Es crea el recurs compartit ocult `Direccio$` amb PowerShell utilitzant el cmdlet `New-SmbShare`.

![Creació del recurs ocult amb PowerShell](IMG/17.png)

Es crea una GPO anomenada `Map Z Drive Direccio` per mapejar la unitat `Z:`.

![Creació de la GPO per mapejar Z:](IMG/18.png)

Es configura la unitat mapejada amb acció `Update`, lletra `Z:` i ubicació `\\FoodLogistic\Direccio$`.

![Configuració de la unitat mapejada Z:](IMG/19.png)

S'activa **Item-level targeting** perquè la GPO només s'apliqui als membres del grup `Direccio`.

![Item-level targeting - Grup Direccio](IMG/20.png)

### 2.3. Fita 3: Control d'Emmagatzematge (FSRM i Quotes NTFS)

#### Quotes NTFS

S'activen les quotes NTFS al volum `C:` amb un límit de **500 MB** per defecte.

![Configuració de quotes NTFS al volum C:](IMG/21.png)

#### Instal·lació de FSRM

S'instal·la el rol **File Server Resource Manager** des de l'assistent d'afegir rols.

![Selecció del rol FSRM](IMG/22.png)

Procés d'instal·lació del rol FSRM.

![Progrés de la instal·lació de FSRM](IMG/23.png)

Instal·lació completada correctament.

![Instal·lació de FSRM completada](IMG/24.png)

#### Quota de Carpeta (FSRM) a Public

Es crea una quota personalitzada a `C:\Public` amb un límit de **200 MB** (Hard Quota).

![Creació de quota a Public](IMG/25.png)

Es configura un avís al **90%** de l'espai amb un missatge personalitzat.

![Configuració del missatge d'avís de quota](IMG/27.png)

Es desa la quota sense crear una plantilla nova.

![Desar quota sense plantilla](IMG/28.png)

#### Filtratge de Fitxers (FSRM) a Operacions

Es configura un **File Screen** actiu a `C:\Operacions` per bloquejar **Executable Files** i **Audio and Video Files**.

![Configuració del File Screen - Grups bloquejats](IMG/29.png)

Es configura una notificació per correu electrònic amb un missatge d'avís de seguretat.

![Configuració del missatge de correu per bloqueig](IMG/30.png)

Resum de la configuració del File Screen abans de crear-lo.

![Resum del File Screen](IMG/31.png)

Es desa el File Screen sense crear plantilla.

![Desar File Screen sense plantilla](IMG/32.png)

Vista de la quota aplicada a `C:\Public` a la consola FSRM.

![Quota aplicada a Public](IMG/34.png)

---

## 3. Proves de Funcionament

### 3.1. Verificació amb l'usuari `u_xofer` (Grup `Transport`)

Inici de sessió al client amb l'usuari `u_xofer`.

![Inici de sessió amb u_xofer](IMG/35.png)

En accedir a `\\FoodLogistic`, l'usuari veu les carpetes `Public` i `Operacions`. La carpeta `Direccio$` roman oculta.

![Recursos visibles per a u_xofer](IMG/36.png)

En intentar accedir manualment a `\\FoodLogistic\Direccio$`, el sistema mostra un missatge d'**Accés denegat**.

![Error d'accés denegat a Direccio$](IMG/37.png)

En intentar copiar un fitxer executable (`notepad.exe`) a `\\FoodLogistic\Operacions`, el sistema mostra un error indicant que l'accés no està permès (bloqueig FSRM).

![Error en copiar executable a Operacions](IMG/46.png)

### 3.2. Verificació amb l'usuari `u_gerent` (Grup `Direccio`)

Inici de sessió al client amb l'usuari `u_gerent`.

![Inici de sessió amb u_gerent](IMG/38.png)

En obrir **Aquest equip**, apareix automàticament la unitat `Z:` mapejada al recurs `\\FoodLogistic\Direccio$`.

![Unitat Z: mapejada automàticament](IMG/40.png)

En intentar accedir a `\\FoodLogistic\Operacions`, el sistema denega l'accés perquè `u_gerent` no pertany al grup `Transport`.

![Error d'accés denegat a Operacions](IMG/41.png)

Accés permès a la carpeta `Public`.

![Accés permès a Public](IMG/42.png)

---

## 4. Conclusions

S'ha implementat amb èxit una infraestructura de fitxers segura per a FoodLogistic que compleix els següents requisits:

- **Estructura organitzativa a Active Directory** amb OUs i grups de seguretat (`Administracio`, `Transport`, `Direccio`).
- **Recursos compartits** creats mitjançant tres mètodes diferents: Explorador de fitxers, Server Manager i PowerShell.
- **Access-Based Enumeration** activat a la carpeta `Operacions`.
- **Recurs ocult** `Direccio$` accessible només per al grup `Direccio`.
- **GPO** que mapeja automàticament la unitat `Z:` per als membres de `Direccio`.
- **Quotes NTFS** aplicades al volum `C:` amb límit de 500 MB per usuari.
- **Quota FSRM** a `Public` amb límit estricte de 200 MB i avís al 90%.
- **Filtratge actiu de fitxers** a `Operacions` que bloqueja executables i fitxers multimèdia.

Les proves de funcionament realitzades des del client confirmen que els controls d'accés, les quotes i les restriccions operen correctament segons els requeriments de l'activitat.