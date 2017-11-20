---
title       : Hajuvusdiagamm
description : Hajuvusdiagrammid ggplot2 paketiga
---
## Hajuvusdiagramm 1

```yaml
type: NormalExercise
key: d72ec247ad
lang: r
xp: 100
skills: 1
```

Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.


`@instructions`
- **Ülesanne 1** Täienda antud koodi nii, et tulemuseks oleks hajuvusdiagramm restoraniarve suuruse ja jootraha suuruse vahel. Siin vali *x*-teljele arve suuruse tunnus.
Hajuvusdiagrammi punktid värvi vastavalt sellele, mis nädalapäevaga oli tegu, värv lisa `geom_` funktsiooni kaudu. Kasutades sobivat `scale_<_>_hue` funktsiooni määra värvilegendis õige päevade järjekord, päevade nimed jäta lühendatud kujule, ära muuda legendi pealkirja.
- **Ülesanne 2** Mis päeval on tehtud kõige suurem arve? Omista selle päeva nimi muutujale `suurim`, kasuta päeva kirjapanekul sama lühendit ja kirjapilti kui on andmestikus.

`@hint`
- Hajuvusdiagrammi saamiseks kasuta `geom_point()` käsku.
- Värvi määramiseks lisa `geom_point()` argumendiks `aes()` funktsioon, selle funktsiooni abil saab nädalapäeva tunnuse siduda argumendiga `color`.
- Värviskaala muutmiseks kasuta `scale_color_hue()` funktsiooni, määrama peab päevade järjekorra, selleks sobib `limits` argument.

`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
```

`@sample_code`
```{r}
# tunnuste nimed andmestikus(total_bill on arve, tip on jootraha dollarites, day nädalapäev)
names(jootraha)

# Ülesanne1: Hajuvusdiagramm värvilisite punktidega
j1 <- ggplot(jootraha, aes(x = ______, y = _______)) + 
            geom____________  +
                       scale_______hue(________________)
j1


# Ülesanne 2: Suurima arvega päev
suurim  <- "_____"
```

`@solution`
```{r}
# tunnuste nimed andmestikus(total_bill on arve, tip on jootraha dollarites, day nädalapäev)
names(jootraha)

# Ülesanne 1: Hajuvusdiagramm värvilisite punktidega
j1 <- ggplot(jootraha, aes(x = total_bill, y = tip)) + 
            geom_point(aes(color = day)) +
                    scale_color_hue(limits = c("Thur", "Fri", "Sat", "Sun"))

j1


# Ülesanne 2: Suurima arvega päev
suurim  <- "Sat"

```





`@sct`
```{r}


test_or(
test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli `ggplot` käsu argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli  ülesandes `aes(.)`  funktsiooni argumente.", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` elemendi lisamise käsus. Kontrolli, kas lisad sobiva elemendi hajuvusdiagrammi tekitamiseks (punktid). Vaata üle ka argumentide kirjapanek `aes()` funktsioonis.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = TRUE, 
    scale_fail_msg = "Probleem on `scale_` käsus. Kasuta `scale_color_hue()` funktsiooni",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = NULL,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL), 
    {
    test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli `ggplot` käsu argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli  ülesandes `aes(.)`  funktsiooni argumente.", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` elemendi lisamise käsus. Kontrolli, kas lisad sobiva elemendi hajuvusdiagrammi tekitamiseks (punktid). Vaata üle ka argumentide kirjapanek `aes()` funktsioonis.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = FALSE, 
    scale_fail_msg = " Kontrolli skaala muutmist.",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = NULL,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)
    test_student_typed('breaks = c("Thur", "Fri", "Sat", "Sun")')
    }
)
 
 
 
 
 
 
test_object("suurim", 
            eq_condition = "equal",
            eval = TRUE,
            undefined_msg = "Muutuja `suurim` on defineerimata.",
            incorrect_msg = "Muutuja `suurim` väärtus on vale.")
 


success_msg("Esimene hajuvusdiagramm on valmis!")

```










---
## Hajuvusdiagramm 2

```yaml
type: NormalExercise
key: 45598b6491
lang: r
xp: 100
skills: 1
```


Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.




`@instructions`
- **Ülesanne 1** Täienda antud koodi nii, et tulemuseks oleks hajuvusdiagramm restoraniarve suuruse ja jootraha suuruse vahel. Siin vali *x*-teljele arve suuruse tunnus.
Hajuvusdiagrammi punktid värvi vastavalt sellele, mis soost arve maksjaga oli tegu, punkti kuju määra selle järgi kas laudkonnas oli suitsetaja või mitte. Värv ja punktikuju lisa `geom_` funktsiooni kaudu. 
- **Ülesanne 2** Lisa vastava `ggplot2` paketi käsuga joonisele lineaarse regeressiooni sirge koos varieeruvust näitavate piiridega.

`@hint`
- Hajuvusdiagrammi saamiseks kasuta `geom_point()` käsku.
- Värvi ja punkti kuju määramiseks lisa `geom_point()` argumendiks `aes()` funktsiooni argumendid:   `color` ja `shape`.
- Funktsiooniga `stat_smooth()` saab lisada mudeli sirge, selleks pane `method = lm` argumendiks.

`@pre_exercise_code`
```{r}
library(ggplot2)
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
```

`@sample_code`
```{r}
# tunnuste nimed andmestikus(total_bill on arve, tip on jootraha dollarites, sex sugu, smoker suitsetaja olemasolu)
names(jootraha)

# Ülesanne 1: Hajuvusdiagramm värviliste ja eri kujuga punktidega
j1 <- ggplot(jootraha, aes(x = ______, y = _______)) + 
            geom____________  
j1


# Ülesanne 2:  Regressioonsirge lisamine
j1 + ________________________________
```

`@solution`
```{r}
# tunnuste nimed andmestikus(total_bill on arve, tip on jootraha dollarites, sex sugu, smoker suitsetaja olemasolu)
names(jootraha)

# Ülesanne 1: Hajuvusdiagramm värviliste ja eri kujuga punktidega
j1 <- ggplot(jootraha, aes(x = total_bill, y = tip)) + 
            geom_point(aes(color = sex, shape = smoker)) 
j1


# Ülesanne 2:  Regressioonsirge lisamine
j1 + stat_smooth(method = lm)

```





`@sct`
```{r}

test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli `ggplot` käsu argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli  ülesandes `aes(.)`  funktsiooni argumente.", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` elemendi lisamise käsus. Kontrolli, kas lisad sobiva elemendi hajuvusdiagrammi tekitamiseks (punktid). Vaata üle ka argumentide kirjapanek `aes()` funktsioonis.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = TRUE, 
    scale_fail_msg = "Probleem on `scale_` käsus.",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = NULL,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)

 
 
 
test_function("stat_smooth",
              args = "method",
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Kasuta  mudeli sirge lisamiseks  funktsiooni `stat_smooth()`.", 
              args_not_specified_msg = "Määra `stat_smooth()` argumendi `method` väärtus.",
              incorrect_msg = "Funktsiooni `stat_smooth()` argumendi `method` väärtus ei ole õige.")      
 
 

success_msg("Väga tubli!")

```

