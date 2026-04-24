
# Servidor de Fitxers Corporatiu  
## Infraestructura segura, organitzada i controlada per a FoodLogistic

## Introducció

Quan el volum de negoci creix, també ho fa el **volum de dades**, i sovint és en aquest punt quan apareixen els problemes: la informació queda **dispersa**, compartimentada per departaments i sense una visió global ni controls homogenis.

**FoodLogistic** no ha estat una excepció: cada departament emmagatzemava la documentació **de forma local**, fet que comportava riscos de:
- Pèrdua d’informació.
- Duplicació de dades.
- Falta de control d’accés.
- Ús indegut de l’espai d’emmagatzematge.

Aquest projecte té com a finalitat **resoldre aquesta problemàtica** mitjançant la implementació d’una **infraestructura de servidor de fitxers** segura, centralitzada i controlada.

---

## Objectiu del projecte

Implementar una infraestructura de fitxers que compleixi els següents requisits:

- ✅ Organització clara per departaments.
- ✅ Control d’accés mitjançant **NTFS i SMB**.
- ✅ Control de l’espai amb **quotes NTFS** i **FSRM**.
- ✅ Restricció de tipus de fitxers no permesos.
- ✅ Administració demostrada mitjançant:
  - Explorador de fitxers
  - Server Manager
  - PowerShell

---

## Descripció de l’activitat

L’activitat es divideix en diverses **fites tècniques**, simulant un procés real de **consultoria, disseny i implementació** per a un client empresarial.

La infraestructura es desplega sobre un domini:

```text
foodlogistic.test
````

Es recomana crear una estructura d’**Unitats Organitzatives (OU)** coherent, la qual haurà de ser **justificada** segons les necessitats del projecte.

***

## 1️⃣ Preparació i seguretat de grups (Active Directory)

### Objectiu

Establir una base sòlida de **seguretat i control d’accés** abans de crear els recursos compartits.

### Grups de seguretat creats

| Grup            | Funció                             |
| --------------- | ---------------------------------- |
| `Administracio` | Gestió de factures i albarans      |
| `Transport`     | Xofers i caps de flota             |
| `Direccio`      | Gerència i informació confidencial |

Aquests grups s’utilitzen posteriorment per assignar permisos NTFS i SMB de forma centralitzada.

***

## 2️⃣ Implementació de recursos compartits (tres mètodes)

Es creen diferents carpetes al servidor, cadascuna utilitzant un **mètode d’administració diferent**, demostrant domini de les eines de Windows Server.

***

### A. Carpeta `Public`

**Mètode:** Explorador d’arxius

#### Configuració

*   Recurs compartit visible per a **tothom**.
*   Permisos:
    *   **SMB:** Lectura
    *   **NTFS:** Modificació

> ✅ Es verifica la combinació de permisos efectiva per assegurar que els usuaris poden treballar correctament sense excedir privilegis.

***

### B. Carpeta `Operacions`

**Mètode:** Server Manager / File and Storage Services

#### Configuració

*   Instal·lació del rol **File and Storage Services** (si no és present).
*   Creació del recurs compartit des de **Server Manager**.
*   Activació de:
    *   **Access-Based Enumeration (ABE)**: la carpeta només és visible per als usuaris amb permisos.

#### Restriccions

*   Només el grup `Transport` hi pot accedir.

***

### C / D. Carpeta `Direccio` (confidencial)

> ⚠️ S’ha d’escollir **només un mètode**.  
> El **mètode D** té una valoració superior.

***

### ✅ Mètode D (PowerShell avançat)

#### Configuració

*   Creació de la carpeta `Direccio`.
*   Compartició mitjançant PowerShell amb:
    *   Accés exclusiu per al grup `Direccio`.
    *   **Access-Based Enumeration** habilitada.

#### Automatització

*   Configuració d’una **GPO** perquè:
    *   La carpeta `Direccio` es munti automàticament com a **unitat Z:**
    *   Només als usuaris del grup `Direccio`.

Aquesta configuració garanteix:

*   Confidencialitat
*   Simplicitat per a l’usuari
*   Compliment del principi de mínim privilegi

***

## 3️⃣ Control d’emmagatzematge (Quotes NTFS i FSRM)

El client informa que alguns usuaris **guarden fitxers personals**, com fotos o vídeos, saturant el disc.

***

### Quotes NTFS (control per volum)

*   Activació de **quotes NTFS** a la unitat de dades.
*   Configuració:
    *   Lím it per defecte: **500 MB per usuari**
    *   Aplicable a qualsevol usuari nou automàticament

***

### File Server Resource Manager (FSRM)

#### Instal·lació

*   Instal·lació del rol **File Server Resource Manager**.

***

#### Quota per carpeta (`Public`)

*   Tipus: **Hard Quota**
*   Límit: **200 MB**
*   Avís al **90% d’ús** amb missatge personalitzat:

```text
Compte! FoodLogístic t'informa que estàs a punt d'esgotar l'espai compartit.
```

***

#### Filtratge de fitxers (`Operacions`)

*   Creació d’un filtre que **impedeix** guardar:
    *   Fitxers executables (`.exe`, `.msi`)
    *   Fitxers d’àudio i vídeo

Aquesta mesura redueix riscos de:

*   Malware
*   Ús indegut de l’espai
*   Pèrdua de rendiment

***

## 4️⃣ Verificació i auditoria

Les proves es realitzen des d’un client **Windows 10 / Windows 11** integrat al domini.

### Comprovacions realitzades

*   🔍 Accés i visibilitat dels recursos segons el grup:
    *   Administracio
    *   Transport
    *   Direccio
*   🚫 Intent de copiar un `.exe` a `Operacions`.
*   🧪 Prova de canvi d’extensió:
    *   Executable renombrat a `.txt`
    *   Verificació del comportament del filtratge actiu de FSRM.

***

## Què cal lliurar

### 📄 Informe tècnic en format Markdown que inclogui:

#### 1. Resum de configuració

Taula amb:

*   Nom de la carpeta
*   Camí UNC
*   Grups amb accés
*   Mètode de creació utilitzat

#### 2. Evidències

*   Captures de pantalla comentades de:
    *   Grups d’AD
    *   Permisos NTFS / SMB
    *   Quotes i filtres FSRM
    *   GPOs aplicades

#### 3. Proves de funcionament

*   Captures des del client:
    *   Accés correcte segons grup
    *   Denegacions de permisos
    *   Funcionament de quotes
    *   Restriccions de tipus de fitxer

***

## Conclusions

La solució implementada permet a FoodLogistic:

*   Centralitzar les dades corporatives.
*   Garantir la seguretat i la confidencialitat.
*   Controlar l’ús de l’emmagatzematge.
*   Reduir riscos operatius i de seguretat.
*   Escalar fàcilment la infraestructura en el futur.

***

## Autoria

Informe tècnic d’implementació  
Servidor de Fitxers – Entorn Windows Server  
FoodLogistic

