---
title       : Tulpdiagamm
description : Tulpdiagrammid  ggplot2  paketiga

---
## Tulpdiagamm esinemissagedustega

```yaml
type: NormalExercise
key: 21d676b9c0
lang: r
xp: 100
skills: 1
```
Töölaual on andmestik `jootraha`. Tegu on ühe kelneri kogutud andmetega paari kuu
pikkusest tööperioodist. Registreeritud on kõik laudkonnad, kes selle perioodi jooksul 
andsid jootraha. Kirja sai laudkonna arve suurus  dollarites (*total_bill*), saadud jootraha dollarites(*tip*),
arve maksja sugu (*sex*), kas laudkonnas oli suitsetajaid (*smoker*), nädalapäev(*day*), kas tegu oli lõuna 
või õhtuga(*time*) ja laudkonnas suurus (*size*).

Ülesandeks on nende andmete iseloomustamine graafikute abil, kasutades paketi **ggplot2** vahendeid.


`@instructions`

- **Ülesanne 1** Aktiveeri pakett **ggplot2**.
- **Ülesanne 2** Täienda joonise koodi<br>
    - sobiva `geom_<...>` funktsiooniga nii, et tulemuseks oleks siniste(`"royalblue"`) tulpadega tulpdiagramm, 
mis näitaks jootraha andnud laudkondade arvu nädalapäevade kaupa. 
    - Muuda *x*-telge sobiva `scale_x_<...>` funktsiooniga nii, et *x*-teljel oleksid nädalapäevad ajalises 
järjestuses ja päevade nimed pikalt väljakirjutatuna ("thursday", "friday", "saturday", "sunday", väiksed tähed!). Lisaks pane *x*- teljele nimi *Day of week*. 
    - Nimeta *y*-telg nimega *Counts* kasutades funktsiooni `ylab()`. 





`@hint`
- Tulpdiagammi saamiseks on vaja kasutada `geom_bar()` kihti. Selleks, et tulpade värv fikseerida kasuta argumenti `fill`, aga ära seda pane `aes(.)` funktsiooni argumendiks.
- Skaala muutmise funktsioonis `scale_x_discrete` peaks määrama argumendid: `name` telje nime muutmiseks, `limits` väärtuste järjekorra seadmiseks ja `labels` selleks, et päevanimed pikalt välja oleks kirjutatud.

`@pre_exercise_code`
```{r}
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
```

`@sample_code`
```{r}
# Tutvu andmetega
summary(jootraha)


# Ülesanne 1: aktiveeri pakett
_______(ggplot2)

# Ülesanne 2: täienda koodi
j1 <- ggplot(jootraha, aes(x = day)) + 
             geom________  + 
                    scale_x____________   +
                    ylab(label = "_________")
j1
```

`@solution`
```{r}
# Tutvu andmetega
summary(jootraha)


# Ülesanne 1: aktiveeri pakett
library(ggplot2)

# Ülesanne 2: täienda koodi
j1 <- ggplot(jootraha, aes(x = day)) + 
             geom_bar(fill = "royalblue") + 
                    scale_x_discrete(name = "Day of week", 
                             limits = c("Thur", "Fri", "Sat", "Sun"), 
                             labels = c("thursday", "friday", "saturday", "sunday")) +
                    ylab(label = "Counts")
j1
```

`@sct`
```{r}

test_function("library",
              args = NULL,
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Esimeses ülesandes kasuta funktsiooni `library()`.")     



#
#test_ggplot(1, exact_scale = TRUE)

test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli `aes(.)` argumente.", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` elemendi lisamise käsus.",
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




test_function("ylab",
              args = "label",
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Kasuta *y*-telje nime määramiseks funktsiooni `ylab()`. Liida see olemasolevale joonisele.", 
              args_not_specified_msg = "Määra *y*-telje nimi `label` argumendiga",
              incorrect_msg = "*y*-telje nimi on vale!")     



success_msg("Esimene joonis sai valmis, tubli!")


