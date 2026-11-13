# Fitxes de funcions · Missió 2

## COUNTIFS

**Documentació:** https://support.google.com/docs/answer/3256550?hl=es

**Què fa:** Compta quantes files compleixen dues o més condicions a la vegada.

**Sintaxi:** `COUNTIFS(interval_criteris1; criteri1; [interval_criteris2; criteri2; ...])`

| Argument | Obligatori? | Què és |
| --- | --- | --- |
| `interval_criteris1` | Sí | Les primeres cel·les que volem mirar. |
| `criteri1` | Sí | La condició que s'ha de complir en aquestes cel·les. |
| `interval_criteris2` | No | Un segon grup de cel·les per filtrar encara més. |
| `criteri2` | No | La condició per al segon grup. |

**Exemple de la documentació:** `=COUNTIFS(A1:A10; ">20"; B1:B10; "<30")`

**El meu exemple amb la lliga:**
`=COUNTIFS('Jornada 1'!G2:G49, "Seguidor de línia", 'Jornada 1'!N2:N49, "OK")`
* **Resultat:** `13` (Vol dir que de totes les curses de Seguidor de línia, 13 s'han acabat bé).

**Compte!** Tots els intervals que posis han de tenir exactament la mateixa mida (mateix número de files i columnes), si no surt error `#VALUE!`.

---

## SUMIFS

**Documentació:** https://support.google.com/docs/answer/3238496?hl=es

**Què fa:** Suma els números d'una columna només si es compleixen diverses condicions a la vegada.

**Sintaxi:** `SUMIFS(interval_suma; interval_criteris1; criteri1; [interval_criteris2; criteri2; ...])`

| Argument | Obligatori? | Què és |
| --- | --- | --- |
| `interval_suma` | Sí | Les cel·les amb els números que volem sumar. |
| `interval_criteris1` | Sí | El primer grup de cel·les on comprovem la condició. |
| `criteri1` | Sí | La condició que s'ha de complir. |
| `interval_criteris2` | No | Un segon grup de cel·les per posar una altra condició. |
| `criteri2` | No | La condició per al segon grup. |

**Exemple de la documentació:** `=SUMIFS(A1:A10; B1:B10; ">20"; C1:C10; "<30")`

**El meu exemple amb la lliga:**
`=SUMIFS('Jornada 1'!R2:R49, 'Jornada 1'!E2:E49, "Cable Suelto", 'Jornada 1'!N2:N49, "OK")`
* **Resultat:** `34` (Són els punts totals de l'equip Cable Suelto en les curses que ha acabat en OK).

**Compte!** L'interval que es suma ha de tenir la mateixa mida que els intervals de les condicions, si no dona error `#VALUE!`.

---

## IFS

**Documentació:** https://support.google.com/docs/answer/7014145?hl=es

**Què fa:** Comprova diverses condicions una darrere l'altra i et dona el resultat de la primera que es compleix, així no cal posar molts IF un dins de l'altre.

**Sintaxi:** `IFS(condició1; valor1; [condició2; valor2; ...])`

| Argument | Obligatori? | Què és |
| --- | --- | --- |
| `condició1` | Sí | La primera comprovació que fem. |
| `valor1` | Sí | El que surt si la primera condició es compleix. |
| `condició2` | No | Una segona comprovació per si la primera no es compleix. |
| `valor2` | No | El que surt si es compleix la segona condició. |

**Exemple de la documentació:** `=IFS(A1>90; "A"; A1>80; "B"; A1>70; "C")`

**El meu exemple amb la lliga:**
`=IFS(N2="DSQ", 0, N2="DNF", 0, J2<15, 10, J2<25, 7, TRUE, 5)`
* **Resultat:** `10` (Calcula els punts de la cursa mirant primer si ha acabat i després el temps que ha fet).

**Compte!** Si cap de les condicions és certa, la fórmula dona error `#N/A`. Per evitar-ho es posa `TRUE` al final de tot amb un valor per defecte.

---

## XLOOKUP

**Documentació:** https://support.google.com/docs/answer/12405947?hl=es

**Què fa:** Busca una dada en una columna i et retorna el que hi ha a la mateixa fila d'una altra columna.

**Sintaxi:** `XLOOKUP(clau_cerca; interval_cerca; interval_resultat; [valor_mancant]; [mode_coincidència]; [mode_cerca])`

| Argument | Obligatori? | Què és |
| --- | --- | --- |
| `clau_cerca` | Sí | El que estem buscant (per exemple, l'ID de la cursa). |
| `interval_cerca` | Sí | La columna on ha d'anar a buscar aquest valor. |
| `interval_resultat` | Sí | La columna d'on treurà la resposta. |
| `valor_mancant` | No | El text que surt si no troba el que busquem. |
| `mode_coincidència` | No | Si volem que la cerca sigui exacta (0) o aproximada. |
| `mode_cerca` | No | L'ordre en què busca (de dalt a baix o de baix a dalt). |

**Exemple de la documentació:** `=XLOOKUP("Plàtan"; A2:A5; B2:B5; "No s'ha trobat")`

**El meu exemple amb la lliga:**
`=XLOOKUP(H6, 'Jornada 1'!A2:A49, 'Jornada 1'!E2:E49, "No existeix")`
* **Resultat:** `Cable Suelto` (Quan trio l'ID `J1-008` al desplegable, el busca a la Jornada 1 i em retorna el nom de l'equip).

**Compte!** La columna on busques i la columna d'on treus el resultat han de tenir exactament la mateixa mida, si no surt error `#VALUE!`.

---

## Preguntes de lectura

1. **Què passa amb SUMIFS si l'interval de suma i l'interval del criteri no tenen la mateixa mida?**
   Dona un error `#VALUE!`. Tots els intervals han de tenir exactament les mateixes files i columnes.

2. **Què torna IFS si cap de les condicions és certa? Com ho podeu evitar?**
   Retorna l'error `#N/A`. Es pot evitar posant `TRUE` al final de tot com a última condició amb un valor per defecte.

3. **Per a què serveix el quart argument de XLOOKUP? Què passa si no el poseu i no es troba res?**
   Serveix per posar un text personalitzat si el codi que busques no existeix (com `"No existeix"`). Si no el poses i no troba res, surt l'error `#N/A`.

4. **Escriu la sintaxi de SUMIF i la de SUMIFS una sota l'altra. Què canvia de lloc?**
   * `SUMIF(interval; criteri; [interval_suma])`
   * `SUMIFS(interval_suma; interval_criteris1; criteri1; [interval_criteris2; criteri2; ...])`
   
   **Què canvia?** L'interval de suma a `SUMIF` va al final de tot i és opcional, mentre que a `SUMIFS` va el primer de tot i és obligatori.
# Reflexió final · Missió 2

La funció que m'ha costat més d'entendre ha estat XLOOKUP, perquè llegint la documentació no acabava d'entendre el concepte de com relacionava dues columnes d'una altra pestanya.

**Què vaig fer per entendre-la?**
Vaig demanar ajuda a la IA perquè m'expliqués el concepte amb exemples visuals senzills i després ho vaig provar al full amb el cercador de curses.
