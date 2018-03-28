---
title       : Termin 1 (inclass)
description : Übungen zu grundlegenden Funktionen mit R





---
## Wiederholung wesentlicher Inhalte

```yaml
type: NormalExercise
key: b7121efa78
lang: r
xp: 100
skills: 1
```
In dieser Aufgabe werden wir kurz den Zugriff auf Objekte unterschiedlicher Typen, das Einlesen von Datensätzen und einfache Berechnungen wiederholen. 

Alle Themen werden in den folgenden Aufgaben nochmals intensiv trainiert. 

`@instructions`

- speichern Sie den zweiten und fünften Eintrag des Vektors `kurse_vec` in `daten_auswahl1`
- speichern Sie nur die Kurse des Vektors `kurse_vec`, die über 18 liegen, in `daten_auswahl2`
- speichern Sie die Kurse der zweiten Spalte und Zeile 30 bis 40 aus `kurse_mat` in `daten_auswahl3`
- speichern Sie die Kurse Facebookaktie in `kurse_dataframe` in `daten_auswahl4`
- berechnen Sie mit den Daten aus `kurse_dataframe` die absolute Kursspanne für alle Handelstage und speichern Sie das Ergebnis in `daten_auswahl5`


`@hint`

`@pre_exercise_code`
```{r}
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")
library(dplyr)
aktienjoin <- full_join(facebook, deutschebank, by = "Date")
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)
remove(facebook)
remove(deutschebank)
aktien <- aktien[order(aktien$Date),]

kurse_vec <- c(aktien$db)
kurse_mat <- cbind(aktien$db,aktien$fb)
kurse_dataframe <- aktien
```

`@sample_code`
```{r}
# alle benötigten Objekte sind bereits eingelesen
daten_auswahl1 <- ___

daten_auswahl2 <- ___

daten_auswahl3 <- ___

daten_auswahl4 <- ___

daten_auswahl5 <- ___


```

`@solution`
```{r}
daten_auswahl1 <- kurse_vec[c(2,5)]

daten_auswahl2 <- kurse_vec[kurse_vec > 18]

daten_auswahl3 <- kurse_mat[ 30:40 , 2 ]

daten_auswahl4 <- kurse_dataframe$fb

daten_auswahl5 <- abs(kurse_dataframe$fb- kurse_dataframe$db)

```

`@sct`
```{r}
test_object("daten_auswahl1") 
test_object("daten_auswahl2")
test_object("daten_auswahl3")
test_object("daten_auswahl4")
test_object("daten_auswahl5")
test_error()
success_msg("Sehr gut!")

```
--- type:NormalExercise lang:r xp:100 skills:1 key:641f650cf3
## Einlesen von Datensätzen in R

Ihnen wurde der Preisverlauf der Deutschen Bank Aktie eines Jahres als `CSV-Datei` unter der angegebenen URL zur Verfügung gestellt.

(Quelle: de.finance.yahoo.com)


*** =instructions

- Lesen Sie die Daten ein und speichern Sie diese im Objekt `deutschebank`.
- Schauen Sie sich die Daten in der Konsole an.

*** =hint
- Nutzen Sie die `read.csv()` Funktion.
- Setzen Sie den Pfad als Argument der Funktion `read.csv()` in "Anführungszeichen".

*** =pre_exercise_code
```{r}
```

*** =sample_code
```{r}

# die Datei liegt in https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv
deutschebank <-


```

*** =solution
```{r}
# der Pfad der Datei ist 
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")


```

*** =sct
```{r}
test_function("read.csv", args = c("file"))
test_object("deutschebank")
#test_output_contains("deutschebank")
test_error()
success_msg("Sehr gut!")

```


--- type:NormalExercise lang:r xp:100 skills:1 key:5db7fe4b29
## Missing Values (I)

