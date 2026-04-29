# P01 — Planificació del Projecte (FoodLogístics S.A.)

> **Ubicació obligatòria:** `/P01/Planificacio/README.md`  
> **Objectiu:** demostrar capacitat de **planificació professional** (no només “fer un Gantt”), amb criteri tècnic, organitzatiu i de gestió de riscos.

---

## 0) Context i propòsit

Un dels errors més habituals en equips tècnics novells és confondre **“fer feina”** amb **“gestionar un projecte”**. Configurar servidors, desenvolupar una web o desplegar serveis sense una planificació rigorosa sovint porta a:

- retards,
- colls d’ampolla,
- dependències mal resoltes,
- improvisació.

En aquest punt, **FoodLogístics S.A.** no vol només una proposta tècnica: vol **garanties**.

**La direcció vol saber:**
- Quan estaran les solucions operatives
- Quin ordre seguirem
- Què farem si una tasca es retarda
- Si sabem treballar com un equip professional

**Aquest README** és l’informe de planificació i ha d’estar alineat amb:
- el **diagrama de Gantt** (PlantUML / UMLTree),
- la **matriu RACI**,
- la **taula de riscos i contingències**.

---

## 1) Abast del projecte

### 1.1 Tasques del projecte (T01–T08)
Aquest projecte es planifica al voltant de les tasques reals del repositori:

- **T01** — _(nom/desc)_
- **T02** — _(nom/desc)_
- **T03** — _(nom/desc)_
- **T04** — _(nom/desc)_
- **T05** — _(nom/desc)_
- **T06** — _(nom/desc)_
- **T07** — _(nom/desc)_
- **T08** — _(nom/desc)_

> ✅ **Nota:** Afegeix una línia per tasca amb “què lliura” (deliverable) i “quan es considera acabada”.

### 1.2 Horitzó temporal
- Durada planificada: **4 setmanes** (segons criteris del diagrama final).  
  > ⚠️ Al text inicial s’esmenten “3 setmanes” però als requisits del diagrama s’indiquen “4 setmanes”.  
  > **Decisió d’equip:** fem servir **4 setmanes** per garantir coherència amb el lliurable del Gantt.

---

## 2) Fase 1 — Anàlisi real: tasques i dependències

### 2.1 Ordre lògic d’execució
Expliqueu amb paraules **l’ordre** i el perquè:

- Quines tasques **són prerequisit** d’altres
- Quines tasques **poden anar en paral·lel**
- Quines tasques són **bloquejants**
- On poden aparèixer **colls d’ampolla**

**Dependències (exemple de format):**
- **T02** depèn de **T01** perquè _(raó tècnica/organitzativa)_.
- **T03** pot començar en paral·lel amb **T02** perquè _(raó)_.
- **T05** bloqueja **T06** perquè _(raó)_.

### 2.2 Mapa de dependències (resum visual/llista)
> Recomanat: un diagrama simple (imatge) o una llista clara.

- **Bloquejants:** _(llista)_
- **Paral·lelitzables:** _(llista)_
- **Crítiques per lliurable final:** _(llista)_

---

## 3) Fase 1.2 — Camí crític (Critical Path)

### 3.1 Identificació del camí crític
Indiqueu:
- Quines tasques, si es retarden, **desplacen el projecte sencer**
- Quines tenen **marge (slack)** i quant (aprox.)

**Camí crític proposat:**
- `T__ → T__ → T__ → T__`

**Justificació (obligatori):**
- Per què aquestes tasques són crítiques?
- Quin impacte tindria un retard de 1–2 dies?

---

## 4) Fase 2 — Estimació d’esforç amb criteri (IA guiat)

### 4.1 Mètode d’estimació (obligatori)
Per a **cada tasca**, estimeu la durada (hores) considerant com a mínim:

- Temps de comprensió (lectura, anàlisi)
- Temps de recerca (si cal)
- Implementació tècnica
- Proves i errors
- Documentació
- Coordinació amb l’equip
- Interrupcions (classes, exàmens, altres tasques)
- Marge d’imprevistos (buffer)

### 4.2 Fitxa d’estimació per tasca (plantilla)
> Copieu i ompliu per **T01–T08**.

#### T0X — _(nom de la tasca)_
- **Objectiu:**  
- **Deliverable:**  
- **Estimació total:** `__ h`
- **Desglossament:**
  - Comprensió: `__ h`
  - Recerca: `__ h`
  - Implementació: `__ h`
  - Proves: `__ h`
  - Documentació: `__ h`
  - Coordinació: `__ h`
  - Buffer: `__ h`
- **Riscos associats:**  
- **Criteri d’acceptació (“Done”):**

### 4.3 Ús d’IA (obligatori i crític)
Expliqueu com heu fet servir IA **sense fer-la servir com a “oracle”**:

- Quines preguntes heu fet (exemples)
- Què heu acceptat i què heu rebutjat
- Quina informació humana (experiència del grup, restriccions, context) ha ajustat l’estimació final

> ✅ Incloeu 2–3 fragments breus (captura o text) de les interaccions d’IA com a evidència del procés.

---

## 5) Fase 3 — Assignació de recursos (treball en equip real)

### 5.1 Membres de l’equip
- **Membre A:** _(nom)_ — _(rol principal: backend/devops/doc/etc.)_
- **Membre B:** _(nom)_ — _(rol principal)_
- _(Opcional: Membre C, D...)_

### 5.2 Criteris d’assignació
Heu d’explicar com heu evitat:
- sobrecàrrega d’una persona,
- temps morts d’altres,
- dependències personals bloquejants.

