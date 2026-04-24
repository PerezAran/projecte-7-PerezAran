[Ir al inicio del Repositorio](./documentacion)https://github.com/classesSMX2n/projecte-7-PerezAran/tree/main/T01%20Coneixement%20la%20compet%C3%A8ncia%20i%20el%20sector
)
# T01: Coneixent la competència i el sector

## 📌 Breu descripció

Aquest treball analitza el sector dels serveis informàtics a Mataró i el Maresme, identificant la competència, la seva estructura organitzativa i definint una estratègia per a la nostra nova empresa de serveis informàtics davant d’un client potencial: **FoodLogístic S.A.**

---

## 🧭 Fase 1: Coneixent el terreny i la competència

### 1. Recerca de mercat: 3 empreses reals a Mataró o rodalies

| Empresa | Ubicació | Mida | Tipus de serveis |
|---------|----------|------|------------------|
| **Tècnics Mataró** | Mataró (Centre) | Microempresa (2-5 treballadors) | Manteniment d’equips, reparació, suport a domicili, xarxes petites. |
| **Maresme Informàtica** | Mataró (Via Europa) | PIME (10-15 treballadors) | Infraestructura TI, serveis al núvol, manteniment preventiu, suport a empreses. |
| **Systech Solutions** | Vilassar de Dalt (Maresme) | PIME (8-12 treballadors) | Desenvolupament de software a mida, ERP, seguretat informàtica i xarxes avançades. |

---

### 2. Organigrama d’una empresa tipus del sector

Prenem com a referència **Maresme Informàtica** (PIME de 10-15 treballadors) per definir un organigrama lògic.

#### Codi PlantUML

```plantuml
@startuml
!theme plain
title Organigrama - Empresa de Serveis Informàtics (PIME tipus)

rectangle "Direcció General" as DG

rectangle "Departament Comercial" as COM
rectangle "Departament Tècnic" as TEC
rectangle "Departament Administració i RRHH" as ADM

DG -down-> COM
DG -down-> TEC
DG -down-> ADM

COM -down-> "Responsable comercial"
COM -down-> "Tècnic comercial (pre-sales)"

TEC -down-> "Responsable de sistemes"
TEC -down-> "Equip de suport (helpdesk)"
TEC -down-> "Equip de xarxes i cloud"

ADM -down-> "Administratiu/Financer"
ADM -down-> "Recursos Humans (externalitzat)"

@enduml


[Ir al inicio del Repositorio](./documentacion)https://github.com/classesSMX2n/projecte-7-PerezAran/tree/main/T01%20Coneixement%20la%20compet%C3%A8ncia%20i%20el%20sector
)
* [Ver la carpeta de Documentación](./documentacion)https://github.com/classesSMX2n/projecte-7-PerezAran/tree/main/T01%20Coneixement%20la%20compet%C3%A8ncia%20i%20el%20sector
