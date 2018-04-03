---
title: Einführung in DataCamp
description: >-
  Dieses Kapitel soll dazu dienen sich in DataCamp zurechtzufinden


---
## Beispiel: Vektoren

```yaml
type: NormalExercise
lang: r
xp: 10
skills: 1
key: a57baa03e8
```

An dieser Stelle finden Sie immer die Aufgabenstellung. 

Starten Sie zunächst mit einer einfachen Übung...

`@instructions`
- Definieren Sie einen Vektor, der aus den Elementen 1 bis 5 besteht.

`@hint`
c(1:5)


`@sample_code`
```{r}
# Dieses Fenster stellt den Editor dar, den Sie bereits aus RStudio kennnen und erlaubt es Skripte zu schreiben.
# Lösungscode wird immer in dieses Fenster geschrieben. Für Zwischenschritte können Sie aber auch direkt in der Konsole arbeiten.

# Wichtig: In dem auskommentierten Teil am Anfang dieses Skriptes finden Sie weitere Hinweise, wie die Aufgabe zu lösen ist.
# Im vorliegenden Beispiel lautet die Anweisung, die Lösung unter dem Objekt *testvektor* zu speichern.

testvektor <-
```
`@solution`
```{r}
testvektor <- c(1:5)
```
`@sct`
```{r}
test_error()
test_object("testvektor",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```





---
## Daten einlesen

```yaml
type: NormalExercise
lang: r
xp: 10
skills: 1
key: 235b491598
```



`@instructions`
Ein einfaches Beispiel soll das Einlesen von Daten mit `read.csv()` demonstrieren.

`@hint`



`@sample_code`
```{r}
# die Daten liegen in https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv

test <-
```
`@solution`
```{r}
test <- read.csv("https://www.uni-duesseldorf.de/redaktion/fileadmin/redaktion/Fakultaeten/Wirtschaftswissenschaftliche_Fakultaet/Statistik/Kurse/BW_09/db_aktie_Feiertage2NA.csv")
```
`@sct`
```{r}
test_object("test")
test_error()
success_msg("Sehr gut!")
```




