---
title       : Joondiagramm ja karpdiagramm
description : ggplot2 joon- ja kapdiagramm


--- 
## Karpdiagrammid

```yaml
type: NormalExercise
key: b63d372b2c
lang: r
xp: 100
skills: 1
```

Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.

Andmestikus on arvutatud lisatunnus `ratio`, mis näitab jootraha ja arve suuruse suhet.



`@instructions`
- **Ülesanne 1** Täienda antud koodi sobivalt,  nii et tulemuseks oleks jootraha ja arve suuruse suhte karpdiagrammid laudkondade suuruse kaupa.
- **Ülesanne 2** Kohenda saadud joonist, lisades teljenimed `"laudkonna suurus"`, `"jootraha ja arve suhe"` käsuga `labs()`.
- **Ülesanne 3** Leia sagedustabel laudkonna suuruse tunnusele, omista see muutujale `tabel` ja prindi ekraanile.

`@hint`
-  Karpdiagammi joonistamiseks kasuta `geom_boxplot()` elementi.
- Kuna `size` on arvtunnus, mitte grupeeriv tunnus, siis on vaja `aes()` funktsiooni vaja lisada `group = size`.



`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
jootraha$ratio <- jootraha$tip/jootraha$total_bill
```


`@sample_code`
```{r}
# tunnuste nimed andmestikus (size - laudkonna suurus)
names(jootraha)

# Ülesanne 1: Karpdiagramm
j1 <- ggplot(jootraha, aes(x = _______, y = _______, group = _______)) + geom_________
j1

# Ülesanne 2: Täienda joonist teljenimedega
j1 + labs(________, ___________)

# Ülesanne 3: Sagedustabel
tabel <- ________________
tabel

```

`@solution`
```{r}
# tunnuste nimed andmestikus (size - laudkonna suurus)
names(jootraha)

# Ülesanne 1: Karpdiagramm
j1 <- ggplot(jootraha, aes(x = size, y = ratio, group = size)) + geom_boxplot()
j1

# Ülesanne 2: Täienda joonist teljenimedega
j1 + labs(x = "laudkonna suurus",  y = "jootraha ja arve suhe")

# Ülesanne 3: Sagedustabel
tabel <- table(jootraha$size)
tabel

```

`@sct`
```{r}

test_student_typed("group = size", not_typed_msg = "Kas määrasid `ggplot()` käsus `aes()` argumendi `group` väärtuseks `size`?" ) 
 

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
    check_scale = TRUE, 
    scale_fail_msg = "Probleem on `scale_` käsus. ",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = NULL,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)

 
test_student_typed("group = size", not_typed_msg = "Kas määrasid argumendi `group` väärtuseks `size`?" ) 
 
 
test_function("labs",
              args = NULL,
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Kasuta  teljenimede määramiseks funktsiooni `labs()`, argumentidega `x` ja `y`.", 
              args_not_specified_msg = NULL,
              incorrect_msg = NULL)     

test_student_typed("laudkonna suurus", not_typed_msg = "Pane *x*-teljele nimi `laudkonna suurus`.")



test_student_typed("jootraha ja arve suhe", not_typed_msg = "Pane *y*-teljele nimi `jootraha ja arve suhe`.")
 
 
 
test_function("table",
              args = NULL,
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Kasuta viimases ülesanedes funktsiooni `table`.", 
              args_not_specified_msg = NULL,
              incorrect_msg = NULL)    
 
 
test_object("tabel", 
            eq_condition = "equal",
            eval = TRUE,
            undefined_msg = "Sagedustabel `tabel` on defineerimata.",
            incorrect_msg = "Sagedustabeli `tabel` sisu on vale.")
 


success_msg("Karpdiagrammide joonis sai valmis, tubli! Karpdiagramme saab kasutada arvulisel skaalal muutuva tunnuse uurimiseks teise tunnuse gruppides. Grupitunnus on tüüpiliselt mingi faktortunnus, aga võib olla ka arvuline nagu siin ülesandes.")



```


---
## Joondiagramm 1

```yaml
type: NormalExercise
key: 45f6582534
lang: r
xp: 100
skills: 1
```

Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.
 