Gegeben ist der Datensatz `aktien` (bereits eingelesen). Er besteht aus den Kursdaten der Deutschen Bank (gehandelt an einer inländischen Börse) und facebook (gehandelt an einer US Börse). 
Durch die unterschiedlichen Feiertage in Deutschland und den USA fehlen einige Werte im Datensatz. Diese Felder sind mit `NA` gekennzeichnet und sind Gegenstand der vorliegenden Aufgabe.

(Quelle der Daten: de.finance.yahoo.com)


*** =instructions
Ersetzen Sie die NA Felder in dem Datensatz durch:

- den Durchschnitt der gesamten Zeitreihe. Hierfür können Sie die `mean()`-Funktion nutzen.
- in den [ ]-Klammern hinter der Variable stehen die Auswahlbedingungen. Beispielsweise: `spalte[ is.na(spalte) ]` gibt nur die Felder aus `spalte` zurück, in denen NA steht.

Ergänzen Sie die fehlenden Werte direkt im Datensatz `aktien`.

*** =hint

- `na.rm = TRUE` entfernt die NA Felder, zur Berechnung des Durchschnitts.
- `is.na(daten)` findet die NAs in den daten.

*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)

# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)
remove(facebook)
remove(deutschebank)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

```

*** =sample_code
```{r}
# Schaue, an welchen Tagen sich NAs befinden
aktien$Date[ is.na(aktien$db) ] # entspricht Zeile 7 und 145 im Datensatz
aktien$Date[ is.na(aktien$fb) ] # entspricht Zeile 197 und 222 im Datensatz

# Ersetzen Sie NAs in der Spalte 'db' durch den Durchschnitt der Spalte

mittelwert_db <- ___(___, na.rm = TRUE)

aktien$___[ 7 ] <- mittelwert_db
aktien$___[___] <- ___

# Ersetzen Sie NAs in der Spalte 'fb' durch den Durchschnitt der Spalte



```

*** =solution
```{r}
# Schaue, an welchen Tagen sich NAs befinden
aktien$Date[is.na(aktien$fb)]
aktien$Date[is.na(aktien$db)]

# Ersetzen Sie NAs in der Spalte 'db' durch den Durchschnitt der Spalte
aktien$db[is.na(aktien$db)] <- mean(aktien$db, na.rm = TRUE)

# Ersetzen Sie NAs in der Spalte 'fb' durch den Durchschnitt der Spalte
aktien$fb[is.na(aktien$fb)] <- mean(aktien$fb, na.rm = TRUE)


```

*** =sct
```{r}

test_function("mean", index = 1, args = c("x", "na.rm"))
test_function("mean", index = 2, args = c("x", "na.rm"))

test_object("aktien")
test_error()
success_msg("Sehr gut!")
```

--- type:NormalExercise lang:r xp:300 skills:1 key:df9a88a1a0
## Missing Values (II)

Gegeben ist wieder der Datensatz `aktien` (bereits eingelesen). Ersetzen Sie zwei NA's durch einen gleitenden Durchschnitt über 10 Tage mit den 5 vorherigen und den 5 folgenden Werten. 

Nützliche R Funktionen:

- `c(1,2,3,4,9)` bildet einen Vektor mit dem Inhalt 1,2,3,4,9.
- `c(1:4,9)` bildet den gleichen Vektor.
- `which(9 == c(1:4,9) )` gibt an, an welcher Stelle der Vektor dem Wert 9 entspricht (also = 5).

*** =instructions


- ersetzen Sie NA am "2016-04-14" (Deutsche Bank) durch den gleitenden Durchschnitt
- ersetzen Sie NA am "2017-01-16" (Facebook) durch den gleitenden Durchschnitt



*** =hint



*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)

# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)
remove(facebook)
remove(deutschebank)

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

```

