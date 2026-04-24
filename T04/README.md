
# Servidor d’Impressió amb Printer Pooling  
## Implementació a Windows Server per a entorns logístics

## Introducció

En el món de la **logística**, la impressió continua tenint un paper clau en els processos operatius diaris: **albarans, fulls de transport, etiquetes**, etc. En aquest context, el client no és una excepció.

L’empresa disposa d’un **magatzem** on el volum d’impressió d’albarans és **crític**. Si una impressora falla o es col·lapsa, els camions no poden sortir, fet que pot provocar el **trencament de la cadena de fred**, amb greus conseqüències operatives i econòmiques.

L’objectiu d’aquesta activitat és **configurar un Servidor d’Impressió a Windows Server** que permeti gestionar aquest volum d’impressió mitjançant la funcionalitat de **Printer Pooling (cua d’impressió compartida)**, balancejant la càrrega entre **dos dispositius d’impressió**.

---

## Objectiu del projecte

- Garantir **alta disponibilitat** del servei d’impressió del magatzem.
- Evitar colls d’ampolla en moments d’alta càrrega.
- Centralitzar la gestió d’usuaris, equips i impressores.
- Automatitzar el desplegament de la impressora als clients mitjançant **GPO**.
- Aplicar mesures bàsiques de **seguretat i control horari**.

---

## Descripció de l’activitat

El servidor haurà de tenir implementats:

- **Active Directory Domain Services (AD DS)**  
- **Print and Document Services**

Aquesta configuració permetrà una **gestió centralitzada**:
- Usuaris i equips autenticats contra el domini.
- Accés controlat als recursos compartits.
- Impressores gestionades exclusivament des del servidor.

Els equips clients, integrats al domini, hauran de poder:
- Iniciar sessió amb credencials de xarxa.
- Accedir automàticament a les impressores desplegades.

Tots els passos del procés s’han de documentar com si fos un **informe tècnic d’implementació per a un client real**, utilitzant un llenguatge:
- Clar
- Estructurat
- Professional

---

## Fases tècniques de la implementació

L’activitat es divideix en **quatre fases tècniques** principals.

---

## 1️⃣ Preparació de l’entorn i simulació de maquinari

### Objectiu
Simular un escenari real d’impressió amb dues impressores disponibles per fer balanceig de càrrega.

### Tasques realitzades
- Verificació i preparació de l’entorn de **Windows Server**.
- Instal·lació i configuració de **dues instàncies de PDF24 Printer**, seguint la guia proporcionada als materials de suport.
- Assignació de noms corporatius a les impressores:

| Impressora | Nom |
|-----------|-----|
| Impressora 1 | `IMP_MAGATZEM_A` |
| Impressora 2 | `IMP_MAGATZEM_B` |

Aquestes impressores representen dispositius físics independents dins del magatzem.

---

## 2️⃣ Instal·lació del rol i configuració del Printer Pooling

### Instal·lació del rol
- Instal·lació del rol **Print and Document Services** al Windows Server.
- Accés a la consola **Print Management** per a la gestió centralitzada.

### Configuració del Printer Pooling

Els passos realitzats són:
1. Accedir a les **propietats** de la impressora `IMP_MAGATZEM_A`.
2. Anar a la pestanya **Ports**.
3. Activar l’opció **Enable printer pooling**.
4. Seleccionar el port corresponent a `IMP_MAGATZEM_B`.

> ✅ A partir d’aquest moment, ambdues impressores funcionen sota **un mateix nom de xarxa**, repartint automàticament els treballs d’impressió.

### Nota tècnica
- A `IMP_MAGATZEM_A` han de quedar **seleccionats els dos ports virtuals**, assegurant el correcte funcionament del pool.

---

## 3️⃣ Desplegament automatitzat mitjançant Group Policy (GPO)

### Context
L’empresa no vol que el personal de magatzem hagi d’instal·lar manualment cap impressora.

### Objectiu
Automatitzar el desplegament de la impressora del magatzem als clients del domini.

### Tasques realitzades
- Creació d’una **GPO** amb el nom:

```text
GPO_Impressores_Magatzem
````

*   Ús de l’opció **"Deploy with Group Policy"** des de la consola **Print Management**.
*   Vinculació de la GPO:
    *   Al domini, o
    *   A una **Unitat Organitzativa (OU)** específica on es troba l’usuari de proves.

### Validació

*   Inici de sessió en un client **Windows 11** integrat al domini.
*   Verificació que la impressora apareix **automàticament** sense intervenció de l’usuari.

### Nota tècnica

En cas que la impressora no aparegui immediatament, cal:

```powershell
gpupdate /force
```

i tancar / reobrir la sessió.

***

## 4️⃣ Prova de càrrega i configuració de seguretat

### Prova de càrrega (balanceig)

*   Enviament de **10 documents consecutius** a la impressora del magatzem.
*   Observació del comportament del servidor:
    *   Repartiment dels treballs entre `IMP_MAGATZEM_A` i `IMP_MAGATZEM_B`.
    *   Confirmació del correcte funcionament del **Printer Pooling**.

### Configuració de seguretat

*   Configuració de restriccions mitjançant:
    *   **Printing Priorities**, o
    *   **Available Times**.

### Restricció horària aplicada

*   Funcionament permès només en **horari laboral**:
    *   🕕 **06:00**
    *   🕙 **22:00**

Aquesta mesura evita usos indeguts fora de l’horari operatiu del magatzem.

***

## Conclusions

La implementació del **Servidor d’Impressió amb Printer Pooling** permet:

*   Millorar la **disponibilitat del servei**.
*   Assegurar la continuïtat operativa del magatzem.
*   Centralitzar i automatitzar la gestió d’impressores.
*   Reduir errors humans i tasques manuals.
*   Aplicar controls bàsics de seguretat i horari.

Aquesta solució és escalable i adaptable a entorns reals amb múltiples impressores físiques.

***

## Autoria

Document tècnic d’implementació  
Entorn Windows Server – Àmbit logístic

