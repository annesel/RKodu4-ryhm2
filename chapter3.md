---
title       : Histogramm
description : ggplot2 histogramm




---
## Histogramm jaotuse iseloomustamiseks

```yaml
type: NormalExercise
key: 1e4fe34afc
lang: r
xp: 100
skills: 1
```

Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.


`@instructions`
- **Ülesanne 1** Lisa andmestikku uus tunnus nimega `ratio`, mille väärtuseks oleks kelneri saadud jootraha ja makstud arve jagatis.
- **Ülesanne 2** Täienda antud koodi nii, et tulemuseks oleks jootraha ja makstud arve suhte histogramm. Histogrammil vali intervallide arvuks 15.
- **Ülesanne 3** Kui joonis valmis, siis uuri veidi andmestikku: kas laudkond, kelle jootraha moodustas arvest rohkem kui poole käis lõunasöögil (*Lunch*) või õhtusöögil(*Dinner*)? Omista õige vastus  stringina (`"Lunch"` või `"Dinner"`) muutujale `erind`.

`@hint`
- Uue tunnuse leidmiseks peab leidma jagatise `jootraha$tip/jootraha$total_bill`.
- Histogrammi joonistamiseks pead  tunnuse `ratio` siduma `x`-teljega ja kasutama `geom_histogram()` elementi.
- Erandliku vaatluse andmestikust leidmiseks saad kasutada filtreerimist: `jootraha[jootraha$ratio > 0.5, ]`.

`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
```

`@sample_code`
```{r}
# tunnuste nimed andmestikus (total_bill on arve, tip on jootraha dollarites)
names(jootraha)

# Ülesanne 1: Uue tunnuse moodustamine
jootraha$_____ <- _______________


# Ülesanne 2:  Histogramm (ära muuda 'y = ..density..' osa koodist!)
ggplot(jootraha, aes(__ = __________, y = ..density..)) + geom_________


# Ülesanne 3: Kas erandlik laudkond käis õhtu või lõunasöögil?
erind <- "_______"

```

`@solution`
```{r}
# tunnuste nimed andmestikus (total_bill on arve, tip on jootraha dollarites)
names(jootraha)

# Ülesanne 1: Uue tunnuse moodustamine
jootraha$ratio <- jootraha$tip/jootraha$total_bill


# Ülesanne 2:  Histogramm (ära muuda 'y = ..density..' osa koodist!)
ggplot(jootraha, aes(x = ratio, y = ..density..)) + geom_histogram(bins = 15)


# Ülesanne 3: Kas erandlik laudkond käis õhtu või lõunasöögil?
erind <- "Dinner"

```

`@sct`
```{r}
#1
test_data_frame("jootraha",
                columns = "ratio",
                eq_condition = "equivalent",
                undefined_msg = "Oled andmestiku `jootraha` kustutanud, alusta uuesti.",
                undefined_cols_msg = "Uus tunnus `ratio` on andmestikku lisamata!",
                incorrect_msg = "Uue tunnuse `ratio` väärtused ei ole õiged. Alusta uuesti.")




#2 
test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli `ggplot` käsu argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli  ülesandes `aes(.)`  funktsiooni argumente.", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` elemendi lisamise käsus. Kontrolli, kas lisad sobiva elemendi. Vaata üle ka argumentide kirjapanek.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = FALSE, 
    scale_fail_msg = "Probleem on `scale_` käsus.",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = NULL,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)

 
 
 
 
 
 
test_object("erind", 
            eq_condition = "equal",
            eval = TRUE,
            undefined_msg = "Muutuja `erind` on defineerimata.",
            incorrect_msg = "Muutuja `erind` väärtus on vale.")
 


success_msg("Tubli! Üks ülesanne on veel histogrammi kohta.")


```




---
## Histogrammi värvi muutmine

```yaml
type: MultipleChoiceExercise
key: 62ca4f17a5
lang: r
xp: 50
skills: 1
```
Lisame histogrammi joonistamise käsku värvi järgmisel moel:
```{r}
ggplot(jootraha, aes(x = ratio, y = ..density..)) + 
        geom_histogram(aes(fill = "chartreuse"))
        
```


Vali õige vastusevariant, kuidas muutub histogrammi värv?


`@instructions`
- Tulemuseks oleval joonisel on histogrammi tulbad rohelist tooni.
- Tulemuseks oleval joonisel on histogrammi tulbad ikka hallid, kuid tulbad on raamistatud rohelisega.
- Tulemuseks oleval joonisel on histogrammi tulbad punast tooni.
- Tulemuseks oleval joonisel on histogrammi tulbad halli tooni, kuid tulbad on raamistatud punasega.
- Tulemuseks oleval joonisel on histogrammi tulbad rohelist tooni ja tulbad on raamistatud punasega.
- Tulpade täitevärvi määramiseks tuleks `fill` asemel kasutada argumenti `color`.



`@hint`
- Mõtle kas andmestikus on tunnus, mille nimi on *chartreuse*?

`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
jootraha$ratio <- jootraha$tip/jootraha$total_bill
```

`@sct`
```{r}
msg1 = "Vale vastus!"
msg2 = "Vale vastus!"
msg3 = "Õige! Kuna täitevärvi määramine on `aes()` funktsiooni argumendiks ja tunnust nimega *chartreuse* andmestikus pole, siis tekitatakse see tunnus (konstantse väärtusega *charteuse*) juurde. Punane värv on vaikimisi kasutatava  diskreetse värviskaala esimene värv, mis värvib siin ära määratud ühe grupi histogrammi."
msg4 = "Vale vastus!"
msg5 = "Vale vastus!"
msg6 = "Vale vastus! `color` määrab raami värvi, mitte täite."

test_mc(correct = 3, feedback_msgs = c(msg1, msg2, msg3, msg4, msg5, msg6))
```