*** =sample_code
```{r}

### deutschebank  (db)
# Finde die Zeile mit dem ersten Feiertag "2016-04-14" und speichere die Zeilennummer in index1
index1 <- which(___ == "___")
# durch Durchschnitt ersetzen
aktien$db[___] <- ___( aktien$db[ c((index1-___):(index1-___),(index1+___):(index1+___))] )
# Überprüfe neuen Wert
aktien$db[___]




### facebook (fb)
# Finde die Zeile mit dem ersten Feiertag "2017-01-16" und speichere die Zeilennummer in index2

# durch Durchschnitt ersetzen

# Überprüfe neuen Wert





```

*** =solution
```{r}
# Deutschebank
# Finde den Index 1
index1 <- which(aktien$Date == "2016-04-14")
# durch Durchschnitt ersetzen
aktien$db[index1] <- mean(c(aktien$db[c((index1-5):(index1-1),(index1+1):(index1+5))]))
# Neuer Wert
aktien$db[index1]


# Facebook 
# Finde den Index 3
index2 <- which(aktien$Date == "2017-01-16")
# durch Durchschnitt ersetzen
aktien$fb[index2] <- mean(c(aktien$fb[c((index2-5):(index2-1),(index2+1):(index2+5))]))
# Neuer Wert
aktien$fb[index2]



```

*** =sct
```{r}
test_function("which", args = "x", index = 1)
test_function("which", args = "x", index = 2)
test_object("index1")
test_object("index2")
test_function("mean", index = 1, args = c("x"))
test_function("mean", index = 2, args = c("x"))
test_output_contains("aktien$db[index1]")
test_output_contains("aktien$fb[index2]")

test_error()
success_msg("Sehr gut!")
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:09dde5f88b
## Missing Values (III)

Ihre Ergebnisse aus der letzten Aufgabe wurden geplotted. Sie sehen rechts den Plot für die facebook Aktie. Beim ersten Plot wurden die fehlenden Werte durch den gesamten Durchschnitt ersetzt, beim zweiten Plot wurden die fehlenden Werte durch den gleitenden 10er-Durchschnitt ersetzt.

Schauen Sie sich beide Plots an und vergleichen Sie die ersetzten Stellen (Feiertage am 16.01.17 und 20.02.17). 

Welche Methode eignet sich besser zur Ersetzung?
*** =instructions


- Gleitender 10er-Durchschnitt
- Durchschnitt gesamte Spalte

*** =hint


*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)

# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]
aktien2 <- aktien

# Gesamten durchschnitt setzen
aktien2$fb[is.na(aktien2$fb)] <- mean(aktien2$fb, na.rm = TRUE)

# Gleitender Durchschnitt setzen
index3 <- which(aktien$Date == "2017-01-16")
aktien$fb[index3] <- mean(c(aktien$fb[c((index3-5):(index3-1),(index3+1):(index3+5))]))
index4 <- which(aktien$Date == "2017-02-20")
aktien$fb[index4] <- mean(c(aktien$fb[c((index4-5):(index4-1),(index4+1):(index4+5))]))

# Plot von facebook Aktien mit NA durch gleitenden 10er Durchschnitt ersetzt
plot(aktien$Date, aktien$fb, type = "l", main = "Facebook Aktie 2016-2017 mit gleitendem 10er-Durchschnitt", xlab = "Datum", ylab = "Eroeffnungspreis ($)")
# Plot von facebook Aktien mit NA durch gesamten Durchschnitt ersetzt
plot(aktien2$Date, aktien2$fb, type = "l", main = "Facebook Aktie 2016-2017 mit gesamt Durchschnitt", xlab = "Datum", ylab = "Eröffnungspreis ($)")

```

*** =sct
```{r}
msg_bad <- "Leider falsch!"
msg_success <- "Richtig!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad))

```

--- type:NormalExercise lang:r xp:100 skills:1 key:860b4a4e28
## Berechnungen in R: Rendite (I)

Gegeben ist wieder der Datensatz `aktien` (bereits eingelesen). Berechnen Sie die diskreten Renditen für jeden Tag der Zeitreihe. 


*** =instructions

