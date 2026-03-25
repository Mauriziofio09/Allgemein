## INSERT - Daten einfügen

`INSERT INTO kunden (id, name, ort) VALUES (1, 'Max Muster', 'Luzern');`

**Mehrere Datensätze:**



`INSERT INTO kunden (name, ort) VALUES '('Anna', 'Bern'),        ('Leo', 'Basel');`

> 💡 **Tipp:** Felder, für die kein Wert angegeben wird, erhalten entweder `NULL` oder ihren **Default-Wert** (falls definiert).

---

## 🧭 UPDATE — Daten ändern

> ✏️ Ändert bestehende Datensätze.

`UPDATE tabelle SET spalte1 = neuer_wert1, spalte2 = neuer_wert2 WHERE bedingung;`

**Beispiel:**

sql

`UPDATE kunden SET ort = 'Zürich' WHERE id = 1;`

> ⚠️ **Ohne WHERE** wird **die gesamte Tabelle aktualisiert** – immer mit Bedingung verwenden!

**Mit mehreren Bedingungen:**

`UPDATE kunden SET ort = 'Genf' WHERE ort = 'Basel' AND name LIKE 'L%';`

---

## 🗑️ DELETE — Daten löschen

> 🧨 Entfernt Datensätze aus einer Tabelle.


`DELETE FROM tabelle WHERE bedingung;`

**Beispiel:**

`DELETE FROM kunden WHERE ort = 'Basel';`

> ⚠️ **Ohne WHERE** werden **alle Datensätze gelöscht!**

**Alternative:** ganze Tabelle leeren (schneller, aber ohne Logging)

`TRUNCATE TABLE tabelle;`

---

## 🔗 CASCADING — Verbundene Aktionen (Foreign Keys)

> 🔄 Automatische Folgeaktionen bei verknüpften Tabellen definieren.


`CREATE TABLE bestellungen (     id INT PRIMARY KEY,    kunde_id INT,    FOREIGN KEY (kunde_id)      REFERENCES kunden(id)      ON DELETE CASCADE      ON UPDATE CASCADE );`

**Bedeutung:**

- 🗑️ `ON DELETE CASCADE`: Löscht abhängige Datensätze, wenn der Primärdatensatz gelöscht wird.
    
- ✏️ `ON UPDATE CASCADE`: Aktualisiert Fremdschlüssel, wenn sich die Referenz-ID ändert.
    
- 🚫 `ON DELETE SET NULL`: Setzt Fremdschlüssel auf `NULL`, statt zu löschen.
    

> 💡 Sehr hilfreich, um **Datenintegrität** in relationalen Strukturen sicherzustellen.

---

## 🔀 MERGE — Kombiniertes Einfügen/Aktualisieren

> 🧠 Führt bedingtes Einfügen oder Aktualisieren in einem Befehl aus.  
> Ideal für **Synchronisationen** z. B. beim Import aus einer anderen Quelle.

sql

`MERGE INTO ziel AS z USING quelle AS q ON (z.id = q.id) WHEN MATCHED THEN     UPDATE SET z.name = q.name WHEN NOT MATCHED THEN     INSERT (id, name)    VALUES (q.id, q.name);`

**Praktisches Beispiel:**

sql

`MERGE INTO kunden AS k USING neue_kunden AS nk ON (k.id = nk.id) WHEN MATCHED THEN     UPDATE SET k.name = nk.name, k.ort = nk.ort WHEN NOT MATCHED THEN     INSERT (id, name, ort)    VALUES (nk.id, nk.name, nk.ort);`

> 💡 Spart Zeit bei Imports, Backups oder periodischer Synchronisation zwischen Tabellen.

---

## 🧩 Quick Overview

|Befehl|Zweck|Beispielaktion|
|---|---|---|
|`INSERT`|Neue Daten einfügen|Neuer Kunde wird angelegt|
|`UPDATE`|Bestehende Daten ändern|Kundenort anpassen|
|`DELETE`|Daten löschen|Kunde entfernen|
|`MERGE`|Einfügen oder Ändern je nach Match|CSV-Import synchronisieren|
|`CASCADE`|Automatische Folgeaktion|Löscht verbundene Datensätze|

---

## 🧠 Bonus: Transaktionen zum sicheren Arbeiten

> Verwende Transaktionen beim Testen oder für sicherheitskritische Operationen.

sql

`BEGIN TRANSACTION; UPDATE kunden SET ort = 'Bern' WHERE id = 5; -- Wenn alles passt: COMMIT; -- Wenn ein Fehler passiert: ROLLBACK;`

> 💡 Damit kannst du Befehle rückgängig machen, bevor sie dauerhaft in der DB landen.

---

> ✅ **Fazit:**  
> Mit diesen fünf Befehlen deckst du 90 % der Datenmanipulation in SQL ab.  
> Lerne sie gut – sie sind das tägliche Werkzeug jedes Datenbankentwicklers!

text

``*** Möchtest du, dass ich dir zusätzlich noch eine **Version mit farbigen Callouts** für Obsidian (z. B. `> [!tip]`, `> [!warning]`) mache, damit das Cheatsheet noch lebendiger aussieht?``