```




















---
## Tulpdiagamm osakaaludega
```yaml
type: NormalExercise
key: d9325fd201
lang: r
xp: 100
skills: 1
```

Töölaual on sama andmestik `jootraha`. Pakett **ggplot2** on juba aktiveeritud.


Selles ülesandes punktis kasuta *y* telje sildistamiseks paketi **scales** abi. Kui pakett on aktiveeritud, siis saab `scales_` käskudes kasutada väärtuste sildistamiseks mõningaid eeldefineeritud vorme, näiteks protsendi kuvamiseks `labels = percent`, dollarimärgi lisamiseks summadele `labels = dollar` jne.




`@instructions`
- **Ülesanne** Täienda antud koodi nii, et tulemuseks oleks tulpdiagramm, mis esitaks iga päeva kohta lõuna (*Lunch*) ja õhtusöökide (*Dinner*) osakaalud. St iga päeva kohta joonisel üks tulp, tulba sees jaotus lõuna ja õhtusöökide vahel antud erineva värviga ja tulba kõrgus summeeruks väärtuseks üks st esitaks tervikut. Muuda vaikimisi skaalasid joonisel järgnevalt:
    - sobiva  `scale_` funktsiooniga tee muudatused nii, et *y*-telje nimi oleks *Percentage* ja telje väärtused oleks sildistatud *%*-märgiga;
    - teise `scale_` funktsiooniga muuda värvilegendi pealkiri kujule *Time*;
    - *x*-telje nimi muuda samuti suurtähega algavaks: *Day*, kasuta nime muutmiseks siin `xlab()` funktsiooni.


`@hint`
- Tingliku jaotuse esitamiseks kasuta `geom` kihti kujul: `geom_bar(position = "fill")`.
- Skaala käsud mida vaja läheb on `scale_y_continuous()` ja `scale_fill_hue()`.


`@pre_exercise_code`
```{r}
# jootraha andmestik, reshape2
library(reshape2)
jootraha <-tips
jootraha$day <- factor(jootraha$day, levels = c("Thur", "Fri", "Sat", "Sun"))
library(ggplot2)
```

`@sample_code`
```{r}
# Vaata tunnuste nimed üle (nädalapäev: day, söögiaeg: time)
names(jootraha)

# Ülesanne : tulpdiagramm osakaaludega
library(scales)
j1 <- ggplot(jootraha, aes(x = ________, ________ = time)) + 
            geom___________  +
                    scale______________ + 
                    scale______________ +
                    xlab_______ 
j1

 

```

`@solution`
```{r}
# Vaata tunnuste nimed üle (nädalapäev: day, söögiaeg: time)
names(jootraha)

# Ülesanne : tulpdiagramm osakaaludega
library(scales)
j1 <- ggplot(jootraha, aes(x = day, fill = time)) + 
            geom_bar(position = "fill") +
                    scale_y_continuous(name = "Percentage", labels = percent) + 
                    scale_fill_hue(name = "Time") + 
                    xlab(label = "Day")
j1

```

`@sct`
```{r}
test_ggplot(index = 1, 
    all_fail_msg = NULL, 
    check_data = TRUE, 
    data_fail_msg = "Kontrolli argumendiks antud andmestikku.", 
    check_aes = TRUE, 
    aes_fail_msg = "Kontrolli `aes(.)` argumente.", 
    exact_aes = FALSE, 
    check_geom = TRUE, 
    geom_fail_msg = "Viga on `geom` elemendi lisamise käsus. Tegu peab olema tulpdiagammiga (`bar`). Lisaks peab määrama `position` argumendi.",
    exact_geom = FALSE, 
    check_geom_params = TRUE, 
    check_facet = TRUE, 
    facet_fail_msg = NULL,
    check_scale = TRUE, 
    scale_fail_msg = "Probleem on  ühes `scale_` käsus. *y*-telje muutmiseks kasuta `scale_y_continuous()`, värvilegendi korral `scale_fill_hue()`. *y*-telje korral kasuta väärtuste sildistamiseks **scales** paketis olemasolevat vormingut.",
    exact_scale = FALSE, 
    check_coord = TRUE, 
    coord_fail_msg = NULL, 
    exact_coord = FALSE, 
    check_stat = TRUE,
    stat_fail_msg = NULL,
    exact_stat = FALSE, 
    check_extra = NULL, extra_fail_msg = NULL, exact_extra = NULL, check = NULL)




test_function("scale_y_continuous",
              args = NULL,
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Kasuta *y*-telje nime määramiseks ja skaala esituse muutmiseks  funktsiooni `scale_y_continuous()`. Lisa argumendid telje nime ja väärtuste siltide jaoks.", 
              args_not_specified_msg = paste("Funktsioonis `scale_y_continuous()` on puudu argument " , c("`name`", "`label`")),
              incorrect_msg = paste("Funktsioonis `scale_y_continuous()` on vale väärtus  argumendil " , c("`name`", "`label`")))     





test_function("scale_fill_hue",
              args = NULL,
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Kasuta siin värvilegendi pealkirja muutmiseks  funktsiooni `scale_fill_hue()` argumendiga `name`.", 
              args_not_specified_msg = NULL,
              incorrect_msg = NULL)     





test_function("xlab",
              args = "label",
              index = 1,
              eval = TRUE,
              eq_condition = "equivalent",
              not_called_msg =  "Kasuta *x*-telje nime määramiseks funktsiooni `xlab()`. Liida see olemasolevale joonisele.", 
              args_not_specified_msg = "Määra *x*-telje nimi `label` argumendiga",
              incorrect_msg = "*x*-telje nimi on vale!")     







success_msg("Teine joonis sai valmis, tubli! Järgmises kahes ülesandes on vaadatud kahe arvulise tunnuse seose uurimiseks sobivat graafikutüüpi")
```