`@instructions`
- **Ülesanne 1** Lisa andmestikku uus tunnus, mis näitaks kui suur on jootraha suurus ühe inimese kohta laudkonnas, st jaga jootraha suurus laudkonna inimeste arvuga. Uue tunnuse nimeks vali `tip.per.person`
- **Ülesanne 2** Täienda antud joonise koodi nii, et tulemuseks oleks joondiagramm, mille abil saaks näha kuidas muutub keskmine inimese kohta makstud jootraha vastavalt laudkonna suurusele.

`@hint`
-  Joondiagrammi saamiseks peab iga laudkonna suuruse kohta olema leitud keskmine inimesekohta antud jootraha suurus. 
- Keskmise arvutamise funktsioon tuleb `stat_summary()` käsus anda `fun.y` väärtuseks.
- Joondiagramm tekib, kui `stat_summary()` käsus argumendi `geom` väärtuseks on `"line"`.

`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
```

`@sample_code`
```{r}
# tunnuste nimed andmestikus (total_bill on arve, tip on jootraha dollarites, size laudkonna suurus)
names(jootraha)

# Ülesanne 1: Uue tunnuse moodustamine
jootraha$_____ <- _______________


# Ülesanne 2: Joondiagramm
ggplot(jootraha, aes(x = _______, y = ____________)) + 
      stat_summary(geom = "_______",  fun.y = _________)  + 
                    scale_x_continuous(breaks = 1:6)


```


`@solution`
```{r}
# tunnuste nimed andmestikus (total_bill on arve, tip on jootraha dollarites, size laudkonna suurus)
names(jootraha)

# Ülesanne 1: Uue tunnuse moodustamine
jootraha$tip.per.person <- jootraha$tip/jootraha$size


# Ülesanne 2: Joondiagramm
ggplot(jootraha, aes(x = size, y = tip.per.person)) + 
      stat_summary(geom = "line",  fun.y = mean) + 
                    scale_x_continuous(breaks = 1:6)

```





`@sct`
```{r}
test_data_frame("jootraha",
                columns = "tip.per.person",
                eq_condition = "equivalent",
                undefined_msg = "Oled andmestiku `jootraha` kustutanud, alusta uuesti.",
                undefined_cols_msg = "Uus tunnus `tip.per.person` on andmestikku lisamata!",
                incorrect_msg = "Uue tunnuse `tip.per.person` väärtused ei ole õiged. Alusta uuesti.")




test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli `ggplot` käsu argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli  ülesandes `aes(.)`  funktsiooni argumente.", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` argumendis. Vaja on joondiagrammi, seega `geom = line`.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = TRUE, 
    scale_fail_msg = "Probleem on `scale_` käsus.  ",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = "Kontrolli `stat_summary()` käsu argumente. *y*-teljele on vaja arvutada keskväärtus, kas andsid keskväärtuse  arvutamise funktsiooni üheks argumendiks?" ,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)



success_msg("Ühe grupi joondiagramm sai valmis, väga tubli! Järgmistes ülesannetes on vaadatud grupitunnuse lisamist sellele graafikule.")



```








---
## Joondiagramm 2

```yaml
type: NormalExercise
key: f83ab3a0d2
lang: r
xp: 100
skills: 1
```

Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.

Andmestikus on olemas tunnus, mis näitab jootraha suurust ühe inimese kohta laudkonnas. Tunnuse nimi on `tip.per.person`.
 
 
Tee eelmise ülesandega sarnane joonis, kuid nüüd lisa soo tunnus nii, et graafikule tekiks kaks joont: üks meeste makstud jootraha kohta ja teine naiste jootraha kohta. Jooned olgu erinevat värvi.

`@instructions`
- **Ülesanne** Täienda antud joonise koodi nii, et tulemuseks oleks joondiagramm, mille abil saaks näha kuidas muutub keskmine inimese kohta makstud jootraha vastavalt laudkonna suurusele grupeerituna soo järgi. Soo grupid olgu tähistatud erineva värviga.

`@hint`
-  Joone värvi määramiseks tunnuse järgi, lisa `aes()` käsku  argumendi `color` väärtuseks vastav tunnus.

`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
jootraha$tip.per.person <- jootraha$tip/jootraha$size
```

`@sample_code`
```{r}
# tunnuste nimed andmestikus 
names(jootraha)

 