- berechnen Sie die diskreten Rendite für die Kurse der Deutsche Bank (`aktien$db`)

*** =hint

- Achten Sie darauf, dass die beiden Vektoren die gleiche Länge haben müssen.
- Die Länge eines Vektors bekommen Sie durch `length(vektor)` und ergibt 254.

*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)
# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

# Nehme Gletenden Durchschnitt um NAs zu füllen
index1 <- which(aktien$Date == "2016-04-14")
aktien$db[index1] <- mean(c(aktien$db[c((index1-5):(index1-1),(index1+1):(index1+5))]))
index2 <- which(aktien$Date == "2016-10-31")
aktien$db[index2] <- mean(c(aktien$db[c((index2-5):(index2-1),(index2+1):(index2+5))]))

```

*** =sample_code
```{r}
# Bedenken Sie, dass sich für den ersten Tag keine Rendite berechnen lässt.

# Erstelle einen Vektor mit den Einträgen aus aktien$db, OHNE den letzten Wert
x_tminus1 <- 
# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- 
# Berechnung der Rendite
renditeDB <- 


```

*** =solution
```{r}
# Erstelle einen vektor mit den Einträgen aus aktien$db. Lasse den letzten Eintrag weg.
x_tminus1 <- aktien$db[1:(length(aktien$db)-1)]

# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- aktien$db[2:length(aktien$db)]

# Berechnung der Rendite
renditeDB <- (x_t - x_tminus1) / x_tminus1



```

*** =sct
```{r}
test_object("x_tminus1")
test_object("x_t")
test_object("renditeDB")
test_error()
success_msg("Sehr gut!")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:ce73d9c96b
## Berechnungen in R: Rendite (II)

Der Datensatz liegt in `aktien`. Berechnen Sie die stetigen Renditen für jeden Tag der Zeitreihe. 



*** =instructions

- berechnen Sie die stetige Rendite für die Kurse der Deutsche Bank (`aktien$db`)



*** =hint

- Achten Sie darauf, dass die beiden Vektoren die gleiche Länge haben müssen.
- Die Länge eines Vektors bekommen Sie durch `length(vektor)` und ergibt 254.


*** =pre_exercise_code
```{r}
# Einlesen der Daten
deutschebank <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
facebook <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/fb_aktie2NA.csv")

# Zusammenführung der Daten
library(dplyr)
# Merging der Datensätze
aktienjoin <- full_join(facebook, deutschebank, by = "Date")

# Verkleinerung der Datensätze
aktien <- select(aktienjoin, Date, fb = Open.x, db = Open.y )
remove(aktienjoin)

# class Datum setzen
aktien$Date <- as.Date(aktien$Date)

# Nach Datum sortieren
aktien <- aktien[order(aktien$Date),]

# Nehme Gletenden Durchschnitt um NAs zu füllen
index1 <- which(aktien$Date == "2016-04-14")
aktien$db[index1] <- mean(c(aktien$db[c((index1-5):(index1-1),(index1+1):(index1+5))]))
index2 <- which(aktien$Date == "2016-10-31")
aktien$db[index2] <- mean(c(aktien$db[c((index2-5):(index2-1),(index2+1):(index2+5))]))


```

*** =sample_code
```{r}
# Erstellung Vektor mit Einträgen aus aktien$db. Entferne den letzten Eintrag.
x_tminus1 <- 
# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- 
# Berechnung der Rendite
logRenditeDB <- 


```

*** =solution
```{r}
# Erstellung Vektor mit Einträgen aus aktien$db. Entferne den letzten Eintrag.
x_tminus1 <- aktien$db[1:(length(aktien$db)-1)]
# Lasse ersten Eintrag weg, da Rendite erst ab 2. Tag berechenbar
x_t <- aktien$db[2:length(aktien$db)]
# Berechnung der Rendite
logRenditeDB <- log(x_t) - log(x_tminus1)


```

*** =sct
```{r}
test_object("x_tminus1")
