> 💡 **Tipps:**
> 
> - `PRIMARY KEY`: eindeutiger Bezeichner
>     
> - `NOT NULL`: darf nicht leer sein
>     
> - `DEFAULT`: Standardwert definieren
>     

**Beispiel mit Default:**

`CREATE TABLE produkte (     id INT PRIMARY KEY,    name VARCHAR(100) NOT NULL,    preis DECIMAL(10,2) DEFAULT 0 );`

---

## 🔧 ALTER — Tabellen anpassen

> Wird verwendet, um Strukturänderungen an bestehenden Tabellen vorzunehmen.

**Spalte hinzufügen:**

`ALTER TABLE kunden ADD email VARCHAR(255);`

**Spalte umbenennen:**

`ALTER TABLE kunden RENAME COLUMN ort TO stadt;`

**Spalte löschen:**

`ALTER TABLE kunden DROP COLUMN geburtsdatum;`

**Datentyp ändern:**

`ALTER TABLE kunden ALTER COLUMN name TYPE VARCHAR(150);`

> ⚠️ Nicht alle Datenbanksysteme erlauben jede dieser Varianten gleich.  
> Beispiel: In MySQL ist die Syntax etwas anders (`MODIFY COLUMN` statt `ALTER COLUMN`).

---

## 💣 DROP — Objekte löschen

> Entfernt Tabellen, Datenbanken oder andere Strukturen **dauerhaft**.

`DROP TABLE kunden; DROP DATABASE firma;`

> ⚠️ **Vorsicht:** Dieser Befehl löscht alles – **nicht rückgängig** zu machen.  
> Verwende vorher `SHOW TABLES;` oder `DESCRIBE` zum Überprüfen.

---

## 🧹 TRUNCATE — Inhalt der Tabelle löschen (Struktur bleibt)

> Löscht **alle Datensätze**, behält aber die Struktur (Spalten, Constraints, etc.).

`TRUNCATE TABLE kunden;`

> 🧠 **Unterschied zu `DELETE`:**
> 
> - `DELETE` kann gefiltert werden (`WHERE`)
>     
> - `TRUNCATE` löscht **alles**, ist aber viel schneller
>     
> - `TRUNCATE` kann in manchen DB-Systemen **nicht rückgängig gemacht** werden.
>     

---

## RENAME — Tabelle/Objekt umbenennen


`RENAME TABLE kunden TO customer;`

> 💡 Einfacher Weg, um Tabellen umzubenennen, z. B. nach einem Refactoring.

---

## 🔐 CONSTRAINTS — Regeln und Beziehungen

> 🚧 Sichern die Datenintegrität (z. B. eindeutige Werte, Beziehungen, Wertebereiche).

**Beispiele:**

`CREATE TABLE bestellungen (     id INT PRIMARY KEY,    kunde_id INT NOT NULL,    datum DATE DEFAULT CURRENT_DATE,    FOREIGN KEY (kunde_id)        REFERENCES kunden(id)        ON DELETE CASCADE );`

**Häufige Constraint-Typen:**

|Constraint|Bedeutung|
|---|---|
|`PRIMARY KEY`|Eindeutige ID für jeden Datensatz|
|`FOREIGN KEY`|Verknüpft Tabellen|
|`UNIQUE`|Kein doppelter Wert erlaubt|
|`CHECK`|Überprüft Bedingung (z. B. `preis > 0`)|
|`NOT NULL`|Wert darf nicht leer sein|
|`DEFAULT`|Legt Standardwert fest|

> 💬 Beispiel mit mehreren Constraints:


`CREATE TABLE user (     id INT PRIMARY KEY,    username VARCHAR(50) UNIQUE NOT NULL,    alter INT CHECK (alter >= 16) );`

---

## 🧩 Quick Overview

|Befehl|Zweck|Beispielaktion|
|---|---|---|

|Befehl|Zweck|Beispielaktion|
|---|---|---|
|`CREATE`|Neues Objekt erstellen|Neue Tabelle `kunden` anlegen|
|`ALTER`|Objektstruktur ändern|Spalte hinzufügen/ändern|
|`DROP`|Objekt löschen|Tabelle entfernen|
|`TRUNCATE`|Alle Zeilen löschen|Tabelle leeren|
|`RENAME`|Objekt umbenennen|Tabelle `kunden` → `customer`|
|`CONSTRAINT`|Integritätsregel definieren|`FOREIGN KEY` zu Kunden anlegen|

---

## ⚡ Bonus: DDL sicher anwenden

> Nutze Transaktionen, soweit das DBMS sie für DDL unterstützt:

`BEGIN TRANSACTION; ALTER TABLE kunden ADD COLUMN bonuspunkte INT DEFAULT 0; COMMIT;`

> 💡 In manchen Systemen (z. B. MySQL ohne InnoDB) werden DDL-Änderungen **sofort** übernommen und können **nicht** rückgängig gemacht werden.

---

> ✅ **Fazit:**  
> Die DDL-Befehle bilden das Fundament deiner Datenbankstruktur.  
> Sie definieren, wie deine Tabellen und Beziehungen aufgebaut sind — die Basis für alles, was du danach mit DML machst.
