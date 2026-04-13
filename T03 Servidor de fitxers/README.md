
# Servidor de Fitxers Segur - FoodLogistic

## Introducció

En el context del creixement empresarial de FoodLogistic, la gestió descentralitzada de dades ha generat inconsistencies operacionals. Aquest projecte implementa una infraestructura de fitxers centralitzada, segura i amb control d'espai mitjançant permisos NTFS/SMB, quotes i filtratge avançat de recursos (FSRM).

## Objectius

Implementar i demostrar el domini de tres metodologies d'administració:
- Explorador de fitxers
- Server Manager
- PowerShell

## Estructura del Projecte

### 1. Preparació d'Active Directory
Creació d'una estructura de grups de seguretat al domini `foodlogistic.test`:
- **Administracio**: Gestió de factures i albarans
- **Transport**: Xofers i caps de flota
- **Direccio**: Gerència

### 2. Recursos Compartits (Tres Mètodes)

| Carpeta | Mètode | Accés | Permisos |
|---------|--------|-------|---------|
| Public | Explorador | Tots | SMB: Lectura / NTFS: Modificació |
| Operacions | Server Manager | Transport | ABE habilitat |
| Confidencial | PowerShell | Direccio | Oculta ($) |

### 3. Control d'Emmagatzematge

- **Quotes NTFS**: 500 MB per usuari (volum de dades)
- **FSRM Quota**: 200 MB hard quota a Public (avís 90%)
- **Filtrat**: Bloqueig de `.exe`, `.msi` i fitxers multimèdia a Operacions

### 4. Verificació i Auditoria

Proves de funcionament des de client Windows 10/11 validant accessos, restriccions i filtratge.