# Ülesanne : Joondiagramm (soo kaupa)
ggplot(jootraha, aes(_____________________________)) + 
        stat_summary(geom = "_______",  fun.y = _________)  + 
                    scale_x_continuous(breaks = 1:6)


```


`@solution`
```{r}
# tunnuste nimed andmestikus (total_bill on arve, tip on jootraha dollarites)
names(jootraha)

# Ülesanne : Joondiagramm (soo kaupa)
ggplot(jootraha, aes(x = size, y = tip.per.person, color = sex)) +
        stat_summary(geom = "line",  fun.y = mean) + 
                    scale_x_continuous(breaks = 1:6)

```






`@sct`
```{r}
test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli `ggplot` käsu argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli  ülesandes `aes(.)`  funktsiooni argumente. Kas lisasid soo tunnuse värvi määrama?", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` argumendis. Vaja on joondiagrammi, seega `geom = line`.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = TRUE, 
    scale_fail_msg = "Probleem on `scale_` käsus.  ",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = "Kontrolli `stat_summary()` käsu argumente. *y*-teljele on vaja arvutada keskväärtus, kas andsid keskväärtuse  arvutamise funktsiooni üheks argumendiks?" ,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)


success_msg("Super! Järgmine ülesanne on viimane!")



```









---
## Joondiagramm 3

```yaml
type: NormalExercise
key: df58425458
lang: r
xp: 100
skills: 1
```

Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.

Andmestikus on olemas tunnus, mis näitab jootraha suurust ühe inimese kohta laudkonnas. Tunnuse nimi on `tip.per.person`.
 
 
Tee eelmise ülesandega sarnane joonis, kuid nüüd lisa soo tunnus nii, et graafikule tekiks kaks sama värvi, kuid erinevat tüüpi joont. Joone tüübi määramiseks kasuta `linetype` argumenti.



`@instructions`
- **Ülesanne** Täienda antud joonise koodi nii, et tulemuseks oleks joondiagramm, mille abil 
saaks näha kuidas muutub keskmine inimese kohta makstud jootraha vastavalt laudkonna suurusele grupeerituna soo järgi, soo grupid olgu tähistatud erineva joonetüübiga (aga sama värvi joon).

`@hint`
-  Joone tüübi määramiseks tunnuse järgi, lisa `aes()` käsku  argumendi `linetype` väärtuseks vastav tunnus.


`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
jootraha$tip.per.person <- jootraha$tip/jootraha$size
```

`@sample_code`
```{r}
# tunnuste nimed andmestikus 
names(jootraha)

 

# Ülesanne : Joondiagramm (soo kaupa)
ggplot(jootraha, aes(_____________________________)) + 
        stat_summary(geom = "_______",  fun.y = _________)  + 
                    scale_x_continuous(breaks = 1:6)

```


`@solution`
```{r}
# tunnuste nimed andmestikus (total_bill on arve, tip on jootraha dollarites)
names(jootraha)

# Ülesanne : Joondiagramm (soo kaupa)
ggplot(jootraha, aes(x = size, y = tip.per.person, linetype = sex)) + 
        stat_summary(geom = "line",  fun.y = mean) +
                    scale_x_continuous(breaks = 1:6)

```




`@sct`
```{r}
test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli `ggplot` käsu argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli  ülesandes `aes(.)`  funktsiooni argumente. Kas lisasid soo tunnuse joone tüüpi `linetype` määrama?", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` argumendis. Vaja on joondiagrammi, seega `geom = line`.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = TRUE, 
    scale_fail_msg = "Probleem on `scale_` käsus.  ",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = "Kontrolli `stat_summary()` käsu argumente. *y*-teljele on vaja arvutada keskväärtus, kas andsid keskväärtuse arvutamise funktsiooni üheks argumendiks?" ,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)



success_msg("Väga tubli, viimane ülesanne sai tehtud! Võta kommi!")


```

