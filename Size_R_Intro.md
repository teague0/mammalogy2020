---
title: "Size & Introduction to R"
author: "Teague O'Mara, Southeastern Louisiana University"
output:
      html_document: 
        keep_md: yes
---



#### Body Size
Body size is one of the most important aspect of biology, and people have been studying how various aspects of our biology scale with size, from the numbers of offspring, to metabolic rates, to lifespan and social group size. Mammals range in body size from the 1.5 g bumblebee bat (*Craseonycteris thonglongyai*) to the 180,000,000 g blue whale (*Balaenoptera musculus*)  
</br>


Most of these types of variables fall into the realm of life history or ecology. We'll talk in more detail about mammalian life history, but for now we'll use these kinds of data to do two things:  
1 - Explore some fundamental traits of mammals  
2 - Begin to be comfortable with data in R  
  
</br>

##### Why am I doing this to you?
Understanding and mastering the interpretation of data are essential to being a scientist and an informed citizen. We're going to take a data-driven approach for a lot of this course since it let's you learn to answer any question you might have and builds a valuable skill set. We'll use R because it's open source, one of the most commonly used analysis environments in biology, and it's free. We're using a cloud version of RStudio (https://rstudio.com/) that is a popular IDE for R. Using the cloud version lets us get around any installation issues (and me peek at your work), but if you want to continue to use R you should install it on your own computer.

We'll focuse on learning how to visualize data and then moving to slightly more complicated analyses. If you want some outside sources for sharpening your R skills, you can look at https://www.learnr4free.com/en/index.html. Mine Dogucu at UC Irvine has compiled a list of sources for beginners. Some of my favorites are:

* RStudio Cloud Primers: https://rstudio.cloud/learn/primers
* R for Data Science https://r4ds.had.co.nz/
* Swirl: https://swirlstats.com/students.html

And my go-tos for R code help:
* Google
* R Cookbook: http://www.cookbook-r.com/  

</br>

Let's take a minute to get familiar with the html document you're reading and the R Markdown (.Rmd) document that made it. Your data analysis & assignments will be made using Rmd files since it lets you create a decently formatted report of what you've done without any extra work.
</br>

##### Let's connect to some data
There are a number of ways to get data into R, and they all are based on the function called `read.table`. `read.csv` or `read.delim` are the most common to use to get information from your hard drive into R, but we'll mostly be using data that I've stored on Google Drive, Github, or pre-loaded into your workspace.  
</br>

We'll begin exploring more about mammals using the PanTHERIA Database. This is a database compiled from the literature & some models to describe biological patterns in mammals and published in 2009 as a data paper in *Ecology*. This (and many other data sets) can be downloaded from the Ecological Data Wiki (https://ecologicaldata.org/home). 
![PanTheria](./images/PanTheria.png)
</br> 
</br>
For this exercise we'll connect directly to a version of the PanTHERIA Data that is stored on Dr. O'Mara's Github and read this into R using `read.csv`.


```r
library(tidyverse) #Note -- you only have to do this once per R Session
mammals <- read.csv("https://github.com/teague0/mammalogy2020/raw/master/data/PanTheriaData.csv")
```
**What's happening here**
`library()` is telling R to load up some independently-developed packages that were installed called `tidyverse.` There is a lot of functionality in R (often called base R), but one of the great things about it is that it's extendable, and these extensions are called packages or libraries. R is awesome, but pretty inconsistent in its language. The `tidyverse` takes care of that by creating some new wrappers and philosophy of data management that remain consistent across a lot of functions. It's philosphy is sort of like learning a language. If you understand some of the grammar, it makes understanding meaning a little easier.

> mammals <- read.csv(...)  

This pulls the data in to an object (a data frame -- like a spreadsheet) called mammals using the function `read.csv` and connects to the url of a .csv file stored on Github. If you look to the Global Environment panel on the right, you'll see that mammals is sitting there with 5416 obs of 58 variables. If you click on it, the data frame will be opened in a viewer window. R is an object-oriented language, which means that it's always looking for a noun (the object) for a verb to work on (the function).  

</br>
Let's see what is in this thing called mammals. Type `mammals` in to the Console. What happens?  

Did you notice all of the NA values? R doesn't like blanks or missing values, so it fills them with NA. In this case, the NAs were already entered to make sure that the data are read correctly.  

But, this is a little hard to read if we want to know what all of the variables are in this big data set. Instead, type in names(mammals) to see the names of the variables included.


```r
names(mammals)
```

```
##  [1] "Subclass"                "Superorder"             
##  [3] "Order"                   "Order_old"              
##  [5] "Family"                  "Genus"                  
##  [7] "Species"                 "Binomial"               
##  [9] "ActivityCycle"           "AdultBodyMass_g"        
## [11] "AdultForearmLen_mm"      "AdultHeadBodyLen_mm"    
## [13] "AgeatEyeOpening_d"       "AgeatFirstBirth_d"      
## [15] "BasalMetRate_mLO2hr"     "BasalMetRateMass_g"     
## [17] "DietBreadth"             "DispersalAge_d"         
## [19] "GestationLen_d"          "HabitatBreadth"         
## [21] "HomeRange_km2"           "HomeRange_Indiv_km2"    
## [23] "InterbirthInterval_d"    "LitterSize"             
## [25] "LittersPerYear"          "MaxLongevity_m"         
## [27] "NeonateBodyMass_g"       "NeonateHeadBodyLen_mm"  
## [29] "PopulationDensity_n.km2" "PopulationGrpSize"      
## [31] "SexualMaturityAge_d"     "SocialGrpSize"          
## [33] "TeatNumber"              "Terrestriality"         
## [35] "TrophicLevel"            "WeaningAge_d"           
## [37] "WeaningBodyMass_g"       "WeaningHeadBodyLen_mm"  
## [39] "References"              "AdultBodyMass_g_EXT"    
## [41] "LittersPerYear_EXT"      "NeonateBodyMass_g_EXT"  
## [43] "WeaningBodyMass_g_EXT"   "GR_Area_km2"            
## [45] "GR_MaxLat_dd"            "GR_MinLat_dd"           
## [47] "GR_MidRangeLat_dd"       "GR_MaxLong_dd"          
## [49] "GR_MinLong_dd"           "GR_MidRangeLong_dd"     
## [51] "HuPopDen_Min_n.km2"      "HuPopDen_Mean_n.km2"    
## [53] "HuPopDen_5p_n.km2"       "HuPopDen_Change"        
## [55] "Precip_Mean_mm"          "Temp_Mean_01degC"       
## [57] "AET_Mean_mm"             "PET_Mean_mm"
```
</br>
This is a little better. It tells us all of the different variable names. They are a little coded to make it easier to read them, and most of them have units attached (like `AdultBodyMass_g`). If there are some variables that are confusing, we can read up on the metadata for the file here: http://esapubs.org/archive/ecol/E090/184/metadata.htm. Metadata are data (usually descriptions) about data. For example, `ActivityCycle` is coded as (1) nocturnal only, (2) nocturnal/crepuscular, cathemeral, crepuscular or diurnal/crepuscular and (3) diurnal only. Without the metadata we wouldn't understand that. 
  
  
#### Making a plot
Let's get right to it. Let's make a plot to see what some of this mammal data looks like. Let's make box plots of each Order's adult body mass. Box plots are great for showing both central tendency & variation of a group. Box plots in R show the median (line in the box), and the box highlights the Interquartile Range (25% - 75% of the data). The ends of the 'whiskers' show the minimum of the data (Min value of data = Q1 - 1.5 * IQR) and maximum of the data (Min value of data = Q1 - 1.5 * IQR). The dots are potential outliers beyond that range.

We'll plot in `ggplot`. It's one of the most powerful, consistent, and flexible ways to make nice figures in R. There is a lot of good help through Google, and I usually run to R-Cookbook for help (http://www.cookbook-r.com/Graphs/).


```r
ggplot(mammals, aes(x = Order, y = AdultBodyMass_g))+
  geom_boxplot()
```

![](Size_R_Intro_files/figure-html/unnamed-chunk-3-1.png)<!-- -->
  
Congrats! We have a first plot. It's not a useful plot, but it did something! The first thing we see is that there is a huge range in the data. So it would make this easier if we transformed the body masses by log10 to even things out a bit. Also, the labels are impossible to read. Let's turn these 90° so that they are legible. 


```r
ggplot(mammals, aes(x = Order, y = log10(AdultBodyMass_g)))+ #log10 transform body mass
  geom_boxplot()+ 
  theme(axis.text.x = element_text(angle=90, vjust=0.5, size=10)) #flip the X-axis labs around to make them legible
```

```
## Warning: Removed 1874 rows containing non-finite values (stat_boxplot).
```

![](Size_R_Intro_files/figure-html/unnamed-chunk-4-1.png)<!-- -->
  
That's better! We now see that Order with the huge amount of variation is the Cetartiodactyla. There are also a few Orders that have very little variation, mostly because they only have a few living members (or only 1, like Tubilidentata -- the aardvark).  

Let's try a scatterplot. Scatterplots are useful for looking at the relationships between 2 (or 3) variables. Since body size should impact how much energy an animal uses, let's see the relationship with basal metabolic rate. In the metadata `BasalMetRateMass_g` is the body mass of the animals that the variable `BasalMetRate_mLO2hr` was measured on, so we'll use that, and log10 transform everything. We'll also color everything by Subclass -- i.e., monotremes vs marsupials vs placentals since there are probalby major changes in those transitions. We'll move the legend to the bottom of the plot to have a bit more room. While we're at it, we can pretty up the axis labels too. 


```r
ggplot(mammals, aes(x = log10(BasalMetRateMass_g), 
                    y = log10(BasalMetRate_mLO2hr),
                    color = Subclass))+
  geom_point()+
  theme(legend.position = "bottom")+
  labs(x = "log(adult body mass (g))",
       y = "log(BMR ml O2 / hr)")
```

```
## Warning: Removed 4843 rows containing missing values (geom_point).
```

![](Size_R_Intro_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

From this plot we can see a few different things. First, it looks like BMR does scale pretty nicely with body mass, but there is some spread around that line, and one crazy outlier. A best-fit line or regression would be nice to have on that figure just to see if there are some Orders that are unusual compared to everyone else. We'll increase the transparency of the points (their alpha) to see if there is anything hiding in the dense areas, and change the color scheme just for fun.


```r
ggplot(mammals, aes(x = log10(BasalMetRateMass_g), 
                    y = log10(BasalMetRate_mLO2hr)))+
  geom_point(aes(color = Subclass), alpha = 0.7)+ #Note this change
  geom_smooth(aes(x = log10(BasalMetRateMass_g), 
                    y = log10(BasalMetRate_mLO2hr)),
                  method="lm", se=FALSE)+ #add in a linear regression without error around it
  scale_color_viridis_d()+ #change the color palette to viridis. _d = discrete (categorical)
  theme_bw()+ #I don't like the grey background
  theme(legend.position = "bottom")+
  labs(x = "log(adult body mass (g))",
       y = "log(BMR ml O2 / hr)")
```

```
## Warning: Removed 4843 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 4843 rows containing missing values (geom_point).
```

![](Size_R_Intro_files/figure-html/unnamed-chunk-6-1.png)<!-- -->
  
First off, you've now learned how to make box plots and scatter plots. That's 80% of good science figures right there. Congrats!  

Second, you can see in this plot that there:
1. Are a lot more Eutheria (placentals) than Metatheria (Marsupials) and Monotremes (Platypus, Echnidas)
2. Eutherians therefore set that regression. Metatherians & Monotremes generally fall below the line. What does this mean?
3. That crazy outlier is a Metatherian. Who is it?  
  
  
I want to know who that outlier is. I could add labels to the plot with the Genus, but that's going to be messy. Instead, I'm going to filter the data to only have the Metatheria and then a log10(MBR) that is over 4.


```r
mammals %>% dplyr::filter(Subclass == "Metatheria" & log10(BasalMetRate_mLO2hr)>4) 
```

```
##     Subclass       Superorder         Order     Order_old      Family     Genus
## 1 Metatheria Australdidelphia Diprotodontia Diprotodontia Acrobatidae Acrobates
##    Species           Binomial ActivityCycle AdultBodyMass_g AdultForearmLen_mm
## 1 pygmaeus Acrobates pygmaeus            NA           13.84                 NA
##   AdultHeadBodyLen_mm AgeatEyeOpening_d AgeatFirstBirth_d BasalMetRate_mLO2hr
## 1                  NA                65            212.91               14938
##   BasalMetRateMass_g DietBreadth DispersalAge_d GestationLen_d HabitatBreadth
## 1                 14           3             NA             NA             NA
##   HomeRange_km2 HomeRange_Indiv_km2 InterbirthInterval_d LitterSize
## 1       0.00596                  NA                  183        2.8
##   LittersPerYear MaxLongevity_m NeonateBodyMass_g NeonateHeadBodyLen_mm
## 1              2           86.4              0.01                    NA
##   PopulationDensity_n.km2 PopulationGrpSize SexualMaturityAge_d SocialGrpSize
## 1                  899.99                NA              272.11            25
##   TeatNumber Terrestriality TrophicLevel WeaningAge_d WeaningBodyMass_g
## 1          4             NA            2         97.5              3.44
##   WeaningHeadBodyLen_mm
## 1                    NA
##                                                                      References
## 1 543;955;1297;1412;1466;1760;1789;1822;1848;2484;2644;2655;2880;2966;2967;2969
##   AdultBodyMass_g_EXT LittersPerYear_EXT NeonateBodyMass_g_EXT
## 1                  NA                 NA                    NA
##   WeaningBodyMass_g_EXT GR_Area_km2 GR_MaxLat_dd GR_MinLat_dd GR_MidRangeLat_dd
## 1                    NA     1691399       -10.69       -39.13            -24.91
##   GR_MaxLong_dd GR_MinLong_dd GR_MidRangeLong_dd HuPopDen_Min_n.km2
## 1        153.63        138.09             145.86                  0
##   HuPopDen_Mean_n.km2 HuPopDen_5p_n.km2 HuPopDen_Change Precip_Mean_mm
## 1               12.18                 0            0.04          61.57
##   Temp_Mean_01degC AET_Mean_mm PET_Mean_mm
## 1            185.7      673.13     1288.68
```
What happened here? First off, this code only produced output in the console / screen. It didn't save anything because it wasn't assigned to an object. Next, I used a pipe ` %>% ` to pass the dataframe `mammals` to the function `filter`. I specified which package to use `dplyr::filter` because there are a lot of different bits of code floating around that use filter. I then ask for only the Metatheria who have the high metabolic rates. The result is 1 species.  
  
</br>

What is this creature? Do you think it's basal metabolic rate is so fast, or is this likely an error? How would you find this out?


#### Now for some homework.
Move on to the file Size_R_Intro_HW.Rmd to see what you'll do next.

