# Servidor d'Impressió amb Printer Pooling i GPO

Aquest projecte documenta la implementació completa d'un **servidor d'impressió a Windows Server** utilitzant **Printer Pooling** per balancejar la càrrega entre dues impressores virtuals (simulades amb PDF24). El desplegament als clients es realitza automàticament mitjançant **GPO** (Group Policy Object), i s'hi afegeixen restriccions horàries i de seguretat per grups.

## 📌 Objectiu

Configurar un entorn d'impressió d'alta disponibilitat per a un magatzem logístic, on el volum d'impressió d'albarans és crític. Si una impressora falla, l'altra assumeix la càrrega sense interrupció, evitant aturades a la cadena de fred.

## 🧱 Tecnologies utilitzades

- **Windows Server 2025** (Controlador de domini)
- **Windows 11** (client unit al domini)
- **PDF24 Creator** (simulació d'impressores virtuals)
- **Active Directory** (gestió d'usuaris i grups)
- **Group Policy Management** (desplegament automàtic)
- **Print Management** (configuració del servidor d'impressió)

## 🚀 Fases d'implementació

### 1. Preparació de l'entorn i simulació de maquinari
- Instal·lació de **PDF24 Creator** al servidor.
- Creació de dues impressores virtuals amb noms corporatius:  
  `IMP_MAGATZEM_A` i `IMP_MAGATZEM_B`.
- Configuració de carpetes de sortida automàtica:
  - `C:\SortidaA` per a la impressora A
  - `C:\SortidaB` per a la impressora B

### 2. Instal·lació del rol i configuració del Printer Pooling
- Addició del rol **Print and Document Services** (només **Print Server**).
- Obertura de la consola **Print Management**.
- A les propietats de `IMP_MAGATZEM_A`:
  - Pestanya **Ports** → marcar **Enable printer pooling**.
  - Seleccionar els ports de les dues impressores (A i B).
- Compartir la impressora a la xarxa (pestanya **Sharing**).

### 3. Desplegament automàtic mitjançant GPO
- Creació de la GPO `GPO_Impressores_Magatzem`.
- Des de **Print Management** → **Deploy with Group Policy**:
  - Vincular la GPO a la OU corresponent.
  - Desplegar **per màquina** (per machine).
- Al client: `gpupdate /force` i reinici de sessió.
- Verificació que la impressora apareix automàticament.

### 4. Proves de càrrega i seguretat
- Enviament de **10 documents** a la impressora del pool.
- Comprovació del balanceig: els PDF es reparteixen entre `SortidaA` i `SortidaB`.
- Configuració de **restricció horària** (de 06:00 a 22:00) a la pestanya **Advanced**.
- (Opcional) Creació d'una tercera impressora `IMP_RESTRINGIDA` i d'un grup de seguretat `Grup_Impressio_Especial` per limitar l'accés només als membres del grup.

