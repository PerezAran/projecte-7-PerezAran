# FoodLogístic S.A. - Landing Page Legal & Compliance

Aquest projecte consisteix en l'adaptació tècnica i legal de la landing page corporativa de **FoodLogístic S.A.** per complir amb les normatives vigents de protecció de dades i serveis de la societat de la informació.

## 📌 Descripció de l'Activitat
L'objectiu principal ha estat integrar els mecanismes de transparència i consentiment exigits pel **RGPD (UE 2016/679)** i la **LSSI-CE (34/2002)**, assegurant que la recollida de dades a través del web sigui lícita i informada.

## ⚖️ Implementacions Legals

S'han incorporat tres seccions fonamentals accessibles des del peu de pàgina (*footer*) mitjançant finestres modals per mantenir l'experiència d'usuari sense abandonar la landing page:

1.  **Avís Legal**: 
    * Identificació del titular: FoodLogístic S.A.
    * NIF: A-12345678.
    * Dades registrals: Inscripció al Registre Mercantil de Barcelona.
    * Condicions d'ús i propietat intel·lectual.

2.  **Política de Privacitat**: 
    * Informació detallada sobre el Responsable del Tractament.
    * Bases legals (Consentiment i Interès legítim).
    * Procediment per exercir els drets **ARSLOP** (Accés, Rectificació, Supressió, Limitació, Oposició i Portabilitat).
    * Temps de conservació de les dades.

3.  **Política de Cookies**: 
    * Classificació de cookies utilitzades (Tècniques, Analítiques i de Personalització).
    * Instruccions per a la seva gestió a través del navegador.

## 🛠️ Modificacions Tècniques

### 1. Banner de Consentiment de Cookies
S'ha implementat un banner emergent (*Cookie Banner*) que apareix automàticament en carregar la pàgina si no hi ha un consentiment previ guardat al `localStorage`.
* **Opcions**: Acceptar totes, Configuració detallada i Rebutjar.
* **Persistència**: Les preferències es guarden localment per evitar molèsties en futures visites.

### 2. Formulari de Contacte amb Doble Consentiment
El formulari s'ha actualitzat seguint el principi de "privacitat des del disseny":
* **Checkbox de Dades (Obligatori)**: Una casella desmarcada per defecte que vincula a la Política de Privacitat. Sense aquesta acceptació, el formulari no s'envia (validació nativa HTML5).
* **Checkbox de Comunicacions (Opcional)**: Una segona casella per autoritzar l'enviament de publicitat i comunicacions comercials, vinculada a l'Avís Legal.
* **Validació de camps**: S'ha programat una validació per JavaScript que verifica que els camps crítics (Nom, Email) estiguin correctament emplenats abans de processar l'enviament.

### 3. Disseny i Usabilitat
* **Modals**: S'han utilitzat elements modals per mostrar els textos legals sense trencar l'estètica moderna de la web.
* **Responsivitat**: El formulari i els elements legals s'adapten a dispositius mòbils (*viewport-fit=cover*).

## 📁 Contingut del lliurament
* `index.html`: Codi font complet que integra el disseny original, el CSS modern i tota la lògica de JavaScript per a la gestió de cookies i modals.
* `README.md`: Aquest document explicatiu.

## 🚀 Com executar el projecte
1. Descarrega el fitxer `index.html`.
2. Obre'l en qualsevol navegador modern (Chrome, Firefox, Safari o Edge).
3. Podràs interactuar amb el banner de cookies i els enllaços legals del footer.

---
**Assignatura:** Seguretat    
**Autor:** Aran Perez
**Data:** Abril 2026
 
## Link repo: https://github.com/PerezAran/web
