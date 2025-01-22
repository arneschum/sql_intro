# Data Definition Language (DDL)

## Wie erstelle ich ein Datenmodell?

- Das Datenmodell kann:
  - Tabellen ergänzen (CREATE TABLE)
  - Tabellen ändern (ALTER TABLE)
  - Tabellen löschen (DROP TABLE)

## Tabellen erzeugen

+ Tabellen zu erzeugen ist der Anfang aller Datenmodelle
+ Grundsätzlich wird es durch das `CREATE TABLE` Statement erstellt:
  + der Name der Tabelle
  + Spaltennamen und Datentypen
  + Konsistenzprüfungen (Constraints) definiert
    + Constraints können sein:
      + CHECK (Domäne = Spalte)
      + PRIMARY KEY (Entität = Tabelle)
      + FOREIGN KEY (referentiell = zu anderen Tabellen)

```sql
--erzeugt Tabelle mit Spalten, Datentypen & Integritätsbedingungen
CREATE TABLE tabelle (
    id int PRIMARY KEY,     --PRIMARY KEY (Entität)
    vorname varchar(50) NOT NULL, -- CHECK CONSTRAINT (Domäne)
    nachname varchar(50) NOT NULL,
    abteilungs_id smallint REFERENCES abteilung (id)  --FOREIGN KEY (referentiell)
);
```

+ Tabellen können immer geändert werden, z. B.:
  + Spalten ergänzt oder vom Datentyp geändert
  + Integritätsbedingungen ergänzt oder verändert
  + ... etc.

```sql 
ALTER TABLE table_name [ADD | DROP | ALTER] [COLUMN | CONSTRAINT] 
```
- oder gelöscht werden:

```sql
DROP TABLE table_name CASCADE --CASCADE = Lösche auch Objekte die vom gelöschten Objekt abhängen
```  


# Data Manipulation Language

## Wie ändere ich Daten in den Tabellen?

- Daten können:
  - eingefügt (INSERT)
  - aktualisiert (UPDATE) oder
  - gelöscht (DELETE) werden

```sql
--alle Spalten gegeben
INSERT INTO tabelle VALUES (1, 'Wert 1', 'Wert 2');

--mit Spaltenauswahl
INSERT INTO (col2, col4) VALUES (1, 'Wert 1')
```

```sql
-- Mehrere Zeilen
INSERT INTO
```

COPY 

CREATE TABLE AS SELECT

SELECT * INTO [table_name] FROM ...

### Automatisiert

psql  

IDE, z. B. python (import pyodbc, import psycopg)


## Aufgabe 1

Erstellen Sie über pgAdmin und seinem ERD-Tool ein Datenmodell, das eine Anwendung in ihrem Studium oder ähnliches implementiert. Was Sie modellieren können Sie beliebig wählen. Achten Sie aber bitte darauf, folgende Punkte zu integrieren:

1) Das Datenmodell enthält ca. 5 Tabellen
2) mindestens **eine** 1:n, n:m Beziehung zwischen den Tabellen
3) Setzen Sie in ihrem Modell auch mindestens **eine** der 3 Integritätsbedingungen um, d. h.:
+ Domänenintegrität
+ Primärschlüssel (für alle Tabellen)
+ Fremdschlüssel (für die 1:n & n:m Beziehungen)
4) Füllen Sie die Tabellen mit ein paar Beispieldatensätzen (hier reichen wenige)

+ Provozieren Sie nun für jeden INSERT INTO Befehl eine Verletzung der Integritätsbedingungen. Wie sind die Fehlermeldungen?