**Decisions clau:**
- Tasques compartides: _(llista)_
- Coordinació (ritme de reunions, handoffs, revisió): _(descriure)_

---

## 6) Fase 4 — Diagrama de Gantt (PlantUML / UMLTree)

### 6.1 Fitxers obligatòris
Aquesta carpeta ha d’incloure:
- `gantt.puml` — codi PlantUML
- `gantt.png` (o `.svg`) — imatge exportada del Gantt

> El Gantt ha de mostrar clarament:
- les **4 setmanes** de planificació,
- tasques **T01–T08**,
- **durada** i **dependències**,
- paral·lelismes,
- relació temporal entre activitats i productes.

### 6.2 Exemple mínim de codi PlantUML (placeholder)
> **Important:** Ajusteu durades i dependències segons la vostra planificació real.

```plantuml
@startgantt
Project starts 2026-05-04

' Setmana 1
[Т01 - Anàlisi] lasts 2 days
[Т02 - Disseny] lasts 3 days and starts at [Т01 - Anàlisi]'s end

' Paral·lel
[Т03 - Setup entorn] lasts 3 days and starts at [Т01 - Anàlisi]'s end

' Setmana 2-3
[Т04 - Implementació] lasts 5 days and starts at [Т02 - Disseny]'s end
[Т05 - Integració] lasts 3 days and starts at [Т04 - Implementació]'s end

' Setmana 4
[Т06 - Testing] lasts 3 days and starts at [Т05 - Integració]'s end
[Т07 - Documentació] lasts 2 days and starts at [Т06 - Testing]'s start
[Т08 - Deploy final] lasts 1 day and starts at [Т06 - Testing]'s end
@endgantt
````

***

## 7) Distribució setmana a setmana (visió executiva)

> Aquí expliqueu **què s’està fent cada setmana**, qui ho fa i què es lliura.

### Setmana 1

*   Objectiu: *(ex: tancar abast i dependències, preparar entorn)*
*   Tasques: *(ex: T01, T03)*
*   Deliverables: *(ex: decisions d’arquitectura, entorn funcional)*

### Setmana 2

*   Objectiu:
*   Tasques:
*   Deliverables:

### Setmana 3

*   Objectiu:
*   Tasques:
*   Deliverables:

### Setmana 4

*   Objectiu:
*   Tasques:
*   Deliverables:

***

## 8) Fase 5 — Pla de contingència (riscos reals)

### 8.1 Taula de riscos i contingències (obligatori)

> Incloeu **mínim 2 riscos crítics** (reals).

**Risc 1 — *(nom)***

*   Problema possible:
*   Part del projecte afectada:
*   Impacte (temps/qualitat/abast):
*   Senyals d’alerta (early warning):
*   Mitigació (abans que passi):
*   Contingència (si passa):
*   Responsable del seguiment:

**Risc 2 — *(nom)***

*   Problema possible:
*   Part del projecte afectada:
*   Impacte (temps/qualitat/abast):
*   Senyals d’alerta:
*   Mitigació:
*   Contingència:
*   Responsable:

***

## 9) Matriu RACI (responsabilitats)

> Creeu un fitxer addicional recomanat: `raci.md` o incloeu-la aquí.

**Llegenda:**

*   **R** = Responsible (executa)
*   **A** = Accountable (valida / responsable final)
*   **C** = Consulted (consulta)
*   **I** = Informed (informat)

### 9.1 RACI (plantilla)

*   **T01:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_
*   **T02:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_
*   **T03:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_
*   **T04:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_
*   **T05:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_
*   **T06:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_
*   **T07:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_
*   **T08:** A: \_\_ | R: \_\_ | C: \_\_ | I: \_\_

***

## 10) Reflexió: colls d’ampolla i decisions clau

### 10.1 Punts crítics detectats

*   Coll d’ampolla principal:
*   Motiu:
*   Com l’hem mitigat:

### 10.2 Decisions més importants de planificació

*   Decisió 1:
*   Decisió 2:
*   Trade-offs (què guanyem / què perdem):

***

## 11) Preguntes clau (OBLIGATÒRIES)

Respostes curtes però justificades:

1.  **Quina és la tasca més crítica del projecte i per què?**
    *   Resposta:

2.  **On heu detectat el principal coll d’ampolla?**
    *   Resposta:

3.  **Quina decisió de planificació ha estat més difícil?**
    *   Resposta:

4.  **Heu hagut de modificar alguna estimació inicial? Per què?**
    *   Resposta:

5.  **Quin risc podria fer fracassar el projecte?**
    *   Resposta:

6.  **Si tinguéssiu una setmana més, què canviaria?**
    *   Resposta:

***

## 12) Evidències (captures / enllaços / fitxers)

Incloeu evidències visuals i útils:

*   Captura del diagrama de Gantt (`gantt.png/.svg`)
*   Captura del codi PlantUML (`gantt.puml`)
*   Notes d’estimació o log de decisions
*   Evidència d’ús crític d’IA (2–3 exemples)

***

## 13) Criteris de qualitat (autocheck)

*   [ ] El Gantt és coherent amb el projecte i amb aquest README
*   [ ] Estimacions realistes i justificades (no arbitràries)
*   [ ] Dependències ben enteses i explicitades
*   [ ] Hi ha paral·lelismes raonables (sense incoherències)
*   [ ] RACI clara (sense rols buits o duplicats sense sentit)
*   [ ] Riscos reals i contingències aplicables
*   [ ] Ús crític de la IA (explicat i evidenciat)

