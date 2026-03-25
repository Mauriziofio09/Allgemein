**Spezifische Spalten:**

`SELECT name, ort FROM kunden;`

**Mit Filter:**

`SELECT * FROM kunden WHERE ort = 'Luzern';`

---

## ⚖️ SELECT DISTINCT — Duplikate entfernen

> Zeigt nur **einmalige Werte**.

`SELECT DISTINCT ort FROM kunden;`

> 💡 Nützlich für Listen von Kategorien oder eindeutigen Werten.

---

## 🔤 WHERE — Bedingungen filtern

> Schränkt Ergebnisse durch Bedingungen ein.

**Vergleiche:**

`SELECT * FROM kunden WHERE id > 5; SELECT * FROM kunden WHERE name LIKE 'M%';`

**Logische Operatoren:**

`SELECT * FROM kunden  WHERE ort = 'Zürich' OR ort = 'Bern';`

**NULL-Checks:**

`SELECT * FROM kunden WHERE email IS NULL;`

---

## 📊 ORDER BY — Sortieren

> Sortiert Ergebnisse nach Spalten.

`SELECT * FROM kunden ORDER BY name ASC; SELECT name, ort FROM kunden ORDER BY ort DESC, name ASC;`

---

## 🎲 GROUP BY — Gruppieren & Aggregieren

> Gruppiert Daten und berechnet Zusammenfassungen.

`SELECT ort, COUNT(*) as anzahl_kunden FROM kunden  GROUP BY ort;`

**Mit HAVING (Filter nach Gruppierung):**

`SELECT ort, COUNT(*) as anzahl FROM kunden  GROUP BY ort  HAVING COUNT(*) > 2;`

---

## ➕ JOINS — Tabellen verknüpfen

> Verbindet Daten aus mehreren Tabellen.

|Join-Typ|Beschreibung|Syntax|
|---|---|---|
|`INNER JOIN`|Nur passende Datensätze|`INNER JOIN ON bedingung`|
|`LEFT JOIN`|Alle aus links + Matches rechts|`LEFT JOIN ON bedingung`|
|`RIGHT JOIN`|Alle aus rechts + Matches links|`RIGHT JOIN ON bedingung`|
|`FULL JOIN`|Alle aus beiden Tabellen|`FULL JOIN ON bedingung`|

**Beispiel INNER JOIN:**

`SELECT k.name, b.bestell_nr FROM kunden k INNER JOIN bestellungen b ON k.id = b.kunde_id;`

---

## 🔢 LIMIT / TOP — Ergebnisse begrenzen

> Schränkt Anzahl der zurückgegebenen Zeilen ein.

**MySQL/PostgreSQL:**

`SELECT * FROM kunden LIMIT 10;`

**SQL Server:**

`SELECT TOP 10 * FROM kunden;`

---

## 🧮 Aggregate Functions — Zusammenfassungen

|Funktion|Beschreibung|Beispiel|
|---|---|---|
|`COUNT(*)`|Anzahl Zeilen|`COUNT(*) as anzahl`|
|`SUM(spalte)`|Summe|`SUM(preis)`|
|`AVG(spalte)`|Durchschnitt|`AVG(gehalt)`|
|`MIN(spalte)`|Minimum|`MIN(preis)`|
|`MAX(spalte)`|Maximum|`MAX(gehalt)`|

**Beispiel:**

`SELECT      COUNT(*) as total_kunden,    AVG(CASE WHEN ort IS NOT NULL THEN 1 ELSE 0 END) as ort_ausgefuellt FROM kunden;`

---

## 🧩 Quick Reference

|Clause|Zweck|Beispiel|
|---|---|---|
|`SELECT`|Spalten wählen|`SELECT name, ort`|
|`FROM`|Tabelle(n)|`FROM kunden`|
|`WHERE`|Filter **vor** GROUP BY|`WHERE ort = 'Bern'`|
|`GROUP BY`|Gruppieren|`GROUP BY ort`|
|`HAVING`|Filter **nach** GROUP BY|`HAVING COUNT(*) > 5`|
|`ORDER BY`|Sortieren|`ORDER BY name ASC`|
|`LIMIT`|Begrenzung|`LIMIT 10`|

---

## 🔥 Complex Query Template

`SELECT      spalte1,    COUNT(*) as anzahl,    AVG(spalte2) as durchschnitt FROM tabelle1 t1 LEFT JOIN tabelle2 t2 ON t1.id = t2.fk_id WHERE bedingung GROUP BY spalte1 HAVING COUNT(*) > 5 ORDER BY anzahl DESC LIMIT 10;`

---

## 💡 Pro Tips

> - **Alias immer verwenden** bei Joins: `kunden k`, `bestellungen b`
>     
> - **WHERE vor GROUP BY** denken (Reihenfolge der Ausführung)
>     
> - **HAVING nur nach GROUP BY** verwenden
>     
> - **DISTINCT sparsam** einsetzen (Performance!)
>     

---

> ✅ **Fazit:**  
> Mit `SELECT` + diesen Clauses kannst du **99% aller Abfragen** erstellen.  
> Die Reihenfolge `SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT` merken!