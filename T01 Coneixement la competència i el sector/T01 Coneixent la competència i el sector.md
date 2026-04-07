# Fase 1: Coneixement el terremy i la competència 

## 1. Recerca de mercat: 3 Competidors al Maresme

### Empresa 1: JSM Inforedes, S.L

Aquesta Empresa s´ubica al Polígon Balançó i Boter, a Mataró, es una empresa PIME petita.

Es dedica al manteniment, cloud, ciberseguretat i al programari de gestió. 

IMG

### Empresa 2: ESED (ciberseguretat)

Aquesta empresa s´ubica a Mataró (tecnocampus), es una empresa PIME especialitzada.

Aquesta empresa es dedica a la ciberseguretat pura: Hacking ètic, serveis gestionats, protecció de dades.

IMG

### Empresa 3: Grup Qualitat

Aquesta empresa té varias seus per tot al maresma, es una empresa PIME mitjana.

Es dediquen a la consultoria i sololucions TIC per la logística i administracions públiques. Són els mes importants de la comarca del maresme.

IMG

## 2. Organigrama:

Hem triat JSM inforedes com a model perquè es l´estructura més habitual  en una PIME de serveis informàtics d´uns 10 a 15 treballadors. Aqui deixem al codi PlanUML la pàgina web per veurel de manera gràfica:

Enllaç: https://www.plantuml.com/plantuml/uml/SyfFKj2rKt3CoKnELR1Io4ZDoSa700001

Codi ornanigrama:

 @startuml
!theme plain
title Organigrama - Empresa de Serveis Informàtics (PIME tipus a Mataró)

' Definició dels nodes
rectangle "Direcció General / Propietari" as Dir
rectangle "Administració\n(Finances i RRHH)" as Admin
rectangle "Cap de Sistemes i Xarxes" as CapTecnic
rectangle "Cap de Projectes / CTO" as CapProjectes
rectangle "Departament Comercial\n(Vendes i Màrqueting)" as Comercial

' Sub-departaments tècnics
rectangle "Equip de Suport (Helpdesk)\n(Nivell 1 i 2)" as Suport
rectangle "Equip de Desplegament\n(Xarxes i Hardware)" as Desplegament
rectangle "Equip de Ciberseguretat\n(Serveis Gestionats)" as Seguretat

' Relacions jeràrquiques
Dir -down-> Admin
Dir -down-> Comercial
Dir -down-> CapTecnic
Dir -down-> CapProjectes

CapTecnic -down-> Suport
CapTecnic -down-> Desplegament
CapTecnic -down-> Seguretat

' Notes explicatives (en català)
note right of Dir
  Pren decisions estratègiques.
  Busca socis (SAGE, Microsoft).
  És la cara visible.
end note

note bottom of Seguretat
  En una PIME petita,
  aquest rol pot ser extern
  o compartit amb el Cap Tècnic.
end note
@enduml