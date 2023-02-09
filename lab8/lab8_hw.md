---
title: "Lab 8 Homework"
author: "Deon Vasquez"
date: "2023-02-09"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
```

## Install `here`
The package `here` is a nice option for keeping directories clear when loading files. I will demonstrate below and let you decide if it is something you want to use.  

```r
#install.packages("here")
library(here)
```

```
## here() starts at C:/Users/vasqu/OneDrive/Desktop/BIS15W2023_dvasquez
```

## Data
For this homework, we will use a data set compiled by the Office of Environment and Heritage in New South Whales, Australia. It contains the enterococci counts in water samples obtained from Sydney beaches as part of the Beachwatch Water Quality Program. Enterococci are bacteria common in the intestines of mammals; they are rarely present in clean water. So, enterococci values are a measurement of pollution. `cfu` stands for colony forming units and measures the number of viable bacteria in a sample [cfu](https://en.wikipedia.org/wiki/Colony-forming_unit).   

This homework loosely follows the tutorial of [R Ladies Sydney](https://rladiessydney.org/). If you get stuck, check it out!  

1. Start by loading the data `sydneybeaches`. Do some exploratory analysis to get an idea of the data structure.

```r
here()
```

```
## [1] "C:/Users/vasqu/OneDrive/Desktop/BIS15W2023_dvasquez"
```

```r
sydneybeaches <- read.csv(here("lab8","data", "sydneybeaches.csv"))
sydneybeaches
```

```
##      BeachId                    Region          Council                    Site
## 1       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 4       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 5       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 6       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 7       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 8       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 9       25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 10      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 11      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 12      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 13      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 14      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 15      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 16      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 17      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 18      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 19      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 20      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 21      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 22      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 23      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 24      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 25      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 26      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 27      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 28      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 29      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 30      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 31      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 32      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 33      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 34      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 35      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 36      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 37      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 38      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 39      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 40      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 41      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 42      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 43      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 44      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 45      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 46      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 47      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 48      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 49      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 50      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 51      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 52      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 53      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 54      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 55      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 56      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 57      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 58      25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 59      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 60      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 61      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 62      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 63      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 64      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 65      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 66      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 67      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 68      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 69      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 70      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 71      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 72      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 73      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 74      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 75      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 76      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 77      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 78      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 79      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 80      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 81      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 82      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 83      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 84      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 85      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 86      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 87      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 88      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 89      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 90      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 91      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 92      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 93      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 94      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 95      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 96      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 97      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 98      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 99      26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 100     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 101     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 102     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 103     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 104     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 105     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 106     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 107     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 108     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 109     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 110     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 111     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 112     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 113     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 114     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 115     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 116     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 117     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 118     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 119     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 120     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 121     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 122     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 123     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 124     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 125     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 126     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 127     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 128     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 129     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 130     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 131     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 132     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 133     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 134     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 135     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 136     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 137     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 138     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 139     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 140     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 141     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 142     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 143     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 144     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 145     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 146     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 147     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 148     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 149     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 150     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 151     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 152     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 153     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 154     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 155     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 156     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 157     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 158     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 159     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 160     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 161     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 162     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 163     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 164     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 165     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 166     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 167     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 168     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 169     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 170     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 171     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 172     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 173     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 174     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 175     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 176     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 177     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 178     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 179     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 180     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 181     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 182     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 183     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 184     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 185     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 186     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 187     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 188     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 189     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 190     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 191     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 192     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 193     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 194     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 195     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 196     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 197     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 198     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 199     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 200     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 201     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 202     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 203     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 204     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 205     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 206     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 207     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 208     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 209     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 210     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 211     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 212     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 213     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 214     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 215     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 216     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 217     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 218     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 219     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 220     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 221     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 222     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 223     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 224     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 225     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 226     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 227     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 228     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 229     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 230     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 231     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 232     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 233     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 234     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 235     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 236     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 237     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 238     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 239     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 240     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 241     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 242     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 243     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 244     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 245     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 246     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 247     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 248     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 249     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 250     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 251     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 252     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 253     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 254     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 255     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 256     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 257     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 258     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 259     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 260     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 261     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 262     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 263     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 264     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 265     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 266     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 267     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 268     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 269     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 270     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 271     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 272     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 273     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 274     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 275     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 276     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 277     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 278     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 279     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 280     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 281     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 282     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 283     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 284     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 285     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 286     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 287     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 288     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 289     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 290     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 291     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 292     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 293     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 294     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 295     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 296     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 297     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 298     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 299     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 300     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 301     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 302     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 303     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 304     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 305     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 306     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 307     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 308     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 309     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 310     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 311     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 312     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 313     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 314     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 315     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 316     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 317     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 318     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 319     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 320     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 321     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 322     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 323     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 324     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 325     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 326     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 327     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 328     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 329     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 330     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 331     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 332     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 333     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 334     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 335     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 336     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 337     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 338     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 339     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 340     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 341     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 342     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 343     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 344     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 345     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 346     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 347     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 348     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 349     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 350     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 351     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 352     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 353     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 354     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 355     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 356     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 357     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 358     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 359     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 360     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 361     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 362     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 363     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 364     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 365     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 366     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 367     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 368     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 369     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 370     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 371     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 372     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 373     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 374     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 375     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 376     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 377     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 378     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 379     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 380     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 381     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 382     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 383     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 384     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 385     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 386     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 387     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 388     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 389     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 390     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 391     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 392     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 393     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 394     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 395     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 396     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 397     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 398     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 399     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 400     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 401     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 402     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 403     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 404     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 405     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 406     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 407     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 408     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 409     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 410     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 411     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 412     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 413     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 414     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 415     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 416     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 417     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 418     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 419     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 420     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 421     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 422     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 423     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 424     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 425     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 426     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 427     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 428     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 429     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 430     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 431     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 432     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 433     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 434     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 435     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 436     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 437     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 438     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 439     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 440     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 441     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 442     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 443     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 444     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 445     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 446     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 447     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 448     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 449     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 450     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 451     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 452     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 453     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 454     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 455     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 456     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 457     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 458     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 459     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 460     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 461     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 462     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 463     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 464     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 465     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 466     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 467     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 468     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 469     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 470     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 471     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 472     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 473     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 474     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 475     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 476     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 477     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 478     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 479     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 480     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 481     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 482     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 483     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 484     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 485     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 486     22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 487     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 488     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 489     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 490     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 491     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 492     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 493     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 494     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 495     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 496     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 497     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 498     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 499     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 500     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 501     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 502     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 503     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 504     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 505     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 506     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 507     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 508     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 509     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 510     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 511     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 512     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 513     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 514     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 515     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 516     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 517     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 518     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 519     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 520     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 521     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 522     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 523     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 524     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 525     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 526     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 527     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 528     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 529     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 530     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 531     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 532     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 533     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 534     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 535     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 536     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 537     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 538     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 539     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 540     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 541     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 542     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 543     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 544     24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 545     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 546     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 547     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 548     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 549     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 550     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 551     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 552     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 553     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 554     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 555     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 556     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 557     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 558     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 559     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 560     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 561     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 562     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 563     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 564     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 565     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 566     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 567     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 568     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 569     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 570     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 571     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 572     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 573     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 574     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 575     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 576     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 577     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 578     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 579     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 580     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 581     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 582     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 583     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 584     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 585     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 586     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 587     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 588     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 589     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 590     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 591     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 592     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 593     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 594     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 595     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 596     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 597     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 598     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 599     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 600     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 601     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 602     23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 603     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 604     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 605     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 606     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 607     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 608     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 609     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 610     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 611     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 612     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 613     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 614     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 615     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 616     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 617     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 618     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 619     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 620     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 621     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 622     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 623     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 624     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 625     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 626     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 627     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 628     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 629     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 630     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 631     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 632     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 633     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 634     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 635     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 636     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 637     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 638     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 639     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 640     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 641     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 642     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 643     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 644     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 645     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 646     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 647     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 648     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 649     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 650     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 651     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 652     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 653     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 654     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 655     25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 656     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 657     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 658     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 659     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 660     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 661     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 662     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 663     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 664     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 665     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 666     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 667     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 668     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 669     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 670     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 671     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 672     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 673     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 674     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 675     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 676     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 677     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 678     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 679     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 680     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 681     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 682     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 683     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 684     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 685     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 686     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 687     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 688     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 689     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 690     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 691     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 692     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 693     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 694     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 695     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 696     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 697     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 698     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 699     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 700     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 701     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 702     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 703     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 704     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 705     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 706     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 707     26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 708     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 709     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 710     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 711     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 712     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 713     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 714     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 715     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 716     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 717     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 718     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 719     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 720     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 721     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 722     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 723     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 724     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 725     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 726     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 727     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 728     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 729     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 730     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 731     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 732     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 733     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 734     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 735     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 736     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 737     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 738     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 739     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 740     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 741     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 742     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 743     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 744     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 745     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 746     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 747     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 748     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 749     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 750     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 751     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 752     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 753     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 754     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 755     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 756     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 757     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 758     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 759     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 760     25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 761     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 762     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 763     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 764     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 765     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 766     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 767     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 768     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 769     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 770     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 771     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 772     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 773     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 774     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 775     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 776     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 777     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 778     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 779     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 780     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 781     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 782     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 783     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 784     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 785     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 786     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 787     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 788     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 789     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 790     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 791     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 792     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 793     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 794     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 795     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 796     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 797     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 798     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 799     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 800     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 801     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 802     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 803     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 804     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 805     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 806     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 807     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 808     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 809     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 810     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 811     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 812     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 813     29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 814     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 815     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 816     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 817     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 818     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 819     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 820     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 821     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 822     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 823     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 824     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 825     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 826     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 827     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 828     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 829     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 830     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 831     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 832     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 833     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 834     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 835     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 836     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 837     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 838     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 839     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 840     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 841     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 842     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 843     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 844     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 845     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 846     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 847     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 848     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 849     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 850     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 851     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 852     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 853     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 854     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 855     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 856     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 857     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 858     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 859     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 860     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 861     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 862     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 863     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 864     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 865     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 866     28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 867     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 868     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 869     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 870     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 871     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 872     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 873     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 874     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 875     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 876     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 877     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 878     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 879     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 880     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 881     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 882     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 883     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 884     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 885     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 886     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 887     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 888     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 889     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 890     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 891     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 892     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 893     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 894     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 895     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 896     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 897     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 898     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 899     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 900     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 901     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 902     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 903     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 904     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 905     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 906     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 907     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 908     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 909     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 910     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 911     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 912     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 913     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 914     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 915     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 916     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 917     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 918     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 919     27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 920     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 921     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 922     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 923     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 924     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 925     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 926     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 927     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 928     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 929     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 930     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 931     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 932     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 933     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 934     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 935     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 936     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 937     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 938     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 939     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 940     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 941     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 942     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 943     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 944     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 945     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 946     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 947     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 948     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 949     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 950     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 951     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 952     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 953     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 954     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 955     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 956     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 957     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 958     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 959     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 960     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 961     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 962     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 963     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 964     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 965     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 966     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 967     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 968     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 969     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 970     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 971     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 972     27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 973     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 974     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 975     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 976     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 977     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 978     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 979     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 980     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 981     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 982     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 983     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 984     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 985     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 986     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 987     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 988     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 989     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 990     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 991     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 992     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 993     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 994     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 995     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 996     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 997     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 998     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 999     27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1000    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1001    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1002    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1003    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1004    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1005    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1006    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1007    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1008    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1009    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1010    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1011    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1012    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1013    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1014    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1015    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1016    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1017    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1018    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1019    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1020    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1021    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1022    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1023    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1024    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1025    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1026    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1027    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1028    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1029    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1030    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1031    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1032    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1033    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1034    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1035    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1036    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1037    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1038    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1039    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1040    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1041    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1042    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1043    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1044    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1045    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1046    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1047    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1048    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1049    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1050    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1051    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1052    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1053    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1054    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1055    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1056    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1057    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1058    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1059    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1060    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1061    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1062    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1063    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1064    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1065    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1066    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1067    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1068    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1069    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1070    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1071    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1072    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1073    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1074    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1075    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1076    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1077    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1078    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1079    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1080    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1081    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1082    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1083    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1084    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1085    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1086    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1087    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1088    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1089    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1090    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1091    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1092    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1093    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1094    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1095    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1096    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1097    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1098    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1099    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1100    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1101    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1102    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1103    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1104    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1105    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1106    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1107    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1108    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1109    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1110    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1111    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1112    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1113    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1114    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1115    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1116    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1117    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1118    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1119    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1120    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1121    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1122    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1123    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1124    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1125    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1126    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1127    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1128    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1129    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1130    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1131    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1132    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1133    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1134    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1135    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1136    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1137    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1138    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1139    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1140    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1141    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1142    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1143    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1144    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1145    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1146    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1147    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1148    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1149    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1150    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1151    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1152    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1153    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1154    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1155    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1156    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1157    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1158    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1159    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1160    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1161    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1162    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1163    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1164    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1165    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1166    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1167    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1168    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1169    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1170    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1171    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1172    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1173    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1174    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1175    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1176    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1177    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1178    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1179    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1180    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1181    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1182    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1183    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1184    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1185    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1186    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1187    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1188    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1189    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1190    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1191    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1192    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1193    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1194    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1195    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1196    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1197    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1198    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1199    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1200    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1201    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1202    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1203    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1204    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1205    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1206    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1207    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1208    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1209    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1210    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1211    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1212    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1213    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1214    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1215    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1216    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1217    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1218    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1219    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1220    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1221    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1222    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1223    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1224    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1225    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1226    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1227    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1228    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1229    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1230    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1231    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1232    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1233    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1234    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1235    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1236    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1237    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1238    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1239    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1240    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1241    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1242    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1243    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1244    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1245    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1246    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1247    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1248    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1249    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1250    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1251    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1252    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1253    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1254    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1255    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1256    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1257    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1258    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1259    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1260    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1261    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1262    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1263    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1264    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1265    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1266    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1267    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1268    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1269    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1270    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1271    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1272    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1273    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1274    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1275    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1276    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1277    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1278    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1279    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1280    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1281    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1282    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1283    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1284    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1285    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1286    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1287    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1288    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1289    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1290    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1291    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1292    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1293    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1294    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1295    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1296    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1297    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1298    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1299    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1300    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1301    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1302    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1303    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1304    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1305    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1306    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1307    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1308    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1309    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1310    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1311    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1312    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1313    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1314    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1315    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1316    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1317    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1318    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1319    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1320    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1321    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1322    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1323    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1324    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1325    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1326    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1327    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1328    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1329    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1330    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1331    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1332    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1333    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1334    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1335    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1336    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1337    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1338    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1339    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1340    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1341    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1342    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1343    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1344    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1345    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1346    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1347    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1348    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1349    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1350    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1351    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1352    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1353    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1354    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1355    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1356    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1357    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1358    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1359    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1360    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1361    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1362    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1363    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1364    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1365    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1366    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1367    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1368    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1369    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1370    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1371    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1372    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1373    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1374    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1375    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1376    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1377    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1378    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1379    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1380    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1381    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1382    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1383    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1384    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1385    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1386    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1387    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1388    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1389    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1390    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1391    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1392    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1393    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1394    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1395    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1396    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1397    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1398    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1399    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1400    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1401    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1402    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1403    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1404    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1405    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1406    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1407    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1408    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1409    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1410    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1411    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1412    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1413    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1414    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1415    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1416    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1417    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1418    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1419    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1420    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1421    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1422    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1423    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1424    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1425    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1426    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1427    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1428    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1429    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1430    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1431    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1432    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1433    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1434    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1435    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1436    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1437    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1438    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1439    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1440    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1441    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1442    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1443    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1444    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1445    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1446    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1447    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1448    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1449    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1450    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1451    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1452    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1453    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1454    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1455    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1456    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1457    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1458    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1459    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1460    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1461    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1462    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1463    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1464    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1465    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1466    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1467    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1468    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1469    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 1470    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1471    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1472    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1473    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1474    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1475    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1476    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1477    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1478    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1479    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1480    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1481    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1482    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1483    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1484    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1485    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1486    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1487    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1488    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1489    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1490    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1491    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1492    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1493    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1494    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1495    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1496    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1497    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1498    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1499    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1500    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1501    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1502    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1503    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1504    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1505    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1506    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1507    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1508    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1509    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1510    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1511    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1512    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1513    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1514    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1515    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1516    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1517    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1518    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1519    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1520    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1521    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1522    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1523    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1524    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1525    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1526    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 1527    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1528    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1529    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1530    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1531    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1532    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1533    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1534    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1535    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1536    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1537    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1538    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1539    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1540    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1541    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1542    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1543    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1544    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1545    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1546    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1547    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1548    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1549    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1550    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1551    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1552    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1553    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1554    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1555    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1556    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1557    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1558    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1559    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1560    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1561    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1562    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1563    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1564    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1565    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1566    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1567    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1568    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1569    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1570    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1571    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1572    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1573    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1574    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1575    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1576    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1577    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1578    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1579    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1580    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1581    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1582    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1583    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 1584    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1585    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1586    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1587    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1588    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1589    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1590    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1591    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1592    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1593    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1594    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1595    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1596    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1597    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1598    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1599    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1600    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1601    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1602    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1603    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1604    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1605    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1606    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1607    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1608    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1609    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1610    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1611    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1612    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1613    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1614    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1615    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1616    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1617    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1618    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1619    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1620    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1621    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1622    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1623    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1624    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1625    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1626    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1627    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1628    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1629    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1630    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1631    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1632    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1633    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1634    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1635    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1636    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1637    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1638    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1639    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1640    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 1641    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1642    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1643    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1644    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1645    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1646    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1647    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1648    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1649    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1650    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1651    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1652    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1653    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1654    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1655    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1656    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1657    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1658    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1659    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1660    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1661    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1662    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1663    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1664    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1665    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1666    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1667    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1668    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1669    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1670    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1671    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1672    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1673    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1674    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1675    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1676    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1677    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1678    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1679    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1680    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1681    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1682    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1683    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1684    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1685    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1686    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1687    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1688    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1689    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1690    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1691    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1692    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1693    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1694    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1695    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1696    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1697    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 1698    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1699    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1700    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1701    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1702    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1703    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1704    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1705    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1706    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1707    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1708    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1709    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1710    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1711    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1712    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1713    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1714    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1715    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1716    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1717    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1718    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1719    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1720    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1721    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1722    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1723    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1724    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1725    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1726    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1727    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1728    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1729    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1730    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1731    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1732    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1733    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1734    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1735    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1736    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1737    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1738    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1739    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1740    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1741    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1742    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1743    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1744    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1745    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1746    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1747    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1748    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1749    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1750    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1751    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1752    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1753    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1754    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 1755    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1756    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1757    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1758    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1759    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1760    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1761    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1762    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1763    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1764    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1765    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1766    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1767    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1768    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1769    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1770    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1771    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1772    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1773    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1774    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1775    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1776    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1777    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1778    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1779    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1780    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1781    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1782    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1783    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1784    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1785    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1786    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1787    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1788    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1789    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1790    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1791    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1792    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1793    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1794    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1795    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1796    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1797    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1798    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1799    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1800    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1801    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1802    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1803    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1804    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1805    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1806    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1807    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1808    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1809    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1810    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1811    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 1812    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1813    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1814    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1815    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1816    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1817    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1818    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1819    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1820    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1821    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1822    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1823    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1824    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1825    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1826    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1827    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1828    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1829    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1830    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1831    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1832    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1833    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1834    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1835    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1836    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1837    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1838    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1839    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1840    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1841    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1842    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1843    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1844    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1845    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1846    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1847    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1848    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1849    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1850    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1851    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1852    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1853    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1854    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1855    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1856    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1857    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1858    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1859    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1860    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1861    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1862    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1863    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1864    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1865    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1866    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1867    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1868    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1869    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1870    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 1871    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1872    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1873    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1874    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1875    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1876    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1877    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1878    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1879    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1880    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1881    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1882    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1883    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1884    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1885    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1886    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1887    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1888    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1889    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1890    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1891    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1892    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1893    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1894    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1895    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1896    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1897    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1898    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1899    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1900    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1901    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1902    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1903    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1904    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1905    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1906    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1907    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1908    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1909    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1910    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1911    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1912    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1913    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1914    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1915    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1916    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1917    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1918    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1919    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1920    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1921    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1922    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1923    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1924    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1925    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1926    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1927    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1928    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1929    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1930    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1931    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1932    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1933    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 1934    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1935    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1936    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1937    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1938    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1939    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1940    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1941    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1942    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1943    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1944    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1945    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1946    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1947    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1948    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1949    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1950    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1951    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1952    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1953    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1954    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1955    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1956    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1957    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1958    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1959    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1960    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1961    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1962    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1963    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1964    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1965    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1966    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1967    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1968    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1969    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1970    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1971    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1972    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1973    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1974    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1975    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1976    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1977    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1978    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1979    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1980    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1981    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1982    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1983    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1984    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1985    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1986    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1987    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1988    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1989    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1990    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1991    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1992    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 1993    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1994    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1995    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1996    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1997    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1998    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 1999    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2000    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2001    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2002    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2003    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2004    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2005    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2006    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2007    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2008    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2009    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2010    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2011    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2012    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2013    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2014    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2015    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2016    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2017    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2018    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2019    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2020    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2021    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2022    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2023    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2024    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2025    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2026    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2027    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2028    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2029    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2030    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2031    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2032    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2033    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2034    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2035    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2036    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2037    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2038    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2039    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2040    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2041    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2042    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2043    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2044    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2045    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2046    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2047    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2048    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2049    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2050    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2051    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2052    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2053    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2054    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2055    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2056    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2057    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2058    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2059    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2060    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2061    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2062    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2063    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2064    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2065    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2066    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2067    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2068    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2069    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2070    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2071    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2072    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2073    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2074    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2075    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2076    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2077    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2078    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2079    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2080    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2081    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2082    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2083    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2084    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2085    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2086    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2087    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2088    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2089    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2090    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2091    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2092    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2093    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2094    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2095    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2096    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2097    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2098    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2099    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2100    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2101    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2102    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2103    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2104    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2105    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2106    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2107    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2108    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2109    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2110    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2111    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2112    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2113    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2114    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2115    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2116    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2117    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2118    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2119    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2120    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2121    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2122    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2123    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2124    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2125    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2126    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2127    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2128    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2129    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2130    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2131    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2132    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2133    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2134    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2135    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2136    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2137    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2138    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2139    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2140    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2141    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2142    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2143    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2144    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2145    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2146    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2147    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2148    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2149    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2150    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2151    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2152    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2153    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2154    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2155    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2156    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2157    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2158    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2159    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2160    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2161    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2162    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2163    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2164    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2165    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2166    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2167    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2168    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2169    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2170    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2171    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2172    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2173    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2174    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2175    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2176    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2177    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2178    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2179    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2180    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2181    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2182    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2183    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2184    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2185    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2186    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2187    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2188    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2189    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2190    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2191    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2192    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2193    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2194    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2195    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2196    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2197    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2198    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2199    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2200    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2201    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2202    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2203    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2204    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2205    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2206    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2207    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2208    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2209    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2210    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2211    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2212    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2213    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2214    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2215    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2216    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2217    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2218    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2219    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2220    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2221    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2222    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2223    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2224    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2225    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2226    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2227    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2228    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2229    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2230    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2231    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2232    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2233    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2234    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2235    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2236    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2237    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2238    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2239    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2240    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2241    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2242    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2243    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2244    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2245    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2246    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2247    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2248    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2249    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2250    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2251    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2252    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2253    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2254    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2255    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2256    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2257    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2258    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2259    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2260    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2261    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2262    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2263    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2264    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2265    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2266    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2267    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2268    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2269    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2270    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2271    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2272    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2273    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2274    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2275    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2276    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2277    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2278    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2279    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2280    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2281    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2282    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2283    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2284    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2285    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2286    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2287    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2288    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2289    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2290    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2291    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2292    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2293    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2294    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2295    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2296    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2297    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2298    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2299    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2300    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2301    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2302    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2303    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2304    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2305    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2306    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2307    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2308    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2309    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2310    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2311    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2312    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2313    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2314    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2315    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2316    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2317    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2318    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2319    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2320    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2321    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2322    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2323    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2324    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2325    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2326    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2327    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2328    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2329    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2330    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2331    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2332    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2333    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2334    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2335    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2336    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2337    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2338    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2339    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2340    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2341    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2342    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2343    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2344    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2345    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2346    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2347    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2348    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2349    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2350    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2351    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2352    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2353    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2354    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2355    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2356    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2357    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2358    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2359    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2360    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2361    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2362    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2363    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2364    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2365    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2366    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2367    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2368    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2369    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2370    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2371    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2372    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2373    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2374    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2375    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2376    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2377    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2378    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2379    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2380    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2381    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2382    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2383    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2384    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2385    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2386    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2387    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2388    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2389    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2390    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2391    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2392    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2393    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2394    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2395    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2396    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2397    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2398    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2399    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2400    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2401    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2402    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2403    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2404    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2405    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2406    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2407    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2408    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2409    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 2410    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2411    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2412    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2413    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2414    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2415    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2416    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2417    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2418    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2419    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2420    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2421    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2422    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2423    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2424    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2425    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2426    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2427    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2428    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2429    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2430    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2431    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2432    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2433    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2434    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2435    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2436    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2437    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2438    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2439    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2440    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2441    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2442    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2443    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2444    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2445    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2446    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2447    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2448    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2449    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2450    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2451    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2452    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2453    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2454    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2455    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2456    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2457    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2458    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2459    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2460    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2461    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2462    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2463    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2464    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2465    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2466    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2467    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 2468    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2469    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2470    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2471    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2472    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2473    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2474    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2475    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2476    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2477    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2478    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2479    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2480    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2481    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2482    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2483    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2484    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2485    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2486    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2487    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2488    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2489    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2490    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2491    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2492    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2493    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2494    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2495    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2496    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2497    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2498    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2499    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2500    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2501    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2502    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2503    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2504    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2505    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2506    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2507    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2508    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2509    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2510    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2511    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2512    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2513    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2514    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2515    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2516    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2517    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2518    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2519    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2520    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2521    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2522    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2523    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2524    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2525    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2526    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2527    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2528    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 2529    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2530    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2531    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2532    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2533    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2534    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2535    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2536    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2537    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2538    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2539    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2540    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2541    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2542    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2543    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2544    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2545    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2546    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2547    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2548    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2549    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2550    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2551    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2552    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2553    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2554    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2555    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2556    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2557    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2558    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2559    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2560    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2561    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2562    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2563    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2564    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2565    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2566    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2567    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2568    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2569    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2570    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2571    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2572    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2573    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2574    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2575    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2576    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2577    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2578    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2579    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2580    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2581    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2582    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2583    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2584    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2585    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2586    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2587    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2588    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2589    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2590    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 2591    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2592    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2593    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2594    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2595    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2596    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2597    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2598    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2599    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2600    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2601    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2602    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2603    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2604    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2605    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2606    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2607    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2608    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2609    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2610    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2611    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2612    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2613    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2614    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2615    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2616    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2617    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2618    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2619    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2620    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2621    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2622    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2623    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2624    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2625    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2626    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2627    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2628    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2629    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2630    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2631    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2632    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2633    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2634    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2635    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2636    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2637    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2638    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2639    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2640    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2641    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2642    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2643    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2644    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2645    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2646    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2647    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2648    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2649    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2650    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2651    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 2652    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2653    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2654    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2655    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2656    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2657    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2658    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2659    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2660    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2661    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2662    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2663    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2664    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2665    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2666    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2667    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2668    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2669    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2670    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2671    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2672    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2673    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2674    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2675    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2676    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2677    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2678    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2679    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2680    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2681    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2682    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2683    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2684    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2685    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2686    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2687    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2688    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2689    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2690    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2691    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2692    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2693    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2694    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2695    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2696    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2697    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2698    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2699    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2700    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2701    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2702    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2703    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2704    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2705    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2706    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2707    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2708    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2709    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2710    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2711    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2712    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 2713    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2714    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2715    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2716    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2717    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2718    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2719    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2720    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2721    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2722    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2723    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2724    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2725    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2726    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2727    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2728    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2729    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2730    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2731    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2732    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2733    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2734    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2735    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2736    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2737    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2738    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2739    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2740    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2741    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2742    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2743    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2744    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2745    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2746    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2747    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2748    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2749    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2750    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2751    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2752    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2753    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2754    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2755    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2756    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2757    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2758    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2759    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2760    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2761    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2762    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2763    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2764    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2765    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2766    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2767    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2768    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2769    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2770    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2771    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2772    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2773    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2774    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 2775    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2776    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2777    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2778    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2779    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2780    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2781    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2782    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2783    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2784    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2785    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2786    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2787    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2788    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2789    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2790    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2791    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2792    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2793    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2794    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2795    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2796    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2797    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2798    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2799    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2800    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2801    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2802    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2803    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2804    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2805    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2806    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2807    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2808    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2809    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2810    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2811    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2812    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2813    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2814    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2815    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2816    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2817    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2818    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2819    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2820    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2821    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2822    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2823    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2824    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2825    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2826    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2827    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2828    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2829    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2830    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2831    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2832    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2833    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2834    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2835    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 2836    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2837    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2838    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2839    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2840    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2841    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2842    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2843    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2844    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2845    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2846    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2847    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2848    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2849    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2850    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2851    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2852    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2853    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2854    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2855    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2856    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2857    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2858    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2859    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2860    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2861    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2862    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2863    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2864    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2865    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2866    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2867    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2868    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2869    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2870    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2871    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2872    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2873    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2874    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2875    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2876    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2877    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2878    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2879    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2880    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2881    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2882    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2883    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2884    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2885    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2886    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2887    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2888    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2889    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2890    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2891    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2892    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2893    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2894    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2895    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2896    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 2897    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2898    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2899    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2900    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2901    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2902    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2903    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2904    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2905    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2906    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2907    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2908    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2909    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2910    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2911    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2912    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2913    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2914    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2915    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2916    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2917    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2918    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2919    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2920    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2921    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2922    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2923    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2924    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2925    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2926    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2927    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2928    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2929    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2930    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2931    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2932    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2933    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2934    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2935    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2936    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2937    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2938    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2939    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2940    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2941    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2942    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2943    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2944    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2945    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2946    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2947    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2948    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2949    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2950    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2951    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2952    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2953    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2954    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2955    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2956    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2957    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 2958    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2959    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2960    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2961    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2962    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2963    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2964    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2965    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2966    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2967    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2968    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2969    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2970    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2971    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2972    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2973    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2974    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2975    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2976    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2977    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2978    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2979    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2980    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2981    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2982    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2983    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2984    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2985    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2986    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2987    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2988    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2989    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2990    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2991    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2992    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2993    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2994    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2995    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2996    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2997    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2998    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 2999    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3000    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3001    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3002    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3003    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3004    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3005    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3006    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3007    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3008    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3009    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3010    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3011    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3012    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3013    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3014    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3015    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3016    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3017    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3018    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3019    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3020    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3021    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3022    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3023    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3024    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3025    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3026    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3027    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3028    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3029    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3030    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3031    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3032    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3033    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3034    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3035    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3036    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3037    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3038    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3039    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3040    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3041    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3042    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3043    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3044    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3045    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3046    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3047    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3048    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3049    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3050    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3051    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3052    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3053    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3054    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3055    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3056    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3057    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3058    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3059    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3060    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3061    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3062    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3063    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3064    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3065    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3066    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3067    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3068    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3069    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3070    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3071    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3072    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3073    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3074    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3075    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3076    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3077    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3078    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3079    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3080    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3081    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3082    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3083    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3084    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3085    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3086    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3087    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3088    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3089    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3090    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3091    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3092    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3093    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3094    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3095    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3096    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3097    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3098    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3099    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3100    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3101    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3102    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3103    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3104    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3105    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3106    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3107    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3108    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3109    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3110    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3111    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3112    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3113    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3114    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3115    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3116    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3117    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3118    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3119    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3120    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3121    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3122    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3123    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3124    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3125    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3126    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3127    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3128    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3129    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3130    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3131    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3132    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3133    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3134    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3135    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3136    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3137    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3138    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3139    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3140    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3141    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3142    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3143    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3144    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3145    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3146    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3147    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3148    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3149    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3150    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3151    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3152    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3153    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3154    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3155    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3156    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3157    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3158    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3159    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3160    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3161    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3162    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3163    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3164    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3165    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3166    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3167    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3168    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3169    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3170    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3171    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3172    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3173    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3174    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3175    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3176    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3177    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3178    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3179    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3180    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3181    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3182    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3183    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3184    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3185    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3186    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3187    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3188    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3189    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3190    25.0 Sydney City Ocean Beaches Randwick Council          Clovelly Beach
## 3191    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3192    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3193    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3194    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3195    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3196    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3197    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3198    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3199    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3200    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3201    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3202    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3203    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3204    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3205    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3206    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3207    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3208    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3209    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3210    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3211    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3212    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3213    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3214    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3215    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3216    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3217    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3218    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3219    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3220    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3221    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3222    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3223    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3224    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3225    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3226    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3227    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3228    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3229    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3230    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3231    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3232    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3233    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3234    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3235    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3236    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3237    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3238    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3239    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3240    26.0 Sydney City Ocean Beaches Randwick Council            Coogee Beach
## 3241    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3242    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3243    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3244    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3245    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3246    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3247    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3248    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3249    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3250    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3251    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3252    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3253    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3254    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3255    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3256    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3257    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3258    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3259    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3260    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3261    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3262    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3263    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3264    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3265    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3266    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3267    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3268    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3269    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3270    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3271    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3272    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3273    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3274    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3275    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3276    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3277    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3278    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3279    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3280    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3281    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3282    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3283    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3284    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3285    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3286    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3287    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3288    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3289    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3290    25.9 Sydney City Ocean Beaches Randwick Council      Gordons Bay (East)
## 3291    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3292    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3293    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3294    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3295    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3296    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3297    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3298    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3299    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3300    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3301    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3302    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3303    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3304    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3305    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3306    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3307    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3308    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3309    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3310    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3311    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3312    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3313    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3314    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3315    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3316    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3317    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3318    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3319    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3320    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3321    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3322    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3323    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3324    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3325    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3326    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3327    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3328    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3329    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3330    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3331    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3332    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3333    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3334    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3335    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3336    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3337    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3338    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3339    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3340    29.0 Sydney City Ocean Beaches Randwick Council        Little Bay Beach
## 3341    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3342    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3343    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3344    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3345    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3346    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3347    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3348    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3349    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3350    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3351    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3352    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3353    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3354    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3355    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3356    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3357    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3358    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3359    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3360    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3361    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3362    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3363    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3364    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3365    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3366    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3367    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3368    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3369    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3370    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3371    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3372    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3373    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3374    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3375    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3376    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3377    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3378    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3379    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3380    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3381    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3382    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3383    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3384    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3385    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3386    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3387    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3388    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3389    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3390    28.0 Sydney City Ocean Beaches Randwick Council           Malabar Beach
## 3391    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3392    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3393    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3394    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3395    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3396    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3397    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3398    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3399    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3400    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3401    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3402    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3403    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3404    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3405    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3406    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3407    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3408    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3409    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3410    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3411    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3412    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3413    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3414    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3415    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3416    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3417    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3418    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3419    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3420    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3421    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3422    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3423    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3424    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3425    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3426    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3427    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3428    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3429    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3430    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3431    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3432    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3433    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3434    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3435    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3436    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3437    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3438    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3439    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3440    27.0 Sydney City Ocean Beaches Randwick Council          Maroubra Beach
## 3441    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3442    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3443    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3444    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3445    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3446    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3447    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3448    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3449    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3450    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3451    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3452    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3453    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3454    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3455    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3456    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3457    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3458    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3459    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3460    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3461    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3462    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3463    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3464    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3465    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3466    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3467    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3468    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3469    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3470    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3471    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3472    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3473    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3474    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3475    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3476    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3477    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3478    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3479    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3480    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3481    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3482    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3483    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3484    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3485    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3486    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3487    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3488    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3489    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3490    27.4 Sydney City Ocean Beaches Randwick Council    South Maroubra Beach
## 3491    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3492    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3493    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3494    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3495    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3496    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3497    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3498    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3499    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3500    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3501    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3502    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3503    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3504    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3505    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3506    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3507    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3508    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3509    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3510    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3511    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3512    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3513    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3514    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3515    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3516    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3517    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3518    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3519    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3520    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3521    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3522    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3523    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3524    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3525    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3526    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3527    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3528    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3529    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3530    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3531    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3532    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3533    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3534    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3535    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3536    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3537    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3538    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3539    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3540    27.3 Sydney City Ocean Beaches Randwick Council South Maroubra Rockpool
## 3541    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3542    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3543    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3544    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3545    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3546    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3547    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3548    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3549    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3550    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3551    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3552    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3553    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3554    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3555    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3556    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3557    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3558    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3559    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3560    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3561    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3562    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3563    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3564    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3565    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3566    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3567    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3568    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3569    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3570    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3571    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3572    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3573    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3574    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3575    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3576    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3577    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3578    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3579    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3580    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3581    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3582    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3583    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3584    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3585    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3586    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3587    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3588    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3589    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3590    22.0 Sydney City Ocean Beaches Waverley Council             Bondi Beach
## 3591    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3592    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3593    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3594    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3595    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3596    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3597    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3598    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3599    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3600    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3601    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3602    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3603    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3604    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3605    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3606    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3607    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3608    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3609    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3610    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3611    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3612    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3613    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3614    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3615    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3616    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3617    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3618    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3619    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3620    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3621    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3622    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3623    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3624    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3625    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3626    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3627    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3628    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3629    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3630    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3631    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3632    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3633    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3634    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3635    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3636    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3637    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3638    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3639    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3640    24.0 Sydney City Ocean Beaches Waverley Council            Bronte Beach
## 3641    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3642    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3643    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3644    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3645    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3646    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3647    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3648    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3649    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3650    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3651    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3652    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3653    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3654    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3655    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3656    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3657    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3658    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3659    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3660    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3661    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3662    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3663    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3664    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3665    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3666    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3667    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3668    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3669    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3670    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3671    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3672    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3673    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3674    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3675    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3676    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3677    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3678    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3679    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3680    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3681    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3682    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3683    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3684    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3685    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3686    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3687    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3688    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3689    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
## 3690    23.0 Sydney City Ocean Beaches Waverley Council          Tamarama Beach
##      Longitude  Latitude       Date Enterococci..cfu.100ml.
## 1     151.2675 -33.91449 02/01/2013                      19
## 2     151.2675 -33.91449 06/01/2013                       3
## 3     151.2675 -33.91449 12/01/2013                       2
## 4     151.2675 -33.91449 18/01/2013                      13
## 5     151.2675 -33.91449 30/01/2013                       8
## 6     151.2675 -33.91449 05/02/2013                       7
## 7     151.2675 -33.91449 11/02/2013                      11
## 8     151.2675 -33.91449 23/02/2013                      97
## 9     151.2675 -33.91449 07/03/2013                       3
## 10    151.2675 -33.91449 25/03/2013                       0
## 11    151.2675 -33.91449 02/04/2013                       6
## 12    151.2675 -33.91449 12/04/2013                       0
## 13    151.2675 -33.91449 18/04/2013                       1
## 14    151.2675 -33.91449 24/04/2013                       8
## 15    151.2675 -33.91449 01/05/2013                       3
## 16    151.2675 -33.91449 20/05/2013                       5
## 17    151.2675 -33.91449 31/05/2013                       0
## 18    151.2675 -33.91449 06/06/2013                       8
## 19    151.2675 -33.91449 12/06/2013                       2
## 20    151.2675 -33.91449 24/06/2013                      35
## 21    151.2675 -33.91449 06/07/2013                       2
## 22    151.2675 -33.91449 18/07/2013                       2
## 23    151.2675 -33.91449 24/07/2013                      57
## 24    151.2675 -33.91449 08/08/2013                      39
## 25    151.2675 -33.91449 22/08/2013                       0
## 26    151.2675 -33.91449 29/08/2013                       0
## 27    151.2675 -33.91449 24/01/2013                       0
## 28    151.2675 -33.91449 17/02/2013                       9
## 29    151.2675 -33.91449 01/03/2013                      20
## 30    151.2675 -33.91449 13/03/2013                       0
## 31    151.2675 -33.91449 19/03/2013                       0
## 32    151.2675 -33.91449 06/04/2013                      28
## 33    151.2675 -33.91449 07/05/2013                       0
## 34    151.2675 -33.91449 14/05/2013                       3
## 35    151.2675 -33.91449 25/05/2013                       9
## 36    151.2675 -33.91449 17/06/2013                      15
## 37    151.2675 -33.91449 30/06/2013                      50
## 38    151.2675 -33.91449 12/07/2013                       1
## 39    151.2675 -33.91449 30/07/2013                       1
## 40    151.2675 -33.91449 14/08/2013                       0
## 41    151.2675 -33.91449 16/08/2013                       0
## 42    151.2675 -33.91449 02/09/2013                       0
## 43    151.2675 -33.91449 28/09/2013                       0
## 44    151.2675 -33.91449 04/10/2013                       0
## 45    151.2675 -33.91449 12/10/2013                       1
## 46    151.2675 -33.91449 28/10/2013                       1
## 47    151.2675 -33.91449 05/11/2013                       6
## 48    151.2675 -33.91449 29/11/2013                      34
## 49    151.2675 -33.91449 07/12/2013                       5
## 50    151.2675 -33.91449 10/09/2013                       0
## 51    151.2675 -33.91449 16/09/2013                       1
## 52    151.2675 -33.91449 22/09/2013                       3
## 53    151.2675 -33.91449 20/10/2013                       3
## 54    151.2675 -33.91449 13/11/2013                       2
## 55    151.2675 -33.91449 21/11/2013                       1
## 56    151.2675 -33.91449 23/12/2013                       1
## 57    151.2675 -33.91449 13/12/2013                       1
## 58    151.2675 -33.91449 31/12/2013                      12
## 59    151.2582 -33.92076 31/12/2013                      11
## 60    151.2582 -33.92076 13/12/2013                       0
## 61    151.2582 -33.92076 23/12/2013                       4
## 62    151.2582 -33.92076 21/11/2013                      30
## 63    151.2582 -33.92076 13/11/2013                       8
## 64    151.2582 -33.92076 20/10/2013                       0
## 65    151.2582 -33.92076 04/10/2013                      18
## 66    151.2582 -33.92076 16/09/2013                     290
## 67    151.2582 -33.92076 07/12/2013                       3
## 68    151.2582 -33.92076 29/11/2013                       5
## 69    151.2582 -33.92076 05/11/2013                       2
## 70    151.2582 -33.92076 28/10/2013                      94
## 71    151.2582 -33.92076 12/10/2013                       3
## 72    151.2582 -33.92076 28/09/2013                       2
## 73    151.2582 -33.92076 22/09/2013                       4
## 74    151.2582 -33.92076 02/09/2013                       0
## 75    151.2582 -33.92076 10/09/2013                      26
## 76    151.2582 -33.92076 16/08/2013                       0
## 77    151.2582 -33.92076 14/08/2013                       0
## 78    151.2582 -33.92076 22/08/2013                       2
## 79    151.2582 -33.92076 08/08/2013                      34
## 80    151.2582 -33.92076 12/07/2013                       2
## 81    151.2582 -33.92076 24/07/2013                      20
## 82    151.2582 -33.92076 30/06/2013                     270
## 83    151.2582 -33.92076 17/06/2013                      35
## 84    151.2582 -33.92076 25/05/2013                      17
## 85    151.2582 -33.92076 31/05/2013                       6
## 86    151.2582 -33.92076 07/05/2013                       2
## 87    151.2582 -33.92076 01/05/2013                       7
## 88    151.2582 -33.92076 24/04/2013                      10
## 89    151.2582 -33.92076 18/04/2013                      15
## 90    151.2582 -33.92076 12/04/2013                      16
## 91    151.2582 -33.92076 25/03/2013                      82
## 92    151.2582 -33.92076 02/04/2013                       7
## 93    151.2582 -33.92076 19/03/2013                       2
## 94    151.2582 -33.92076 13/03/2013                       4
## 95    151.2582 -33.92076 01/03/2013                     110
## 96    151.2582 -33.92076 07/03/2013                      11
## 97    151.2582 -33.92076 17/02/2013                      30
## 98    151.2582 -33.92076 23/02/2013                     630
## 99    151.2582 -33.92076 30/01/2013                      22
## 100   151.2582 -33.92076 05/02/2013                       2
## 101   151.2582 -33.92076 24/01/2013                      48
## 102   151.2582 -33.92076 12/01/2013                      17
## 103   151.2582 -33.92076 29/08/2013                       1
## 104   151.2582 -33.92076 30/07/2013                       1
## 105   151.2582 -33.92076 18/07/2013                       9
## 106   151.2582 -33.92076 06/07/2013                       5
## 107   151.2582 -33.92076 24/06/2013                      84
## 108   151.2582 -33.92076 12/06/2013                      84
## 109   151.2582 -33.92076 06/06/2013                       8
## 110   151.2582 -33.92076 20/05/2013                       2
## 111   151.2582 -33.92076 14/05/2013                      10
## 112   151.2582 -33.92076 06/04/2013                      49
## 113   151.2582 -33.92076 11/02/2013                     110
## 114   151.2582 -33.92076 18/01/2013                      18
## 115   151.2582 -33.92076 06/01/2013                       4
## 116   151.2582 -33.92076 02/01/2013                      15
## 117   151.2646 -33.91565 19/03/2013                      56
## 118   151.2646 -33.91565 25/03/2013                       4
## 119   151.2646 -33.91565 18/04/2013                       1
## 120   151.2646 -33.91565 20/05/2013                       1
## 121   151.2646 -33.91565 06/06/2013                       0
## 122   151.2646 -33.91565 12/06/2013                     660
## 123   151.2646 -33.91565 31/05/2013                       2
## 124   151.2646 -33.91565 24/06/2013                      41
## 125   151.2646 -33.91565 18/07/2013                       4
## 126   151.2646 -33.91565 24/07/2013                      43
## 127   151.2646 -33.91565 22/08/2013                       4
## 128   151.2646 -33.91565 29/08/2013                       1
## 129   151.2646 -33.91565 08/08/2013                      13
## 130   151.2646 -33.91565 06/04/2013                      27
## 131   151.2646 -33.91565 02/04/2013                       1
## 132   151.2646 -33.91565 12/04/2013                       0
## 133   151.2646 -33.91565 24/04/2013                      13
## 134   151.2646 -33.91565 01/05/2013                       0
## 135   151.2646 -33.91565 07/05/2013                       0
## 136   151.2646 -33.91565 14/05/2013                       5
## 137   151.2646 -33.91565 25/05/2013                       8
## 138   151.2646 -33.91565 30/06/2013                      42
## 139   151.2646 -33.91565 06/07/2013                       2
## 140   151.2646 -33.91565 12/07/2013                       8
## 141   151.2646 -33.91565 30/07/2013                       0
## 142   151.2646 -33.91565 14/08/2013                       0
## 143   151.2646 -33.91565 16/08/2013                       0
## 144   151.2646 -33.91565 02/09/2013                       0
## 145   151.2646 -33.91565 16/09/2013                       5
## 146   151.2646 -33.91565 04/10/2013                       0
## 147   151.2646 -33.91565 28/09/2013                       0
## 148   151.2646 -33.91565 12/10/2013                       0
## 149   151.2646 -33.91565 28/10/2013                       3
## 150   151.2646 -33.91565 21/11/2013                      12
## 151   151.2646 -33.91565 05/11/2013                       8
## 152   151.2646 -33.91565 13/11/2013                       2
## 153   151.2646 -33.91565 29/11/2013                      46
## 154   151.2646 -33.91565 13/12/2013                       0
## 155   151.2646 -33.91565 10/09/2013                       1
## 156   151.2646 -33.91565 22/09/2013                       5
## 157   151.2646 -33.91565 20/10/2013                       3
## 158   151.2646 -33.91565 23/12/2013                       0
## 159   151.2646 -33.91565 31/12/2013                      68
## 160   151.2646 -33.91565 07/12/2013                       1
## 161   151.2515 -33.98012 31/12/2013                     420
## 162   151.2515 -33.98012 23/12/2013                       3
## 163   151.2515 -33.98012 07/12/2013                       9
## 164   151.2515 -33.98012 20/10/2013                       3
## 165   151.2515 -33.98012 13/12/2013                      25
## 166   151.2515 -33.98012 22/09/2013                       8
## 167   151.2515 -33.98012 29/11/2013                       9
## 168   151.2515 -33.98012 10/09/2013                       2
## 169   151.2515 -33.98012 02/09/2013                       1
## 170   151.2515 -33.98012 13/11/2013                       8
## 171   151.2515 -33.98012 05/11/2013                      34
## 172   151.2515 -33.98012 21/11/2013                      26
## 173   151.2515 -33.98012 28/10/2013                      33
## 174   151.2515 -33.98012 12/10/2013                       2
## 175   151.2515 -33.98012 04/10/2013                      11
## 176   151.2515 -33.98012 28/09/2013                       5
## 177   151.2515 -33.98012 16/09/2013                       1
## 178   151.2515 -33.98012 29/08/2013                       0
## 179   151.2515 -33.98012 30/07/2013                       0
## 180   151.2515 -33.98012 18/07/2013                       2
## 181   151.2515 -33.98012 06/07/2013                       0
## 182   151.2515 -33.98012 12/06/2013                       1
## 183   151.2515 -33.98012 24/06/2013                      59
## 184   151.2515 -33.98012 06/06/2013                       6
## 185   151.2515 -33.98012 20/05/2013                       0
## 186   151.2515 -33.98012 01/05/2013                       4
## 187   151.2515 -33.98012 14/05/2013                       4
## 188   151.2515 -33.98012 07/05/2013                       0
## 189   151.2515 -33.98012 24/04/2013                       4
## 190   151.2515 -33.98012 06/04/2013                      10
## 191   151.2515 -33.98012 19/03/2013                       0
## 192   151.2515 -33.98012 17/02/2013                     160
## 193   151.2515 -33.98012 01/03/2013                      56
## 194   151.2515 -33.98012 13/03/2013                       5
## 195   151.2515 -33.98012 24/01/2013                      45
## 196   151.2515 -33.98012 08/08/2013                       7
## 197   151.2515 -33.98012 14/08/2013                       1
## 198   151.2515 -33.98012 16/08/2013                       0
## 199   151.2515 -33.98012 22/08/2013                      27
## 200   151.2515 -33.98012 24/07/2013                       0
## 201   151.2515 -33.98012 12/07/2013                       9
## 202   151.2515 -33.98012 17/06/2013                       1
## 203   151.2515 -33.98012 30/06/2013                    4900
## 204   151.2515 -33.98012 31/05/2013                       2
## 205   151.2515 -33.98012 25/05/2013                       9
## 206   151.2515 -33.98012 18/04/2013                       0
## 207   151.2515 -33.98012 12/04/2013                      20
## 208   151.2515 -33.98012 25/03/2013                     420
## 209   151.2515 -33.98012 02/04/2013                      50
## 210   151.2515 -33.98012 07/03/2013                      31
## 211   151.2515 -33.98012 23/02/2013                     330
## 212   151.2515 -33.98012 11/02/2013                     150
## 213   151.2515 -33.98012 02/01/2013                       9
## 214   151.2515 -33.98012 06/01/2013                       3
## 215   151.2515 -33.98012 18/01/2013                       1
## 216   151.2515 -33.98012 12/01/2013                      72
## 217   151.2515 -33.98012 30/01/2013                      44
## 218   151.2515 -33.98012 05/02/2013                       7
## 219   151.2522 -33.96436 05/02/2013                      13
## 220   151.2522 -33.96436 30/01/2013                      13
## 221   151.2522 -33.96436 12/01/2013                     390
## 222   151.2522 -33.96436 18/01/2013                      15
## 223   151.2522 -33.96436 02/01/2013                       2
## 224   151.2522 -33.96436 17/02/2013                      23
## 225   151.2522 -33.96436 23/02/2013                     390
## 226   151.2522 -33.96436 07/03/2013                       6
## 227   151.2522 -33.96436 25/03/2013                      28
## 228   151.2522 -33.96436 02/04/2013                      12
## 229   151.2522 -33.96436 12/04/2013                       8
## 230   151.2522 -33.96436 18/04/2013                       3
## 231   151.2522 -33.96436 24/04/2013                       6
## 232   151.2522 -33.96436 14/05/2013                      40
## 233   151.2522 -33.96436 25/05/2013                      50
## 234   151.2522 -33.96436 01/05/2013                      32
## 235   151.2522 -33.96436 30/06/2013                    2500
## 236   151.2522 -33.96436 17/06/2013                      40
## 237   151.2522 -33.96436 12/07/2013                       2
## 238   151.2522 -33.96436 30/07/2013                      11
## 239   151.2522 -33.96436 16/08/2013                       1
## 240   151.2522 -33.96436 14/08/2013                       5
## 241   151.2522 -33.96436 24/01/2013                     110
## 242   151.2522 -33.96436 06/01/2013                       4
## 243   151.2522 -33.96436 19/03/2013                       4
## 244   151.2522 -33.96436 13/03/2013                       9
## 245   151.2522 -33.96436 11/02/2013                     140
## 246   151.2522 -33.96436 01/03/2013                      24
## 247   151.2522 -33.96436 06/04/2013                      52
## 248   151.2522 -33.96436 07/05/2013                       5
## 249   151.2522 -33.96436 06/06/2013                       3
## 250   151.2522 -33.96436 31/05/2013                       4
## 251   151.2522 -33.96436 20/05/2013                       5
## 252   151.2522 -33.96436 24/06/2013                      20
## 253   151.2522 -33.96436 12/06/2013                       9
## 254   151.2522 -33.96436 06/07/2013                       0
## 255   151.2522 -33.96436 24/07/2013                     170
## 256   151.2522 -33.96436 18/07/2013                       9
## 257   151.2522 -33.96436 08/08/2013                      54
## 258   151.2522 -33.96436 22/08/2013                       1
## 259   151.2522 -33.96436 29/08/2013                       2
## 260   151.2522 -33.96436 10/09/2013                      10
## 261   151.2522 -33.96436 16/09/2013                       6
## 262   151.2522 -33.96436 04/10/2013                       6
## 263   151.2522 -33.96436 28/10/2013                      50
## 264   151.2522 -33.96436 21/11/2013                       5
## 265   151.2522 -33.96436 13/11/2013                       7
## 266   151.2522 -33.96436 13/12/2013                      13
## 267   151.2522 -33.96436 02/09/2013                       1
## 268   151.2522 -33.96436 28/09/2013                       5
## 269   151.2522 -33.96436 22/09/2013                       1
## 270   151.2522 -33.96436 05/11/2013                      26
## 271   151.2522 -33.96436 20/10/2013                      10
## 272   151.2522 -33.96436 12/10/2013                       4
## 273   151.2522 -33.96436 23/12/2013                      10
## 274   151.2522 -33.96436 07/12/2013                       9
## 275   151.2522 -33.96436 29/11/2013                       4
## 276   151.2522 -33.96436 31/12/2013                    1500
## 277   151.2572 -33.94879 21/11/2013                       3
## 278   151.2572 -33.94879 31/12/2013                    2100
## 279   151.2572 -33.94879 13/12/2013                       0
## 280   151.2572 -33.94879 04/10/2013                       0
## 281   151.2572 -33.94879 28/10/2013                      36
## 282   151.2572 -33.94879 23/12/2013                       0
## 283   151.2572 -33.94879 13/11/2013                       0
## 284   151.2572 -33.94879 16/09/2013                     130
## 285   151.2572 -33.94879 07/12/2013                       1
## 286   151.2572 -33.94879 29/11/2013                      11
## 287   151.2572 -33.94879 05/11/2013                       3
## 288   151.2572 -33.94879 12/10/2013                       2
## 289   151.2572 -33.94879 20/10/2013                       0
## 290   151.2572 -33.94879 28/09/2013                       1
## 291   151.2572 -33.94879 22/09/2013                       7
## 292   151.2572 -33.94879 10/09/2013                       4
## 293   151.2572 -33.94879 02/09/2013                       0
## 294   151.2572 -33.94879 22/08/2013                       0
## 295   151.2572 -33.94879 16/08/2013                       0
## 296   151.2572 -33.94879 08/08/2013                      10
## 297   151.2572 -33.94879 24/07/2013                       3
## 298   151.2572 -33.94879 18/07/2013                       5
## 299   151.2572 -33.94879 12/07/2013                       1
## 300   151.2572 -33.94879 24/06/2013                      16
## 301   151.2572 -33.94879 31/05/2013                      23
## 302   151.2572 -33.94879 17/06/2013                      37
## 303   151.2572 -33.94879 18/04/2013                       8
## 304   151.2572 -33.94879 24/04/2013                       0
## 305   151.2572 -33.94879 01/05/2013                       3
## 306   151.2572 -33.94879 12/04/2013                       3
## 307   151.2572 -33.94879 02/04/2013                      16
## 308   151.2572 -33.94879 25/03/2013                      33
## 309   151.2572 -33.94879 07/03/2013                       1
## 310   151.2572 -33.94879 12/01/2013                      20
## 311   151.2572 -33.94879 18/01/2013                       2
## 312   151.2572 -33.94879 05/02/2013                       0
## 313   151.2572 -33.94879 30/01/2013                      11
## 314   151.2572 -33.94879 23/02/2013                      60
## 315   151.2572 -33.94879 17/02/2013                       6
## 316   151.2572 -33.94879 11/02/2013                       4
## 317   151.2572 -33.94879 14/08/2013                       0
## 318   151.2572 -33.94879 29/08/2013                       0
## 319   151.2572 -33.94879 02/01/2013                       1
## 320   151.2572 -33.94879 30/07/2013                       0
## 321   151.2572 -33.94879 30/06/2013                      64
## 322   151.2572 -33.94879 06/07/2013                       6
## 323   151.2572 -33.94879 14/05/2013                       9
## 324   151.2572 -33.94879 07/05/2013                       1
## 325   151.2572 -33.94879 25/05/2013                      16
## 326   151.2572 -33.94879 20/05/2013                       2
## 327   151.2572 -33.94879 06/06/2013                       6
## 328   151.2572 -33.94879 12/06/2013                       3
## 329   151.2572 -33.94879 06/04/2013                      46
## 330   151.2572 -33.94879 19/03/2013                       0
## 331   151.2572 -33.94879 13/03/2013                       4
## 332   151.2572 -33.94879 01/03/2013                      10
## 333   151.2572 -33.94879 06/01/2013                       1
## 334   151.2572 -33.94879 24/01/2013                       5
## 335   151.2572 -33.95161 24/01/2013                      28
## 336   151.2572 -33.95161 01/03/2013                     450
## 337   151.2572 -33.95161 17/02/2013                       1
## 338   151.2572 -33.95161 13/03/2013                       2
## 339   151.2572 -33.95161 19/03/2013                      21
## 340   151.2572 -33.95161 06/04/2013                      16
## 341   151.2572 -33.95161 01/05/2013                       0
## 342   151.2572 -33.95161 24/04/2013                       6
## 343   151.2572 -33.95161 25/05/2013                      16
## 344   151.2572 -33.95161 07/05/2013                       0
## 345   151.2572 -33.95161 14/05/2013                       3
## 346   151.2572 -33.95161 06/07/2013                       3
## 347   151.2572 -33.95161 30/06/2013                      66
## 348   151.2572 -33.95161 17/06/2013                      47
## 349   151.2572 -33.95161 30/07/2013                       2
## 350   151.2572 -33.95161 12/07/2013                       1
## 351   151.2572 -33.95161 02/01/2013                       1
## 352   151.2572 -33.95161 02/09/2013                       2
## 353   151.2572 -33.95161 14/08/2013                       0
## 354   151.2572 -33.95161 16/08/2013                       0
## 355   151.2572 -33.95161 11/02/2013                      30
## 356   151.2572 -33.95161 23/02/2013                      92
## 357   151.2572 -33.95161 30/01/2013                      13
## 358   151.2572 -33.95161 05/02/2013                       0
## 359   151.2572 -33.95161 18/01/2013                       2
## 360   151.2572 -33.95161 12/01/2013                      33
## 361   151.2572 -33.95161 06/01/2013                       0
## 362   151.2572 -33.95161 07/03/2013                      13
## 363   151.2572 -33.95161 25/03/2013                      17
## 364   151.2572 -33.95161 02/04/2013                       0
## 365   151.2572 -33.95161 12/04/2013                       2
## 366   151.2572 -33.95161 18/04/2013                       8
## 367   151.2572 -33.95161 20/05/2013                       2
## 368   151.2572 -33.95161 31/05/2013                       2
## 369   151.2572 -33.95161 06/06/2013                       0
## 370   151.2572 -33.95161 24/06/2013                      27
## 371   151.2572 -33.95161 12/06/2013                       0
## 372   151.2572 -33.95161 18/07/2013                       3
## 373   151.2572 -33.95161 24/07/2013                       1
## 374   151.2572 -33.95161 08/08/2013                       5
## 375   151.2572 -33.95161 22/08/2013                       1
## 376   151.2572 -33.95161 29/08/2013                       0
## 377   151.2572 -33.95161 10/09/2013                       1
## 378   151.2572 -33.95161 22/09/2013                       4
## 379   151.2572 -33.95161 20/10/2013                       1
## 380   151.2572 -33.95161 07/12/2013                       0
## 381   151.2572 -33.95161 16/09/2013                       2
## 382   151.2572 -33.95161 28/09/2013                       3
## 383   151.2572 -33.95161 13/11/2013                       0
## 384   151.2572 -33.95161 05/11/2013                       0
## 385   151.2572 -33.95161 23/12/2013                       3
## 386   151.2572 -33.95161 28/10/2013                     120
## 387   151.2572 -33.95161 04/10/2013                       1
## 388   151.2572 -33.95161 12/10/2013                       0
## 389   151.2572 -33.95161 13/12/2013                       6
## 390   151.2572 -33.95161 21/11/2013                      20
## 391   151.2572 -33.95161 31/12/2013                    1200
## 392   151.2572 -33.95161 29/11/2013                       5
## 393   151.2582 -33.95354 29/11/2013                      90
## 394   151.2582 -33.95354 07/12/2013                      79
## 395   151.2582 -33.95354 31/12/2013                     630
## 396   151.2582 -33.95354 23/12/2013                       3
## 397   151.2582 -33.95354 12/10/2013                       7
## 398   151.2582 -33.95354 28/10/2013                     210
## 399   151.2582 -33.95354 05/11/2013                      25
## 400   151.2582 -33.95354 28/09/2013                       3
## 401   151.2582 -33.95354 13/12/2013                       4
## 402   151.2582 -33.95354 20/10/2013                      12
## 403   151.2582 -33.95354 21/11/2013                       2
## 404   151.2582 -33.95354 13/11/2013                       3
## 405   151.2582 -33.95354 22/09/2013                       1
## 406   151.2582 -33.95354 04/10/2013                       1
## 407   151.2582 -33.95354 16/09/2013                       8
## 408   151.2582 -33.95354 18/04/2013                      13
## 409   151.2582 -33.95354 25/03/2013                      37
## 410   151.2582 -33.95354 07/03/2013                      69
## 411   151.2582 -33.95354 06/01/2013                       2
## 412   151.2582 -33.95354 12/01/2013                     110
## 413   151.2582 -33.95354 18/01/2013                      13
## 414   151.2582 -33.95354 30/01/2013                     100
## 415   151.2582 -33.95354 11/02/2013                      79
## 416   151.2582 -33.95354 02/01/2013                      12
## 417   151.2582 -33.95354 24/04/2013                      16
## 418   151.2582 -33.95354 01/05/2013                      10
## 419   151.2582 -33.95354 06/04/2013                      69
## 420   151.2582 -33.95354 12/04/2013                      18
## 421   151.2582 -33.95354 02/04/2013                      38
## 422   151.2582 -33.95354 19/03/2013                      16
## 423   151.2582 -33.95354 13/03/2013                       5
## 424   151.2582 -33.95354 17/02/2013                     480
## 425   151.2582 -33.95354 01/03/2013                      22
## 426   151.2582 -33.95354 23/02/2013                     570
## 427   151.2582 -33.95354 24/01/2013                      83
## 428   151.2582 -33.95354 05/02/2013                     630
## 429   151.2776 -33.89151 05/02/2013                       5
## 430   151.2776 -33.89151 30/01/2013                       6
## 431   151.2776 -33.89151 24/01/2013                       9
## 432   151.2776 -33.89151 23/02/2013                      67
## 433   151.2776 -33.89151 17/02/2013                      14
## 434   151.2776 -33.89151 19/03/2013                       6
## 435   151.2776 -33.89151 13/03/2013                       0
## 436   151.2776 -33.89151 01/03/2013                     360
## 437   151.2776 -33.89151 06/04/2013                      69
## 438   151.2776 -33.89151 12/04/2013                       1
## 439   151.2776 -33.89151 01/05/2013                       2
## 440   151.2776 -33.89151 24/04/2013                       0
## 441   151.2776 -33.89151 14/05/2013                       3
## 442   151.2776 -33.89151 07/05/2013                       2
## 443   151.2776 -33.89151 25/05/2013                      19
## 444   151.2776 -33.89151 17/06/2013                      10
## 445   151.2776 -33.89151 31/05/2013                       1
## 446   151.2776 -33.89151 06/01/2013                       1
## 447   151.2776 -33.89151 02/01/2013                       3
## 448   151.2776 -33.89151 02/09/2013                       0
## 449   151.2776 -33.89151 22/08/2013                       2
## 450   151.2776 -33.89151 16/08/2013                       0
## 451   151.2776 -33.89151 14/08/2013                       0
## 452   151.2776 -33.89151 30/07/2013                       0
## 453   151.2776 -33.89151 30/06/2013                     300
## 454   151.2776 -33.89151 12/07/2013                       0
## 455   151.2776 -33.89151 11/02/2013                     600
## 456   151.2776 -33.89151 18/01/2013                       1
## 457   151.2776 -33.89151 12/01/2013                       2
## 458   151.2776 -33.89151 07/03/2013                       1
## 459   151.2776 -33.89151 02/04/2013                       1
## 460   151.2776 -33.89151 18/04/2013                       7
## 461   151.2776 -33.89151 25/03/2013                       0
## 462   151.2776 -33.89151 20/05/2013                       1
## 463   151.2776 -33.89151 06/07/2013                      26
## 464   151.2776 -33.89151 06/06/2013                       0
## 465   151.2776 -33.89151 24/06/2013                       9
## 466   151.2776 -33.89151 12/06/2013                      79
## 467   151.2776 -33.89151 16/09/2013                      32
## 468   151.2776 -33.89151 10/09/2013                       0
## 469   151.2776 -33.89151 22/09/2013                       4
## 470   151.2776 -33.89151 29/08/2013                       0
## 471   151.2776 -33.89151 08/08/2013                      16
## 472   151.2776 -33.89151 24/07/2013                     120
## 473   151.2776 -33.89151 18/07/2013                       5
## 474   151.2776 -33.89151 21/11/2013                       5
## 475   151.2776 -33.89151 13/11/2013                       3
## 476   151.2776 -33.89151 20/10/2013                       1
## 477   151.2776 -33.89151 13/12/2013                       0
## 478   151.2776 -33.89151 04/10/2013                       0
## 479   151.2776 -33.89151 28/09/2013                       2
## 480   151.2776 -33.89151 28/10/2013                       5
## 481   151.2776 -33.89151 31/12/2013                      32
## 482   151.2776 -33.89151 05/11/2013                      27
## 483   151.2776 -33.89151 12/10/2013                       0
## 484   151.2776 -33.89151 23/12/2013                       9
## 485   151.2776 -33.89151 29/11/2013                       1
## 486   151.2776 -33.89151 07/12/2013                       0
## 487   151.2686 -33.90307 07/12/2013                       2
## 488   151.2686 -33.90307 31/12/2013                      16
## 489   151.2686 -33.90307 29/11/2013                       2
## 490   151.2686 -33.90307 23/12/2013                      13
## 491   151.2686 -33.90307 20/10/2013                       3
## 492   151.2686 -33.90307 12/10/2013                       1
## 493   151.2686 -33.90307 05/11/2013                      45
## 494   151.2686 -33.90307 28/09/2013                       2
## 495   151.2686 -33.90307 22/09/2013                      13
## 496   151.2686 -33.90307 13/12/2013                       1
## 497   151.2686 -33.90307 10/09/2013                       0
## 498   151.2686 -33.90307 28/10/2013                      33
## 499   151.2686 -33.90307 13/11/2013                       5
## 500   151.2686 -33.90307 21/11/2013                      34
## 501   151.2686 -33.90307 30/07/2013                       6
## 502   151.2686 -33.90307 14/08/2013                       0
## 503   151.2686 -33.90307 04/10/2013                       0
## 504   151.2686 -33.90307 29/08/2013                       0
## 505   151.2686 -33.90307 16/09/2013                       0
## 506   151.2686 -33.90307 12/06/2013                      81
## 507   151.2686 -33.90307 30/06/2013                      50
## 508   151.2686 -33.90307 06/07/2013                       4
## 509   151.2686 -33.90307 20/05/2013                       2
## 510   151.2686 -33.90307 14/05/2013                      13
## 511   151.2686 -33.90307 25/05/2013                      18
## 512   151.2686 -33.90307 06/04/2013                      60
## 513   151.2686 -33.90307 19/03/2013                       5
## 514   151.2686 -33.90307 13/03/2013                       6
## 515   151.2686 -33.90307 24/01/2013                       6
## 516   151.2686 -33.90307 06/01/2013                       2
## 517   151.2686 -33.90307 01/03/2013                      32
## 518   151.2686 -33.90307 17/06/2013                      12
## 519   151.2686 -33.90307 24/06/2013                      19
## 520   151.2686 -33.90307 24/07/2013                      24
## 521   151.2686 -33.90307 12/07/2013                       0
## 522   151.2686 -33.90307 18/07/2013                       3
## 523   151.2686 -33.90307 08/08/2013                      64
## 524   151.2686 -33.90307 16/08/2013                       1
## 525   151.2686 -33.90307 22/08/2013                       0
## 526   151.2686 -33.90307 02/09/2013                       0
## 527   151.2686 -33.90307 06/06/2013                       8
## 528   151.2686 -33.90307 31/05/2013                       3
## 529   151.2686 -33.90307 01/05/2013                       4
## 530   151.2686 -33.90307 07/05/2013                       0
## 531   151.2686 -33.90307 12/04/2013                       5
## 532   151.2686 -33.90307 18/04/2013                      34
## 533   151.2686 -33.90307 24/04/2013                       1
## 534   151.2686 -33.90307 02/04/2013                       3
## 535   151.2686 -33.90307 07/03/2013                       8
## 536   151.2686 -33.90307 25/03/2013                       2
## 537   151.2686 -33.90307 17/02/2013                      16
## 538   151.2686 -33.90307 23/02/2013                     780
## 539   151.2686 -33.90307 18/01/2013                       3
## 540   151.2686 -33.90307 02/01/2013                       4
## 541   151.2686 -33.90307 12/01/2013                      38
## 542   151.2686 -33.90307 30/01/2013                      25
## 543   151.2686 -33.90307 05/02/2013                       2
## 544   151.2686 -33.90307 11/02/2013                      38
## 545   151.2706 -33.90056 05/02/2013                       3
## 546   151.2706 -33.90056 30/01/2013                      23
## 547   151.2706 -33.90056 12/01/2013                       7
## 548   151.2706 -33.90056 24/01/2013                       5
## 549   151.2706 -33.90056 07/03/2013                       3
## 550   151.2706 -33.90056 17/02/2013                      11
## 551   151.2706 -33.90056 23/02/2013                      90
## 552   151.2706 -33.90056 19/03/2013                       2
## 553   151.2706 -33.90056 01/03/2013                     270
## 554   151.2706 -33.90056 13/03/2013                       0
## 555   151.2706 -33.90056 02/04/2013                       2
## 556   151.2706 -33.90056 12/04/2013                       1
## 557   151.2706 -33.90056 06/04/2013                      54
## 558   151.2706 -33.90056 01/05/2013                       2
## 559   151.2706 -33.90056 18/04/2013                       3
## 560   151.2706 -33.90056 24/04/2013                       3
## 561   151.2706 -33.90056 07/05/2013                       2
## 562   151.2706 -33.90056 25/05/2013                       9
## 563   151.2706 -33.90056 31/05/2013                       0
## 564   151.2706 -33.90056 17/06/2013                      21
## 565   151.2706 -33.90056 02/01/2013                       1
## 566   151.2706 -33.90056 06/01/2013                       0
## 567   151.2706 -33.90056 02/09/2013                       0
## 568   151.2706 -33.90056 16/08/2013                       0
## 569   151.2706 -33.90056 22/08/2013                       2
## 570   151.2706 -33.90056 14/08/2013                       2
## 571   151.2706 -33.90056 24/07/2013                      32
## 572   151.2706 -33.90056 08/08/2013                      61
## 573   151.2706 -33.90056 12/07/2013                       1
## 574   151.2706 -33.90056 11/02/2013                      13
## 575   151.2706 -33.90056 18/01/2013                      22
## 576   151.2706 -33.90056 25/03/2013                       4
## 577   151.2706 -33.90056 20/05/2013                       1
## 578   151.2706 -33.90056 14/05/2013                       2
## 579   151.2706 -33.90056 06/07/2013                       5
## 580   151.2706 -33.90056 30/06/2013                     210
## 581   151.2706 -33.90056 12/06/2013                     690
## 582   151.2706 -33.90056 24/06/2013                      15
## 583   151.2706 -33.90056 06/06/2013                       2
## 584   151.2706 -33.90056 16/09/2013                      39
## 585   151.2706 -33.90056 04/10/2013                       2
## 586   151.2706 -33.90056 29/08/2013                       0
## 587   151.2706 -33.90056 30/07/2013                       3
## 588   151.2706 -33.90056 18/07/2013                       0
## 589   151.2706 -33.90056 13/11/2013                       6
## 590   151.2706 -33.90056 21/11/2013                      35
## 591   151.2706 -33.90056 20/10/2013                       1
## 592   151.2706 -33.90056 10/09/2013                       0
## 593   151.2706 -33.90056 13/12/2013                       2
## 594   151.2706 -33.90056 22/09/2013                       2
## 595   151.2706 -33.90056 28/09/2013                       0
## 596   151.2706 -33.90056 31/12/2013                      29
## 597   151.2706 -33.90056 28/10/2013                      14
## 598   151.2706 -33.90056 05/11/2013                       4
## 599   151.2706 -33.90056 12/10/2013                       0
## 600   151.2706 -33.90056 23/12/2013                       8
## 601   151.2706 -33.90056 29/11/2013                       1
## 602   151.2706 -33.90056 07/12/2013                       2
## 603   151.2675 -33.91449 08/10/2014                       3
## 604   151.2675 -33.91449 16/10/2014                      11
## 605   151.2675 -33.91449 25/10/2014                       5
## 606   151.2675 -33.91449 02/11/2014                       1
## 607   151.2675 -33.91449 10/11/2014                       1
## 608   151.2675 -33.91449 18/11/2014                       0
## 609   151.2675 -33.91449 13/12/2014                      21
## 610   151.2675 -33.91449 19/12/2014                       6
## 611   151.2675 -33.91449 16/01/2014                       3
## 612   151.2675 -33.91449 24/01/2014                       5
## 613   151.2675 -33.91449 09/02/2014                       6
## 614   151.2675 -33.91449 25/02/2014                       5
## 615   151.2675 -33.91449 05/03/2014                       3
## 616   151.2675 -33.91449 06/04/2014                      60
## 617   151.2675 -33.91449 06/05/2014                       1
## 618   151.2675 -33.91449 16/05/2014                       0
## 619   151.2675 -33.91449 22/05/2014                       5
## 620   151.2675 -33.91449 10/06/2014                       9
## 621   151.2675 -33.91449 26/06/2014                       0
## 622   151.2675 -33.91449 08/07/2014                       0
## 623   151.2675 -33.91449 14/07/2014                       1
## 624   151.2675 -33.91449 24/07/2014                       0
## 625   151.2675 -33.91449 05/08/2014                       0
## 626   151.2675 -33.91449 21/08/2014                       2
## 627   151.2675 -33.91449 21/10/2014                       4
## 628   151.2675 -33.91449 26/11/2014                       1
## 629   151.2675 -33.91449 04/12/2014                      53
## 630   151.2675 -33.91449 12/09/2014                       0
## 631   151.2675 -33.91449 18/09/2014                       0
## 632   151.2675 -33.91449 24/09/2014                       0
## 633   151.2675 -33.91449 28/12/2014                     360
## 634   151.2675 -33.91449 08/01/2014                       3
## 635   151.2675 -33.91449 01/02/2014                       8
## 636   151.2675 -33.91449 17/02/2014                      50
## 637   151.2675 -33.91449 13/03/2014                      22
## 638   151.2675 -33.91449 21/03/2014                      12
## 639   151.2675 -33.91449 29/03/2014                       4
## 640   151.2675 -33.91449 22/04/2014                       3
## 641   151.2675 -33.91449 14/04/2014                      14
## 642   151.2675 -33.91449 30/04/2014                      11
## 643   151.2675 -33.91449 12/05/2014                       4
## 644   151.2675 -33.91449 28/05/2014                       2
## 645   151.2675 -33.91449 03/06/2014                       2
## 646   151.2675 -33.91449 19/06/2014                       1
## 647   151.2675 -33.91449 03/07/2014                       0
## 648   151.2675 -33.91449 18/07/2014                       0
## 649   151.2675 -33.91449 01/08/2014                       1
## 650   151.2675 -33.91449 11/08/2014                       0
## 651   151.2675 -33.91449 15/08/2014                       1
## 652   151.2675 -33.91449 27/08/2014                       7
## 653   151.2675 -33.91449 02/09/2014                       0
## 654   151.2675 -33.91449 08/09/2014                       4
## 655   151.2675 -33.91449 30/09/2014                      18
## 656   151.2582 -33.92076 30/09/2014                      12
## 657   151.2582 -33.92076 24/09/2014                       0
## 658   151.2582 -33.92076 08/09/2014                       2
## 659   151.2582 -33.92076 27/08/2014                      72
## 660   151.2582 -33.92076 21/08/2014                      35
## 661   151.2582 -33.92076 15/08/2014                       0
## 662   151.2582 -33.92076 11/08/2014                      39
## 663   151.2582 -33.92076 01/08/2014                       2
## 664   151.2582 -33.92076 05/08/2014                       1
## 665   151.2582 -33.92076 19/06/2014                      20
## 666   151.2582 -33.92076 10/06/2014                     570
## 667   151.2582 -33.92076 28/05/2014                       6
## 668   151.2582 -33.92076 12/05/2014                       5
## 669   151.2582 -33.92076 14/04/2014                      16
## 670   151.2582 -33.92076 22/04/2014                       8
## 671   151.2582 -33.92076 05/03/2014                      19
## 672   151.2582 -33.92076 29/03/2014                      22
## 673   151.2582 -33.92076 21/03/2014                      57
## 674   151.2582 -33.92076 13/03/2014                     110
## 675   151.2582 -33.92076 09/02/2014                       4
## 676   151.2582 -33.92076 16/01/2014                      16
## 677   151.2582 -33.92076 08/01/2014                      22
## 678   151.2582 -33.92076 28/12/2014                     450
## 679   151.2582 -33.92076 18/09/2014                       0
## 680   151.2582 -33.92076 12/09/2014                       4
## 681   151.2582 -33.92076 04/12/2014                      66
## 682   151.2582 -33.92076 26/11/2014                      27
## 683   151.2582 -33.92076 02/11/2014                      30
## 684   151.2582 -33.92076 10/11/2014                       0
## 685   151.2582 -33.92076 18/11/2014                       3
## 686   151.2582 -33.92076 02/09/2014                       0
## 687   151.2582 -33.92076 24/07/2014                       3
## 688   151.2582 -33.92076 14/07/2014                       2
## 689   151.2582 -33.92076 08/07/2014                       0
## 690   151.2582 -33.92076 18/07/2014                       1
## 691   151.2582 -33.92076 26/06/2014                       4
## 692   151.2582 -33.92076 03/07/2014                       1
## 693   151.2582 -33.92076 22/05/2014                      10
## 694   151.2582 -33.92076 16/05/2014                       6
## 695   151.2582 -33.92076 06/05/2014                       7
## 696   151.2582 -33.92076 30/04/2014                      20
## 697   151.2582 -33.92076 06/04/2014                     160
## 698   151.2582 -33.92076 25/02/2014                      40
## 699   151.2582 -33.92076 17/02/2014                     110
## 700   151.2582 -33.92076 24/01/2014                      20
## 701   151.2582 -33.92076 01/02/2014                      29
## 702   151.2582 -33.92076 19/12/2014                      25
## 703   151.2582 -33.92076 13/12/2014                      42
## 704   151.2582 -33.92076 25/10/2014                       4
## 705   151.2582 -33.92076 16/10/2014                       8
## 706   151.2582 -33.92076 21/10/2014                       6
## 707   151.2582 -33.92076 08/10/2014                     620
## 708   151.2646 -33.91565 08/10/2014                      44
## 709   151.2646 -33.91565 16/10/2014                       1
## 710   151.2646 -33.91565 25/10/2014                       3
## 711   151.2646 -33.91565 02/11/2014                       2
## 712   151.2646 -33.91565 10/11/2014                      11
## 713   151.2646 -33.91565 18/11/2014                       0
## 714   151.2646 -33.91565 08/01/2014                       3
## 715   151.2646 -33.91565 16/01/2014                       6
## 716   151.2646 -33.91565 24/01/2014                       0
## 717   151.2646 -33.91565 09/02/2014                       0
## 718   151.2646 -33.91565 25/02/2014                       2
## 719   151.2646 -33.91565 06/04/2014                      35
## 720   151.2646 -33.91565 29/03/2014                      24
## 721   151.2646 -33.91565 05/03/2014                       9
## 722   151.2646 -33.91565 13/03/2014                      23
## 723   151.2646 -33.91565 21/03/2014                      31
## 724   151.2646 -33.91565 22/04/2014                       0
## 725   151.2646 -33.91565 06/05/2014                       0
## 726   151.2646 -33.91565 16/05/2014                       4
## 727   151.2646 -33.91565 19/06/2014                       0
## 728   151.2646 -33.91565 26/06/2014                       0
## 729   151.2646 -33.91565 10/06/2014                      16
## 730   151.2646 -33.91565 22/05/2014                       0
## 731   151.2646 -33.91565 24/07/2014                       0
## 732   151.2646 -33.91565 08/07/2014                       2
## 733   151.2646 -33.91565 14/07/2014                       0
## 734   151.2646 -33.91565 05/08/2014                       0
## 735   151.2646 -33.91565 21/10/2014                       0
## 736   151.2646 -33.91565 21/08/2014                       4
## 737   151.2646 -33.91565 26/11/2014                      32
## 738   151.2646 -33.91565 04/12/2014                      17
## 739   151.2646 -33.91565 13/12/2014                       5
## 740   151.2646 -33.91565 19/12/2014                      30
## 741   151.2646 -33.91565 18/09/2014                       0
## 742   151.2646 -33.91565 24/09/2014                       1
## 743   151.2646 -33.91565 28/12/2014                     450
## 744   151.2646 -33.91565 01/02/2014                       5
## 745   151.2646 -33.91565 17/02/2014                      89
## 746   151.2646 -33.91565 14/04/2014                       4
## 747   151.2646 -33.91565 30/04/2014                       8
## 748   151.2646 -33.91565 12/05/2014                       0
## 749   151.2646 -33.91565 28/05/2014                       5
## 750   151.2646 -33.91565 18/07/2014                       0
## 751   151.2646 -33.91565 01/08/2014                       1
## 752   151.2646 -33.91565 03/06/2014                       0
## 753   151.2646 -33.91565 03/07/2014                       0
## 754   151.2646 -33.91565 11/08/2014                       0
## 755   151.2646 -33.91565 15/08/2014                       1
## 756   151.2646 -33.91565 27/08/2014                      13
## 757   151.2646 -33.91565 02/09/2014                       0
## 758   151.2646 -33.91565 08/09/2014                       2
## 759   151.2646 -33.91565 12/09/2014                       2
## 760   151.2646 -33.91565 30/09/2014                       0
## 761   151.2515 -33.98012 30/09/2014                       0
## 762   151.2515 -33.98012 08/09/2014                       4
## 763   151.2515 -33.98012 12/09/2014                       0
## 764   151.2515 -33.98012 27/08/2014                     120
## 765   151.2515 -33.98012 02/09/2014                       0
## 766   151.2515 -33.98012 15/08/2014                       1
## 767   151.2515 -33.98012 11/08/2014                      12
## 768   151.2515 -33.98012 01/08/2014                       0
## 769   151.2515 -33.98012 03/07/2014                       0
## 770   151.2515 -33.98012 18/07/2014                       0
## 771   151.2515 -33.98012 28/05/2014                       6
## 772   151.2515 -33.98012 03/06/2014                      10
## 773   151.2515 -33.98012 14/04/2014                      24
## 774   151.2515 -33.98012 30/04/2014                      95
## 775   151.2515 -33.98012 01/02/2014                      13
## 776   151.2515 -33.98012 17/02/2014                      46
## 777   151.2515 -33.98012 28/12/2014                      10
## 778   151.2515 -33.98012 24/09/2014                       3
## 779   151.2515 -33.98012 19/12/2014                      21
## 780   151.2515 -33.98012 18/09/2014                       0
## 781   151.2515 -33.98012 04/12/2014                      81
## 782   151.2515 -33.98012 26/11/2014                       2
## 783   151.2515 -33.98012 21/10/2014                      42
## 784   151.2515 -33.98012 05/08/2014                       3
## 785   151.2515 -33.98012 21/08/2014                      11
## 786   151.2515 -33.98012 24/07/2014                       1
## 787   151.2515 -33.98012 08/07/2014                       0
## 788   151.2515 -33.98012 14/07/2014                       2
## 789   151.2515 -33.98012 10/06/2014                      22
## 790   151.2515 -33.98012 19/06/2014                       6
## 791   151.2515 -33.98012 26/06/2014                       4
## 792   151.2515 -33.98012 12/05/2014                       0
## 793   151.2515 -33.98012 16/05/2014                       2
## 794   151.2515 -33.98012 22/05/2014                       3
## 795   151.2515 -33.98012 22/04/2014                      30
## 796   151.2515 -33.98012 06/05/2014                       8
## 797   151.2515 -33.98012 13/03/2014                      36
## 798   151.2515 -33.98012 05/03/2014                       3
## 799   151.2515 -33.98012 29/03/2014                      39
## 800   151.2515 -33.98012 21/03/2014                      60
## 801   151.2515 -33.98012 06/04/2014                       2
## 802   151.2515 -33.98012 09/02/2014                       8
## 803   151.2515 -33.98012 25/02/2014                       7
## 804   151.2515 -33.98012 16/01/2014                       1
## 805   151.2515 -33.98012 24/01/2014                      20
## 806   151.2515 -33.98012 08/01/2014                       5
## 807   151.2515 -33.98012 13/12/2014                      15
## 808   151.2515 -33.98012 18/11/2014                       3
## 809   151.2515 -33.98012 02/11/2014                       1
## 810   151.2515 -33.98012 10/11/2014                     120
## 811   151.2515 -33.98012 25/10/2014                      52
## 812   151.2515 -33.98012 08/10/2014                      51
## 813   151.2515 -33.98012 16/10/2014                      27
## 814   151.2522 -33.96436 16/10/2014                      11
## 815   151.2522 -33.96436 08/10/2014                     160
## 816   151.2522 -33.96436 25/10/2014                     200
## 817   151.2522 -33.96436 02/11/2014                       7
## 818   151.2522 -33.96436 10/11/2014                       0
## 819   151.2522 -33.96436 18/11/2014                      19
## 820   151.2522 -33.96436 26/11/2014                      12
## 821   151.2522 -33.96436 28/12/2014                      10
## 822   151.2522 -33.96436 16/01/2014                      17
## 823   151.2522 -33.96436 08/01/2014                       3
## 824   151.2522 -33.96436 09/02/2014                       2
## 825   151.2522 -33.96436 29/03/2014                     170
## 826   151.2522 -33.96436 06/04/2014                      45
## 827   151.2522 -33.96436 21/03/2014                       4
## 828   151.2522 -33.96436 05/03/2014                      66
## 829   151.2522 -33.96436 13/03/2014                      58
## 830   151.2522 -33.96436 22/04/2014                      16
## 831   151.2522 -33.96436 14/04/2014                      11
## 832   151.2522 -33.96436 22/05/2014                      38
## 833   151.2522 -33.96436 12/05/2014                      60
## 834   151.2522 -33.96436 19/06/2014                       4
## 835   151.2522 -33.96436 10/06/2014                       4
## 836   151.2522 -33.96436 03/06/2014                      12
## 837   151.2522 -33.96436 08/07/2014                       2
## 838   151.2522 -33.96436 14/07/2014                       2
## 839   151.2522 -33.96436 24/07/2014                       4
## 840   151.2522 -33.96436 05/08/2014                      31
## 841   151.2522 -33.96436 21/08/2014                      10
## 842   151.2522 -33.96436 15/08/2014                      12
## 843   151.2522 -33.96436 21/10/2014                       8
## 844   151.2522 -33.96436 04/12/2014                     990
## 845   151.2522 -33.96436 13/12/2014                       7
## 846   151.2522 -33.96436 24/09/2014                       9
## 847   151.2522 -33.96436 30/09/2014                       4
## 848   151.2522 -33.96436 19/12/2014                      17
## 849   151.2522 -33.96436 01/02/2014                      35
## 850   151.2522 -33.96436 24/01/2014                       4
## 851   151.2522 -33.96436 17/02/2014                     140
## 852   151.2522 -33.96436 25/02/2014                       6
## 853   151.2522 -33.96436 30/04/2014                     180
## 854   151.2522 -33.96436 28/05/2014                      50
## 855   151.2522 -33.96436 16/05/2014                      32
## 856   151.2522 -33.96436 06/05/2014                       7
## 857   151.2522 -33.96436 18/07/2014                      25
## 858   151.2522 -33.96436 03/07/2014                      33
## 859   151.2522 -33.96436 26/06/2014                     110
## 860   151.2522 -33.96436 01/08/2014                      14
## 861   151.2522 -33.96436 11/08/2014                     110
## 862   151.2522 -33.96436 27/08/2014                      67
## 863   151.2522 -33.96436 02/09/2014                       2
## 864   151.2522 -33.96436 12/09/2014                       2
## 865   151.2522 -33.96436 18/09/2014                       2
## 866   151.2522 -33.96436 08/09/2014                      44
## 867   151.2572 -33.94879 30/09/2014                       0
## 868   151.2572 -33.94879 24/09/2014                       0
## 869   151.2572 -33.94879 21/08/2014                       9
## 870   151.2572 -33.94879 15/08/2014                       1
## 871   151.2572 -33.94879 05/08/2014                       0
## 872   151.2572 -33.94879 08/07/2014                       3
## 873   151.2572 -33.94879 24/07/2014                       0
## 874   151.2572 -33.94879 14/07/2014                       3
## 875   151.2572 -33.94879 16/05/2014                       3
## 876   151.2572 -33.94879 22/05/2014                       2
## 877   151.2572 -33.94879 12/05/2014                       0
## 878   151.2572 -33.94879 03/06/2014                       2
## 879   151.2572 -33.94879 10/06/2014                       0
## 880   151.2572 -33.94879 19/06/2014                       0
## 881   151.2572 -33.94879 14/04/2014                       1
## 882   151.2572 -33.94879 05/03/2014                       3
## 883   151.2572 -33.94879 22/04/2014                       3
## 884   151.2572 -33.94879 13/03/2014                      16
## 885   151.2572 -33.94879 21/03/2014                       9
## 886   151.2572 -33.94879 29/03/2014                      18
## 887   151.2572 -33.94879 06/04/2014                       4
## 888   151.2572 -33.94879 09/02/2014                       1
## 889   151.2572 -33.94879 16/01/2014                      32
## 890   151.2572 -33.94879 28/12/2014                      13
## 891   151.2572 -33.94879 08/01/2014                       0
## 892   151.2572 -33.94879 18/09/2014                       0
## 893   151.2572 -33.94879 08/09/2014                       1
## 894   151.2572 -33.94879 12/09/2014                       2
## 895   151.2572 -33.94879 26/11/2014                       8
## 896   151.2572 -33.94879 25/10/2014                      15
## 897   151.2572 -33.94879 02/11/2014                       1
## 898   151.2572 -33.94879 18/11/2014                       1
## 899   151.2572 -33.94879 10/11/2014                       3
## 900   151.2572 -33.94879 16/10/2014                       1
## 901   151.2572 -33.94879 02/09/2014                       1
## 902   151.2572 -33.94879 08/10/2014                      87
## 903   151.2572 -33.94879 27/08/2014                      13
## 904   151.2572 -33.94879 11/08/2014                      35
## 905   151.2572 -33.94879 01/08/2014                       2
## 906   151.2572 -33.94879 18/07/2014                       0
## 907   151.2572 -33.94879 28/05/2014                       3
## 908   151.2572 -33.94879 26/06/2014                       1
## 909   151.2572 -33.94879 03/07/2014                       2
## 910   151.2572 -33.94879 06/05/2014                       2
## 911   151.2572 -33.94879 30/04/2014                      46
## 912   151.2572 -33.94879 25/02/2014                      28
## 913   151.2572 -33.94879 17/02/2014                      70
## 914   151.2572 -33.94879 24/01/2014                       5
## 915   151.2572 -33.94879 01/02/2014                       3
## 916   151.2572 -33.94879 19/12/2014                       6
## 917   151.2572 -33.94879 04/12/2014                      27
## 918   151.2572 -33.94879 13/12/2014                       2
## 919   151.2572 -33.94879 21/10/2014                       1
## 920   151.2572 -33.95161 21/10/2014                       0
## 921   151.2572 -33.95161 13/12/2014                       0
## 922   151.2572 -33.95161 26/11/2014                       3
## 923   151.2572 -33.95161 04/12/2014                      34
## 924   151.2572 -33.95161 28/12/2014                       5
## 925   151.2572 -33.95161 19/12/2014                       8
## 926   151.2572 -33.95161 01/02/2014                       3
## 927   151.2572 -33.95161 17/02/2014                      39
## 928   151.2572 -33.95161 14/04/2014                       0
## 929   151.2572 -33.95161 30/04/2014                      43
## 930   151.2572 -33.95161 12/05/2014                       0
## 931   151.2572 -33.95161 03/07/2014                       0
## 932   151.2572 -33.95161 28/05/2014                       2
## 933   151.2572 -33.95161 03/06/2014                       0
## 934   151.2572 -33.95161 18/07/2014                       0
## 935   151.2572 -33.95161 01/08/2014                       2
## 936   151.2572 -33.95161 11/08/2014                       2
## 937   151.2572 -33.95161 27/08/2014                      21
## 938   151.2572 -33.95161 15/08/2014                       1
## 939   151.2572 -33.95161 08/10/2014                      56
## 940   151.2572 -33.95161 02/09/2014                       0
## 941   151.2572 -33.95161 16/10/2014                       2
## 942   151.2572 -33.95161 10/11/2014                      13
## 943   151.2572 -33.95161 18/11/2014                       0
## 944   151.2572 -33.95161 02/11/2014                       2
## 945   151.2572 -33.95161 25/10/2014                       3
## 946   151.2572 -33.95161 12/09/2014                       2
## 947   151.2572 -33.95161 08/09/2014                       0
## 948   151.2572 -33.95161 08/01/2014                       0
## 949   151.2572 -33.95161 30/09/2014                       0
## 950   151.2572 -33.95161 16/01/2014                      23
## 951   151.2572 -33.95161 24/01/2014                       3
## 952   151.2572 -33.95161 09/02/2014                       0
## 953   151.2572 -33.95161 25/02/2014                       0
## 954   151.2572 -33.95161 06/04/2014                       1
## 955   151.2572 -33.95161 29/03/2014                     460
## 956   151.2572 -33.95161 21/03/2014                       1
## 957   151.2572 -33.95161 13/03/2014                      15
## 958   151.2572 -33.95161 22/04/2014                       3
## 959   151.2572 -33.95161 05/03/2014                       5
## 960   151.2572 -33.95161 19/06/2014                       0
## 961   151.2572 -33.95161 10/06/2014                       1
## 962   151.2572 -33.95161 06/05/2014                       0
## 963   151.2572 -33.95161 22/05/2014                       4
## 964   151.2572 -33.95161 16/05/2014                       2
## 965   151.2572 -33.95161 14/07/2014                       0
## 966   151.2572 -33.95161 24/07/2014                       0
## 967   151.2572 -33.95161 08/07/2014                      26
## 968   151.2572 -33.95161 26/06/2014                       2
## 969   151.2572 -33.95161 05/08/2014                       0
## 970   151.2572 -33.95161 21/08/2014                       4
## 971   151.2572 -33.95161 24/09/2014                       0
## 972   151.2572 -33.95161 18/09/2014                       0
## 973   151.2582 -33.95354 18/09/2014                       2
## 974   151.2582 -33.95354 12/09/2014                       3
## 975   151.2582 -33.95354 24/09/2014                       1
## 976   151.2582 -33.95354 21/08/2014                      70
## 977   151.2582 -33.95354 05/08/2014                       0
## 978   151.2582 -33.95354 26/06/2014                       3
## 979   151.2582 -33.95354 03/07/2014                       1
## 980   151.2582 -33.95354 08/07/2014                       0
## 981   151.2582 -33.95354 24/07/2014                      12
## 982   151.2582 -33.95354 14/07/2014                       0
## 983   151.2582 -33.95354 18/07/2014                       0
## 984   151.2582 -33.95354 16/05/2014                       5
## 985   151.2582 -33.95354 22/05/2014                       2
## 986   151.2582 -33.95354 06/05/2014                       7
## 987   151.2582 -33.95354 06/04/2014                     270
## 988   151.2582 -33.95354 25/02/2014                       5
## 989   151.2582 -33.95354 24/01/2014                      16
## 990   151.2582 -33.95354 01/02/2014                       5
## 991   151.2582 -33.95354 30/09/2014                       5
## 992   151.2582 -33.95354 08/09/2014                      34
## 993   151.2582 -33.95354 19/12/2014                       8
## 994   151.2582 -33.95354 25/10/2014                       7
## 995   151.2582 -33.95354 02/11/2014                       8
## 996   151.2582 -33.95354 18/11/2014                       5
## 997   151.2582 -33.95354 10/11/2014                       5
## 998   151.2582 -33.95354 13/12/2014                      14
## 999   151.2582 -33.95354 16/10/2014                      35
## 1000  151.2582 -33.95354 02/09/2014                       1
## 1001  151.2582 -33.95354 08/10/2014                      61
## 1002  151.2582 -33.95354 15/08/2014                       6
## 1003  151.2582 -33.95354 27/08/2014                      68
## 1004  151.2582 -33.95354 11/08/2014                       3
## 1005  151.2582 -33.95354 01/08/2014                       2
## 1006  151.2582 -33.95354 03/06/2014                       2
## 1007  151.2582 -33.95354 28/05/2014                      40
## 1008  151.2582 -33.95354 10/06/2014                       8
## 1009  151.2582 -33.95354 19/06/2014                       1
## 1010  151.2582 -33.95354 12/05/2014                       3
## 1011  151.2582 -33.95354 30/04/2014                      13
## 1012  151.2582 -33.95354 22/04/2014                      52
## 1013  151.2582 -33.95354 14/04/2014                       3
## 1014  151.2582 -33.95354 29/03/2014                      41
## 1015  151.2582 -33.95354 21/03/2014                     160
## 1016  151.2582 -33.95354 13/03/2014                      81
## 1017  151.2582 -33.95354 05/03/2014                      18
## 1018  151.2582 -33.95354 17/02/2014                     190
## 1019  151.2582 -33.95354 09/02/2014                       3
## 1020  151.2582 -33.95354 16/01/2014                      29
## 1021  151.2582 -33.95354 28/12/2014                     780
## 1022  151.2582 -33.95354 04/12/2014                      38
## 1023  151.2582 -33.95354 08/01/2014                       8
## 1024  151.2582 -33.95354 26/11/2014                       8
## 1025  151.2582 -33.95354 21/10/2014                      11
## 1026  151.2776 -33.89151 21/10/2014                       1
## 1027  151.2776 -33.89151 02/11/2014                      10
## 1028  151.2776 -33.89151 04/12/2014                      46
## 1029  151.2776 -33.89151 26/11/2014                      24
## 1030  151.2776 -33.89151 16/01/2014                       3
## 1031  151.2776 -33.89151 08/01/2014                       6
## 1032  151.2776 -33.89151 28/12/2014                      13
## 1033  151.2776 -33.89151 01/02/2014                      15
## 1034  151.2776 -33.89151 17/02/2014                     140
## 1035  151.2776 -33.89151 13/03/2014                      39
## 1036  151.2776 -33.89151 21/03/2014                       7
## 1037  151.2776 -33.89151 29/03/2014                      14
## 1038  151.2776 -33.89151 14/04/2014                      17
## 1039  151.2776 -33.89151 22/04/2014                       2
## 1040  151.2776 -33.89151 30/04/2014                      10
## 1041  151.2776 -33.89151 12/05/2014                       1
## 1042  151.2776 -33.89151 28/05/2014                       7
## 1043  151.2776 -33.89151 19/06/2014                       4
## 1044  151.2776 -33.89151 03/06/2014                       1
## 1045  151.2776 -33.89151 01/08/2014                       2
## 1046  151.2776 -33.89151 15/08/2014                       3
## 1047  151.2776 -33.89151 18/07/2014                       2
## 1048  151.2776 -33.89151 02/09/2014                       0
## 1049  151.2776 -33.89151 27/08/2014                      30
## 1050  151.2776 -33.89151 11/08/2014                       5
## 1051  151.2776 -33.89151 21/08/2014                       3
## 1052  151.2776 -33.89151 16/10/2014                      10
## 1053  151.2776 -33.89151 08/09/2014                       2
## 1054  151.2776 -33.89151 08/10/2014                      34
## 1055  151.2776 -33.89151 13/12/2014                       0
## 1056  151.2776 -33.89151 19/12/2014                       4
## 1057  151.2776 -33.89151 18/11/2014                       0
## 1058  151.2776 -33.89151 10/11/2014                       0
## 1059  151.2776 -33.89151 25/10/2014                       8
## 1060  151.2776 -33.89151 30/09/2014                       2
## 1061  151.2776 -33.89151 24/01/2014                       3
## 1062  151.2776 -33.89151 05/03/2014                       3
## 1063  151.2776 -33.89151 25/02/2014                       2
## 1064  151.2776 -33.89151 09/02/2014                       7
## 1065  151.2776 -33.89151 06/04/2014                      22
## 1066  151.2776 -33.89151 06/05/2014                       3
## 1067  151.2776 -33.89151 16/05/2014                       6
## 1068  151.2776 -33.89151 10/06/2014                      66
## 1069  151.2776 -33.89151 26/06/2014                       0
## 1070  151.2776 -33.89151 22/05/2014                       1
## 1071  151.2776 -33.89151 24/07/2014                       0
## 1072  151.2776 -33.89151 14/07/2014                       0
## 1073  151.2776 -33.89151 08/07/2014                       1
## 1074  151.2776 -33.89151 03/07/2014                       1
## 1075  151.2776 -33.89151 05/08/2014                       1
## 1076  151.2776 -33.89151 12/09/2014                       4
## 1077  151.2776 -33.89151 24/09/2014                       1
## 1078  151.2776 -33.89151 18/09/2014                       1
## 1079  151.2686 -33.90307 12/09/2014                       1
## 1080  151.2686 -33.90307 08/09/2014                       2
## 1081  151.2686 -33.90307 11/08/2014                       0
## 1082  151.2686 -33.90307 15/08/2014                       0
## 1083  151.2686 -33.90307 27/08/2014                      11
## 1084  151.2686 -33.90307 02/09/2014                       2
## 1085  151.2686 -33.90307 03/07/2014                       0
## 1086  151.2686 -33.90307 01/08/2014                       3
## 1087  151.2686 -33.90307 18/07/2014                       2
## 1088  151.2686 -33.90307 06/05/2014                       2
## 1089  151.2686 -33.90307 28/05/2014                      15
## 1090  151.2686 -33.90307 30/04/2014                       3
## 1091  151.2686 -33.90307 25/02/2014                      10
## 1092  151.2686 -33.90307 14/04/2014                       2
## 1093  151.2686 -33.90307 17/02/2014                      16
## 1094  151.2686 -33.90307 24/01/2014                       4
## 1095  151.2686 -33.90307 01/02/2014                      17
## 1096  151.2686 -33.90307 30/09/2014                       0
## 1097  151.2686 -33.90307 28/12/2014                      22
## 1098  151.2686 -33.90307 18/09/2014                       0
## 1099  151.2686 -33.90307 24/09/2014                       1
## 1100  151.2686 -33.90307 13/12/2014                       5
## 1101  151.2686 -33.90307 19/12/2014                       1
## 1102  151.2686 -33.90307 04/12/2014                      72
## 1103  151.2686 -33.90307 21/10/2014                       0
## 1104  151.2686 -33.90307 21/08/2014                      15
## 1105  151.2686 -33.90307 24/07/2014                       0
## 1106  151.2686 -33.90307 14/07/2014                       0
## 1107  151.2686 -33.90307 05/08/2014                       0
## 1108  151.2686 -33.90307 03/06/2014                       4
## 1109  151.2686 -33.90307 10/06/2014                      56
## 1110  151.2686 -33.90307 19/06/2014                       4
## 1111  151.2686 -33.90307 26/06/2014                       0
## 1112  151.2686 -33.90307 08/07/2014                       1
## 1113  151.2686 -33.90307 22/05/2014                       0
## 1114  151.2686 -33.90307 12/05/2014                       4
## 1115  151.2686 -33.90307 16/05/2014                       9
## 1116  151.2686 -33.90307 22/04/2014                       2
## 1117  151.2686 -33.90307 29/03/2014                      10
## 1118  151.2686 -33.90307 06/04/2014                     510
## 1119  151.2686 -33.90307 21/03/2014                       6
## 1120  151.2686 -33.90307 13/03/2014                      28
## 1121  151.2686 -33.90307 05/03/2014                      24
## 1122  151.2686 -33.90307 09/02/2014                       1
## 1123  151.2686 -33.90307 16/01/2014                      14
## 1124  151.2686 -33.90307 08/01/2014                       2
## 1125  151.2686 -33.90307 26/11/2014                      19
## 1126  151.2686 -33.90307 18/11/2014                       7
## 1127  151.2686 -33.90307 02/11/2014                       1
## 1128  151.2686 -33.90307 10/11/2014                       8
## 1129  151.2686 -33.90307 25/10/2014                       7
## 1130  151.2686 -33.90307 08/10/2014                       3
## 1131  151.2686 -33.90307 16/10/2014                       1
## 1132  151.2706 -33.90056 08/10/2014                      18
## 1133  151.2706 -33.90056 10/11/2014                       0
## 1134  151.2706 -33.90056 18/11/2014                       4
## 1135  151.2706 -33.90056 02/11/2014                       4
## 1136  151.2706 -33.90056 26/11/2014                      14
## 1137  151.2706 -33.90056 04/12/2014                      78
## 1138  151.2706 -33.90056 08/01/2014                      28
## 1139  151.2706 -33.90056 16/01/2014                       0
## 1140  151.2706 -33.90056 28/12/2014                      10
## 1141  151.2706 -33.90056 09/02/2014                       3
## 1142  151.2706 -33.90056 05/03/2014                      10
## 1143  151.2706 -33.90056 13/03/2014                      33
## 1144  151.2706 -33.90056 21/03/2014                       5
## 1145  151.2706 -33.90056 29/03/2014                       6
## 1146  151.2706 -33.90056 14/04/2014                       6
## 1147  151.2706 -33.90056 22/04/2014                       2
## 1148  151.2706 -33.90056 12/05/2014                       0
## 1149  151.2706 -33.90056 28/05/2014                      14
## 1150  151.2706 -33.90056 08/07/2014                       1
## 1151  151.2706 -33.90056 10/06/2014                    1100
## 1152  151.2706 -33.90056 19/06/2014                       2
## 1153  151.2706 -33.90056 03/06/2014                       1
## 1154  151.2706 -33.90056 15/08/2014                       4
## 1155  151.2706 -33.90056 01/08/2014                       2
## 1156  151.2706 -33.90056 05/08/2014                       1
## 1157  151.2706 -33.90056 24/07/2014                       0
## 1158  151.2706 -33.90056 21/08/2014                      44
## 1159  151.2706 -33.90056 11/08/2014                       0
## 1160  151.2706 -33.90056 27/08/2014                       3
## 1161  151.2706 -33.90056 21/10/2014                       0
## 1162  151.2706 -33.90056 16/10/2014                       3
## 1163  151.2706 -33.90056 19/12/2014                       5
## 1164  151.2706 -33.90056 13/12/2014                      12
## 1165  151.2706 -33.90056 25/10/2014                       5
## 1166  151.2706 -33.90056 24/09/2014                       0
## 1167  151.2706 -33.90056 30/09/2014                       4
## 1168  151.2706 -33.90056 01/02/2014                      13
## 1169  151.2706 -33.90056 24/01/2014                       2
## 1170  151.2706 -33.90056 17/02/2014                     110
## 1171  151.2706 -33.90056 25/02/2014                       1
## 1172  151.2706 -33.90056 06/04/2014                     450
## 1173  151.2706 -33.90056 30/04/2014                       7
## 1174  151.2706 -33.90056 06/05/2014                       4
## 1175  151.2706 -33.90056 16/05/2014                       3
## 1176  151.2706 -33.90056 22/05/2014                       0
## 1177  151.2706 -33.90056 26/06/2014                       9
## 1178  151.2706 -33.90056 18/07/2014                       0
## 1179  151.2706 -33.90056 03/07/2014                      68
## 1180  151.2706 -33.90056 14/07/2014                       0
## 1181  151.2706 -33.90056 02/09/2014                       0
## 1182  151.2706 -33.90056 08/09/2014                       2
## 1183  151.2706 -33.90056 12/09/2014                       7
## 1184  151.2706 -33.90056 18/09/2014                       0
## 1185  151.2675 -33.91449 27/07/2015                       1
## 1186  151.2675 -33.91449 31/07/2015                       0
## 1187  151.2675 -33.91449 07/08/2015                       0
## 1188  151.2675 -33.91449 14/08/2015                       0
## 1189  151.2675 -33.91449 19/08/2015                      19
## 1190  151.2675 -33.91449 25/08/2015                      30
## 1191  151.2675 -33.91449 29/09/2015                       0
## 1192  151.2675 -33.91449 11/11/2015                       5
## 1193  151.2675 -33.91449 17/11/2015                       2
## 1194  151.2675 -33.91449 23/11/2015                      13
## 1195  151.2675 -33.91449 29/11/2015                       2
## 1196  151.2675 -33.91449 05/12/2015                       1
## 1197  151.2675 -33.91449 17/12/2015                      17
## 1198  151.2675 -33.91449 22/12/2015                      75
## 1199  151.2675 -33.91449 29/12/2015                       0
## 1200  151.2675 -33.91449 14/02/2015                       6
## 1201  151.2675 -33.91449 06/02/2015                       6
## 1202  151.2675 -33.91449 25/03/2015                      11
## 1203  151.2675 -33.91449 17/03/2015                      12
## 1204  151.2675 -33.91449 09/04/2015                      12
## 1205  151.2675 -33.91449 01/04/2015                      44
## 1206  151.2675 -33.91449 27/04/2015                      29
## 1207  151.2675 -33.91449 17/04/2015                       4
## 1208  151.2675 -33.91449 27/05/2015                       3
## 1209  151.2675 -33.91449 09/06/2015                       1
## 1210  151.2675 -33.91449 15/06/2015                       3
## 1211  151.2675 -33.91449 20/06/2015                       4
## 1212  151.2675 -33.91449 31/08/2015                      10
## 1213  151.2675 -33.91449 04/09/2015                       7
## 1214  151.2675 -33.91449 11/09/2015                       4
## 1215  151.2675 -33.91449 17/09/2015                       0
## 1216  151.2675 -33.91449 23/09/2015                       6
## 1217  151.2675 -33.91449 26/06/2015                       1
## 1218  151.2675 -33.91449 02/07/2015                       0
## 1219  151.2675 -33.91449 21/07/2015                       3
## 1220  151.2675 -33.91449 06/10/2015                       1
## 1221  151.2675 -33.91449 12/10/2015                       3
## 1222  151.2675 -33.91449 18/10/2015                       1
## 1223  151.2675 -33.91449 24/10/2015                       2
## 1224  151.2675 -33.91449 30/10/2015                      12
## 1225  151.2675 -33.91449 05/11/2015                       9
## 1226  151.2675 -33.91449 11/12/2015                       1
## 1227  151.2675 -33.91449 05/01/2015                       2
## 1228  151.2675 -33.91449 15/01/2015                       0
## 1229  151.2675 -33.91449 21/01/2015                       6
## 1230  151.2675 -33.91449 29/01/2015                      15
## 1231  151.2675 -33.91449 22/02/2015                       1
## 1232  151.2675 -33.91449 27/02/2015                      16
## 1233  151.2675 -33.91449 05/03/2015                       1
## 1234  151.2675 -33.91449 09/03/2015                       0
## 1235  151.2675 -33.91449 05/05/2015                       2
## 1236  151.2675 -33.91449 11/05/2015                       5
## 1237  151.2675 -33.91449 22/05/2015                      84
## 1238  151.2675 -33.91449 17/05/2015                       4
## 1239  151.2675 -33.91449 03/06/2015                       7
## 1240  151.2675 -33.91449 08/07/2015                       0
## 1241  151.2675 -33.91449 15/07/2015                       0
## 1242  151.2582 -33.92076 15/07/2015                       5
## 1243  151.2582 -33.92076 08/07/2015                      25
## 1244  151.2582 -33.92076 21/07/2015                      14
## 1245  151.2582 -33.92076 15/06/2015                       0
## 1246  151.2582 -33.92076 20/06/2015                      11
## 1247  151.2582 -33.92076 26/06/2015                      10
## 1248  151.2582 -33.92076 03/06/2015                       1
## 1249  151.2582 -33.92076 09/06/2015                      22
## 1250  151.2582 -33.92076 17/05/2015                      17
## 1251  151.2582 -33.92076 22/05/2015                     200
## 1252  151.2582 -33.92076 09/03/2015                       9
## 1253  151.2582 -33.92076 05/03/2015                      32
## 1254  151.2582 -33.92076 27/02/2015                     420
## 1255  151.2582 -33.92076 22/02/2015                     180
## 1256  151.2582 -33.92076 21/01/2015                      52
## 1257  151.2582 -33.92076 05/01/2015                       7
## 1258  151.2582 -33.92076 29/12/2015                       6
## 1259  151.2582 -33.92076 11/12/2015                      19
## 1260  151.2582 -33.92076 05/12/2015                       3
## 1261  151.2582 -33.92076 05/11/2015                     230
## 1262  151.2582 -33.92076 30/10/2015                       7
## 1263  151.2582 -33.92076 18/10/2015                       3
## 1264  151.2582 -33.92076 12/10/2015                      14
## 1265  151.2582 -33.92076 06/10/2015                       2
## 1266  151.2582 -33.92076 23/09/2015                       3
## 1267  151.2582 -33.92076 29/09/2015                      11
## 1268  151.2582 -33.92076 02/07/2015                       4
## 1269  151.2582 -33.92076 17/09/2015                       0
## 1270  151.2582 -33.92076 11/09/2015                       2
## 1271  151.2582 -33.92076 04/09/2015                      80
## 1272  151.2582 -33.92076 31/08/2015                      10
## 1273  151.2582 -33.92076 14/08/2015                       3
## 1274  151.2582 -33.92076 07/08/2015                       1
## 1275  151.2582 -33.92076 27/05/2015                       1
## 1276  151.2582 -33.92076 17/04/2015                      66
## 1277  151.2582 -33.92076 11/05/2015                       5
## 1278  151.2582 -33.92076 27/04/2015                      31
## 1279  151.2582 -33.92076 05/05/2015                      42
## 1280  151.2582 -33.92076 01/04/2015                      57
## 1281  151.2582 -33.92076 09/04/2015                       5
## 1282  151.2582 -33.92076 17/03/2015                     140
## 1283  151.2582 -33.92076 25/03/2015                      24
## 1284  151.2582 -33.92076 06/02/2015                      16
## 1285  151.2582 -33.92076 14/02/2015                      11
## 1286  151.2582 -33.92076 29/01/2015                       9
## 1287  151.2582 -33.92076 15/01/2015                       3
## 1288  151.2582 -33.92076 22/12/2015                     110
## 1289  151.2582 -33.92076 17/12/2015                      90
## 1290  151.2582 -33.92076 29/11/2015                      21
## 1291  151.2582 -33.92076 23/11/2015                       7
## 1292  151.2582 -33.92076 17/11/2015                      50
## 1293  151.2582 -33.92076 11/11/2015                     140
## 1294  151.2582 -33.92076 24/10/2015                       8
## 1295  151.2582 -33.92076 25/08/2015                      55
## 1296  151.2582 -33.92076 19/08/2015                       2
## 1297  151.2582 -33.92076 31/07/2015                       0
## 1298  151.2582 -33.92076 27/07/2015                       3
## 1299  151.2646 -33.91565 27/07/2015                       0
## 1300  151.2646 -33.91565 31/07/2015                       0
## 1301  151.2646 -33.91565 07/08/2015                       0
## 1302  151.2646 -33.91565 19/08/2015                       3
## 1303  151.2646 -33.91565 14/08/2015                       0
## 1304  151.2646 -33.91565 25/08/2015                      14
## 1305  151.2646 -33.91565 31/08/2015                       2
## 1306  151.2646 -33.91565 29/09/2015                       0
## 1307  151.2646 -33.91565 06/10/2015                      17
## 1308  151.2646 -33.91565 23/09/2015                       8
## 1309  151.2646 -33.91565 17/11/2015                       2
## 1310  151.2646 -33.91565 30/10/2015                      10
## 1311  151.2646 -33.91565 29/11/2015                       3
## 1312  151.2646 -33.91565 05/12/2015                       0
## 1313  151.2646 -33.91565 11/12/2015                      25
## 1314  151.2646 -33.91565 17/12/2015                       5
## 1315  151.2646 -33.91565 22/12/2015                      47
## 1316  151.2646 -33.91565 29/12/2015                       1
## 1317  151.2646 -33.91565 05/01/2015                       3
## 1318  151.2646 -33.91565 06/02/2015                       9
## 1319  151.2646 -33.91565 25/03/2015                      12
## 1320  151.2646 -33.91565 01/04/2015                      26
## 1321  151.2646 -33.91565 09/04/2015                      19
## 1322  151.2646 -33.91565 17/04/2015                       1
## 1323  151.2646 -33.91565 05/03/2015                      35
## 1324  151.2646 -33.91565 17/03/2015                       0
## 1325  151.2646 -33.91565 27/04/2015                      70
## 1326  151.2646 -33.91565 20/06/2015                       5
## 1327  151.2646 -33.91565 15/06/2015                       0
## 1328  151.2646 -33.91565 27/05/2015                      40
## 1329  151.2646 -33.91565 09/06/2015                       1
## 1330  151.2646 -33.91565 04/09/2015                      21
## 1331  151.2646 -33.91565 11/09/2015                       0
## 1332  151.2646 -33.91565 26/06/2015                       2
## 1333  151.2646 -33.91565 02/07/2015                       1
## 1334  151.2646 -33.91565 17/09/2015                       1
## 1335  151.2646 -33.91565 21/07/2015                       2
## 1336  151.2646 -33.91565 08/07/2015                       6
## 1337  151.2646 -33.91565 15/07/2015                       1
## 1338  151.2646 -33.91565 12/10/2015                       1
## 1339  151.2646 -33.91565 18/10/2015                       0
## 1340  151.2646 -33.91565 24/10/2015                       1
## 1341  151.2646 -33.91565 05/11/2015                      31
## 1342  151.2646 -33.91565 11/11/2015                      33
## 1343  151.2646 -33.91565 23/11/2015                       1
## 1344  151.2646 -33.91565 15/01/2015                       0
## 1345  151.2646 -33.91565 22/02/2015                      48
## 1346  151.2646 -33.91565 21/01/2015                      10
## 1347  151.2646 -33.91565 29/01/2015                       5
## 1348  151.2646 -33.91565 14/02/2015                       1
## 1349  151.2646 -33.91565 17/05/2015                       2
## 1350  151.2646 -33.91565 11/05/2015                       1
## 1351  151.2646 -33.91565 05/05/2015                       1
## 1352  151.2646 -33.91565 22/05/2015                    1500
## 1353  151.2646 -33.91565 27/02/2015                      28
## 1354  151.2646 -33.91565 09/03/2015                       0
## 1355  151.2646 -33.91565 03/06/2015                       8
## 1356  151.2515 -33.98012 02/07/2015                      16
## 1357  151.2515 -33.98012 17/03/2015                      18
## 1358  151.2515 -33.98012 25/03/2015                       7
## 1359  151.2515 -33.98012 09/04/2015                      14
## 1360  151.2515 -33.98012 17/04/2015                      50
## 1361  151.2515 -33.98012 03/06/2015                       7
## 1362  151.2515 -33.98012 27/04/2015                      12
## 1363  151.2515 -33.98012 05/05/2015                       7
## 1364  151.2515 -33.98012 11/05/2015                       9
## 1365  151.2515 -33.98012 06/02/2015                      16
## 1366  151.2515 -33.98012 29/01/2015                      30
## 1367  151.2515 -33.98012 14/02/2015                      18
## 1368  151.2515 -33.98012 09/03/2015                       1
## 1369  151.2515 -33.98012 15/01/2015                       1
## 1370  151.2515 -33.98012 21/01/2015                       6
## 1371  151.2515 -33.98012 22/12/2015                      72
## 1372  151.2515 -33.98012 29/11/2015                      18
## 1373  151.2515 -33.98012 17/12/2015                      92
## 1374  151.2515 -33.98012 23/11/2015                      16
## 1375  151.2515 -33.98012 11/11/2015                      31
## 1376  151.2515 -33.98012 24/10/2015                       5
## 1377  151.2515 -33.98012 18/10/2015                       8
## 1378  151.2515 -33.98012 12/10/2015                       5
## 1379  151.2515 -33.98012 08/07/2015                      22
## 1380  151.2515 -33.98012 21/07/2015                       9
## 1381  151.2515 -33.98012 15/07/2015                       4
## 1382  151.2515 -33.98012 20/06/2015                      31
## 1383  151.2515 -33.98012 26/06/2015                      12
## 1384  151.2515 -33.98012 25/08/2015                      31
## 1385  151.2515 -33.98012 11/09/2015                       2
## 1386  151.2515 -33.98012 31/07/2015                       1
## 1387  151.2515 -33.98012 19/08/2015                       2
## 1388  151.2515 -33.98012 09/06/2015                       8
## 1389  151.2515 -33.98012 15/06/2015                      95
## 1390  151.2515 -33.98012 27/07/2015                       7
## 1391  151.2515 -33.98012 17/05/2015                      21
## 1392  151.2515 -33.98012 27/05/2015                       3
## 1393  151.2515 -33.98012 22/05/2015                      86
## 1394  151.2515 -33.98012 05/03/2015                      20
## 1395  151.2515 -33.98012 27/02/2015                       1
## 1396  151.2515 -33.98012 01/04/2015                      19
## 1397  151.2515 -33.98012 22/02/2015                      10
## 1398  151.2515 -33.98012 05/01/2015                      35
## 1399  151.2515 -33.98012 29/12/2015                       6
## 1400  151.2515 -33.98012 11/12/2015                     480
## 1401  151.2515 -33.98012 05/12/2015                       2
## 1402  151.2515 -33.98012 30/10/2015                       8
## 1403  151.2515 -33.98012 05/11/2015                      16
## 1404  151.2515 -33.98012 17/11/2015                      10
## 1405  151.2515 -33.98012 06/10/2015                       1
## 1406  151.2515 -33.98012 17/09/2015                       8
## 1407  151.2515 -33.98012 23/09/2015                       3
## 1408  151.2515 -33.98012 29/09/2015                       0
## 1409  151.2515 -33.98012 31/08/2015                      15
## 1410  151.2515 -33.98012 04/09/2015                      26
## 1411  151.2515 -33.98012 14/08/2015                       0
## 1412  151.2515 -33.98012 07/08/2015                       0
## 1413  151.2522 -33.96436 07/08/2015                       8
## 1414  151.2522 -33.96436 14/08/2015                      39
## 1415  151.2522 -33.96436 04/09/2015                     110
## 1416  151.2522 -33.96436 31/08/2015                      13
## 1417  151.2522 -33.96436 11/09/2015                       7
## 1418  151.2522 -33.96436 17/09/2015                       6
## 1419  151.2522 -33.96436 29/09/2015                      36
## 1420  151.2522 -33.96436 23/09/2015                     120
## 1421  151.2522 -33.96436 06/10/2015                       7
## 1422  151.2522 -33.96436 12/10/2015                      18
## 1423  151.2522 -33.96436 18/10/2015                      12
## 1424  151.2522 -33.96436 30/10/2015                     120
## 1425  151.2522 -33.96436 05/11/2015                      11
## 1426  151.2522 -33.96436 05/12/2015                       4
## 1427  151.2522 -33.96436 11/12/2015                     360
## 1428  151.2522 -33.96436 29/12/2015                       8
## 1429  151.2522 -33.96436 05/01/2015                     570
## 1430  151.2522 -33.96436 22/02/2015                       8
## 1431  151.2522 -33.96436 27/02/2015                       2
## 1432  151.2522 -33.96436 05/03/2015                      24
## 1433  151.2522 -33.96436 09/03/2015                      45
## 1434  151.2522 -33.96436 17/05/2015                      15
## 1435  151.2522 -33.96436 05/05/2015                       4
## 1436  151.2522 -33.96436 27/07/2015                       6
## 1437  151.2522 -33.96436 15/06/2015                      12
## 1438  151.2522 -33.96436 03/06/2015                      45
## 1439  151.2522 -33.96436 22/05/2015                     190
## 1440  151.2522 -33.96436 19/08/2015                       7
## 1441  151.2522 -33.96436 25/08/2015                      19
## 1442  151.2522 -33.96436 31/07/2015                      13
## 1443  151.2522 -33.96436 20/06/2015                      12
## 1444  151.2522 -33.96436 26/06/2015                       4
## 1445  151.2522 -33.96436 15/07/2015                      10
## 1446  151.2522 -33.96436 21/07/2015                       8
## 1447  151.2522 -33.96436 08/07/2015                      28
## 1448  151.2522 -33.96436 24/10/2015                       4
## 1449  151.2522 -33.96436 17/11/2015                       4
## 1450  151.2522 -33.96436 11/11/2015                      82
## 1451  151.2522 -33.96436 23/11/2015                      58
## 1452  151.2522 -33.96436 17/12/2015                     100
## 1453  151.2522 -33.96436 29/11/2015                     140
## 1454  151.2522 -33.96436 22/12/2015                     180
## 1455  151.2522 -33.96436 15/01/2015                      10
## 1456  151.2522 -33.96436 21/01/2015                     110
## 1457  151.2522 -33.96436 14/02/2015                      16
## 1458  151.2522 -33.96436 29/01/2015                       8
## 1459  151.2522 -33.96436 06/02/2015                      61
## 1460  151.2522 -33.96436 11/05/2015                      40
## 1461  151.2522 -33.96436 27/05/2015                       0
## 1462  151.2522 -33.96436 17/04/2015                     900
## 1463  151.2522 -33.96436 27/04/2015                      21
## 1464  151.2522 -33.96436 09/04/2015                      10
## 1465  151.2522 -33.96436 01/04/2015                      50
## 1466  151.2522 -33.96436 17/03/2015                       6
## 1467  151.2522 -33.96436 25/03/2015                      31
## 1468  151.2522 -33.96436 02/07/2015                      78
## 1469  151.2522 -33.96436 09/06/2015                       2
## 1470  151.2572 -33.94879 26/06/2015                      20
## 1471  151.2572 -33.94879 20/06/2015                       8
## 1472  151.2572 -33.94879 15/06/2015                       4
## 1473  151.2572 -33.94879 21/07/2015                       1
## 1474  151.2572 -33.94879 08/07/2015                      32
## 1475  151.2572 -33.94879 15/07/2015                       2
## 1476  151.2572 -33.94879 01/04/2015                      12
## 1477  151.2572 -33.94879 17/05/2015                      30
## 1478  151.2572 -33.94879 27/05/2015                       0
## 1479  151.2572 -33.94879 09/06/2015                      10
## 1480  151.2572 -33.94879 22/05/2015                     180
## 1481  151.2572 -33.94879 22/02/2015                      21
## 1482  151.2572 -33.94879 27/02/2015                       3
## 1483  151.2572 -33.94879 05/03/2015                      29
## 1484  151.2572 -33.94879 05/01/2015                       1
## 1485  151.2572 -33.94879 29/12/2015                       1
## 1486  151.2572 -33.94879 05/12/2015                       0
## 1487  151.2572 -33.94879 11/12/2015                       1
## 1488  151.2572 -33.94879 17/11/2015                       0
## 1489  151.2572 -33.94879 30/10/2015                       1
## 1490  151.2572 -33.94879 06/10/2015                       0
## 1491  151.2572 -33.94879 29/09/2015                       0
## 1492  151.2572 -33.94879 23/09/2015                       4
## 1493  151.2572 -33.94879 02/07/2015                       3
## 1494  151.2572 -33.94879 14/08/2015                       2
## 1495  151.2572 -33.94879 17/09/2015                       0
## 1496  151.2572 -33.94879 31/08/2015                       7
## 1497  151.2572 -33.94879 04/09/2015                       9
## 1498  151.2572 -33.94879 03/06/2015                       1
## 1499  151.2572 -33.94879 07/08/2015                       0
## 1500  151.2572 -33.94879 17/04/2015                       8
## 1501  151.2572 -33.94879 11/05/2015                       5
## 1502  151.2572 -33.94879 05/05/2015                       5
## 1503  151.2572 -33.94879 27/04/2015                      15
## 1504  151.2572 -33.94879 09/03/2015                       0
## 1505  151.2572 -33.94879 09/04/2015                       5
## 1506  151.2572 -33.94879 17/03/2015                      18
## 1507  151.2572 -33.94879 25/03/2015                       8
## 1508  151.2572 -33.94879 06/02/2015                       1
## 1509  151.2572 -33.94879 29/01/2015                       5
## 1510  151.2572 -33.94879 14/02/2015                       7
## 1511  151.2572 -33.94879 15/01/2015                       2
## 1512  151.2572 -33.94879 21/01/2015                      78
## 1513  151.2572 -33.94879 22/12/2015                      52
## 1514  151.2572 -33.94879 17/12/2015                      39
## 1515  151.2572 -33.94879 23/11/2015                       2
## 1516  151.2572 -33.94879 29/11/2015                       9
## 1517  151.2572 -33.94879 05/11/2015                     150
## 1518  151.2572 -33.94879 11/11/2015                       3
## 1519  151.2572 -33.94879 18/10/2015                       2
## 1520  151.2572 -33.94879 24/10/2015                       2
## 1521  151.2572 -33.94879 12/10/2015                       6
## 1522  151.2572 -33.94879 11/09/2015                       1
## 1523  151.2572 -33.94879 19/08/2015                       0
## 1524  151.2572 -33.94879 25/08/2015                      21
## 1525  151.2572 -33.94879 27/07/2015                       2
## 1526  151.2572 -33.94879 31/07/2015                       0
## 1527  151.2572 -33.95161 25/08/2015                      17
## 1528  151.2572 -33.95161 11/09/2015                       0
## 1529  151.2572 -33.95161 17/09/2015                       0
## 1530  151.2572 -33.95161 12/10/2015                       3
## 1531  151.2572 -33.95161 24/10/2015                       0
## 1532  151.2572 -33.95161 18/10/2015                       0
## 1533  151.2572 -33.95161 11/11/2015                      12
## 1534  151.2572 -33.95161 05/11/2015                      13
## 1535  151.2572 -33.95161 23/11/2015                       0
## 1536  151.2572 -33.95161 17/12/2015                      42
## 1537  151.2572 -33.95161 21/01/2015                       8
## 1538  151.2572 -33.95161 15/01/2015                       2
## 1539  151.2572 -33.95161 14/02/2015                       3
## 1540  151.2572 -33.95161 29/01/2015                       1
## 1541  151.2572 -33.95161 22/02/2015                      13
## 1542  151.2572 -33.95161 25/03/2015                       4
## 1543  151.2572 -33.95161 09/03/2015                       1
## 1544  151.2572 -33.95161 27/02/2015                       0
## 1545  151.2572 -33.95161 27/04/2015                       2
## 1546  151.2572 -33.95161 05/05/2015                       9
## 1547  151.2572 -33.95161 11/05/2015                       6
## 1548  151.2572 -33.95161 17/05/2015                       0
## 1549  151.2572 -33.95161 22/05/2015                     130
## 1550  151.2572 -33.95161 07/08/2015                       0
## 1551  151.2572 -33.95161 31/07/2015                       1
## 1552  151.2572 -33.95161 27/07/2015                       0
## 1553  151.2572 -33.95161 03/06/2015                       0
## 1554  151.2572 -33.95161 04/09/2015                       9
## 1555  151.2572 -33.95161 31/08/2015                       6
## 1556  151.2572 -33.95161 14/08/2015                       0
## 1557  151.2572 -33.95161 19/08/2015                       0
## 1558  151.2572 -33.95161 02/07/2015                       5
## 1559  151.2572 -33.95161 23/09/2015                      10
## 1560  151.2572 -33.95161 29/09/2015                       1
## 1561  151.2572 -33.95161 06/10/2015                       0
## 1562  151.2572 -33.95161 30/10/2015                      55
## 1563  151.2572 -33.95161 17/11/2015                       8
## 1564  151.2572 -33.95161 11/12/2015                       4
## 1565  151.2572 -33.95161 05/12/2015                       0
## 1566  151.2572 -33.95161 29/11/2015                       2
## 1567  151.2572 -33.95161 29/12/2015                       0
## 1568  151.2572 -33.95161 22/12/2015                      29
## 1569  151.2572 -33.95161 05/01/2015                       1
## 1570  151.2572 -33.95161 05/03/2015                       5
## 1571  151.2572 -33.95161 06/02/2015                       1
## 1572  151.2572 -33.95161 09/06/2015                       2
## 1573  151.2572 -33.95161 27/05/2015                       1
## 1574  151.2572 -33.95161 01/04/2015                       5
## 1575  151.2572 -33.95161 17/03/2015                      10
## 1576  151.2572 -33.95161 09/04/2015                       4
## 1577  151.2572 -33.95161 17/04/2015                       1
## 1578  151.2572 -33.95161 15/07/2015                       2
## 1579  151.2572 -33.95161 08/07/2015                      26
## 1580  151.2572 -33.95161 21/07/2015                       5
## 1581  151.2572 -33.95161 15/06/2015                       3
## 1582  151.2572 -33.95161 20/06/2015                       6
## 1583  151.2572 -33.95161 26/06/2015                       2
## 1584  151.2582 -33.95354 26/06/2015                      23
## 1585  151.2582 -33.95354 20/06/2015                      40
## 1586  151.2582 -33.95354 15/06/2015                      75
## 1587  151.2582 -33.95354 21/07/2015                       3
## 1588  151.2582 -33.95354 02/07/2015                       1
## 1589  151.2582 -33.95354 17/04/2015                       7
## 1590  151.2582 -33.95354 27/04/2015                      90
## 1591  151.2582 -33.95354 09/04/2015                      88
## 1592  151.2582 -33.95354 17/03/2015                      80
## 1593  151.2582 -33.95354 01/04/2015                      14
## 1594  151.2582 -33.95354 25/03/2015                      22
## 1595  151.2582 -33.95354 27/05/2015                       5
## 1596  151.2582 -33.95354 09/06/2015                       0
## 1597  151.2582 -33.95354 06/02/2015                      11
## 1598  151.2582 -33.95354 14/02/2015                      11
## 1599  151.2582 -33.95354 22/12/2015                      60
## 1600  151.2582 -33.95354 29/12/2015                      25
## 1601  151.2582 -33.95354 17/12/2015                     130
## 1602  151.2582 -33.95354 29/11/2015                      47
## 1603  151.2582 -33.95354 23/11/2015                       7
## 1604  151.2582 -33.95354 05/12/2015                       0
## 1605  151.2582 -33.95354 11/12/2015                      16
## 1606  151.2582 -33.95354 17/11/2015                       0
## 1607  151.2582 -33.95354 11/11/2015                       8
## 1608  151.2582 -33.95354 29/09/2015                       6
## 1609  151.2582 -33.95354 15/07/2015                       0
## 1610  151.2582 -33.95354 08/07/2015                      19
## 1611  151.2582 -33.95354 19/08/2015                       1
## 1612  151.2582 -33.95354 25/08/2015                      78
## 1613  151.2582 -33.95354 14/08/2015                       0
## 1614  151.2582 -33.95354 03/06/2015                       2
## 1615  151.2582 -33.95354 27/07/2015                       0
## 1616  151.2582 -33.95354 31/07/2015                      11
## 1617  151.2582 -33.95354 07/08/2015                       0
## 1618  151.2582 -33.95354 22/05/2015                     840
## 1619  151.2582 -33.95354 17/05/2015                      40
## 1620  151.2582 -33.95354 11/05/2015                      13
## 1621  151.2582 -33.95354 05/05/2015                       7
## 1622  151.2582 -33.95354 27/02/2015                       4
## 1623  151.2582 -33.95354 05/03/2015                      10
## 1624  151.2582 -33.95354 09/03/2015                       2
## 1625  151.2582 -33.95354 22/02/2015                      92
## 1626  151.2582 -33.95354 29/01/2015                      31
## 1627  151.2582 -33.95354 15/01/2015                       2
## 1628  151.2582 -33.95354 21/01/2015                      18
## 1629  151.2582 -33.95354 05/01/2015                      14
## 1630  151.2582 -33.95354 05/11/2015                     150
## 1631  151.2582 -33.95354 30/10/2015                       1
## 1632  151.2582 -33.95354 18/10/2015                      10
## 1633  151.2582 -33.95354 24/10/2015                       0
## 1634  151.2582 -33.95354 12/10/2015                      13
## 1635  151.2582 -33.95354 17/09/2015                       0
## 1636  151.2582 -33.95354 11/09/2015                       1
## 1637  151.2582 -33.95354 04/09/2015                     540
## 1638  151.2582 -33.95354 23/09/2015                       8
## 1639  151.2582 -33.95354 06/10/2015                      13
## 1640  151.2582 -33.95354 31/08/2015                       5
## 1641  151.2776 -33.89151 31/08/2015                       4
## 1642  151.2776 -33.89151 06/10/2015                       0
## 1643  151.2776 -33.89151 23/09/2015                       3
## 1644  151.2776 -33.89151 11/09/2015                       2
## 1645  151.2776 -33.89151 04/09/2015                      21
## 1646  151.2776 -33.89151 17/09/2015                      10
## 1647  151.2776 -33.89151 18/10/2015                       5
## 1648  151.2776 -33.89151 12/10/2015                       5
## 1649  151.2776 -33.89151 30/10/2015                       0
## 1650  151.2776 -33.89151 05/11/2015                      31
## 1651  151.2776 -33.89151 29/12/2015                       3
## 1652  151.2776 -33.89151 11/12/2015                       4
## 1653  151.2776 -33.89151 05/01/2015                       4
## 1654  151.2776 -33.89151 29/01/2015                       5
## 1655  151.2776 -33.89151 21/01/2015                       6
## 1656  151.2776 -33.89151 22/02/2015                       4
## 1657  151.2776 -33.89151 27/02/2015                       9
## 1658  151.2776 -33.89151 09/03/2015                       8
## 1659  151.2776 -33.89151 05/03/2015                      16
## 1660  151.2776 -33.89151 05/05/2015                      18
## 1661  151.2776 -33.89151 17/05/2015                       4
## 1662  151.2776 -33.89151 11/05/2015                       4
## 1663  151.2776 -33.89151 22/05/2015                     270
## 1664  151.2776 -33.89151 03/06/2015                      25
## 1665  151.2776 -33.89151 14/08/2015                       3
## 1666  151.2776 -33.89151 31/07/2015                       3
## 1667  151.2776 -33.89151 27/07/2015                       0
## 1668  151.2776 -33.89151 19/08/2015                       9
## 1669  151.2776 -33.89151 07/08/2015                       0
## 1670  151.2776 -33.89151 25/08/2015                      18
## 1671  151.2776 -33.89151 15/07/2015                       1
## 1672  151.2776 -33.89151 08/07/2015                       4
## 1673  151.2776 -33.89151 29/09/2015                       1
## 1674  151.2776 -33.89151 24/10/2015                       3
## 1675  151.2776 -33.89151 11/11/2015                       8
## 1676  151.2776 -33.89151 17/11/2015                       6
## 1677  151.2776 -33.89151 23/11/2015                       0
## 1678  151.2776 -33.89151 17/12/2015                      38
## 1679  151.2776 -33.89151 29/11/2015                       3
## 1680  151.2776 -33.89151 22/12/2015                      64
## 1681  151.2776 -33.89151 05/12/2015                       0
## 1682  151.2776 -33.89151 15/01/2015                       2
## 1683  151.2776 -33.89151 14/02/2015                      36
## 1684  151.2776 -33.89151 06/02/2015                       1
## 1685  151.2776 -33.89151 17/03/2015                       3
## 1686  151.2776 -33.89151 09/06/2015                       3
## 1687  151.2776 -33.89151 27/05/2015                       4
## 1688  151.2776 -33.89151 01/04/2015                      25
## 1689  151.2776 -33.89151 25/03/2015                      42
## 1690  151.2776 -33.89151 09/04/2015                      16
## 1691  151.2776 -33.89151 17/04/2015                       7
## 1692  151.2776 -33.89151 27/04/2015                      27
## 1693  151.2776 -33.89151 21/07/2015                       7
## 1694  151.2776 -33.89151 20/06/2015                       4
## 1695  151.2776 -33.89151 26/06/2015                       8
## 1696  151.2776 -33.89151 02/07/2015                       6
## 1697  151.2776 -33.89151 15/06/2015                       4
## 1698  151.2686 -33.90307 02/07/2015                       6
## 1699  151.2686 -33.90307 27/04/2015                      28
## 1700  151.2686 -33.90307 09/04/2015                      18
## 1701  151.2686 -33.90307 17/03/2015                       8
## 1702  151.2686 -33.90307 09/03/2015                       0
## 1703  151.2686 -33.90307 25/03/2015                      14
## 1704  151.2686 -33.90307 11/05/2015                       0
## 1705  151.2686 -33.90307 05/05/2015                       1
## 1706  151.2686 -33.90307 03/06/2015                      21
## 1707  151.2686 -33.90307 22/02/2015                      72
## 1708  151.2686 -33.90307 06/02/2015                      10
## 1709  151.2686 -33.90307 29/01/2015                       3
## 1710  151.2686 -33.90307 14/02/2015                       3
## 1711  151.2686 -33.90307 15/01/2015                       0
## 1712  151.2686 -33.90307 21/01/2015                      40
## 1713  151.2686 -33.90307 17/12/2015                      32
## 1714  151.2686 -33.90307 22/12/2015                     210
## 1715  151.2686 -33.90307 29/11/2015                       2
## 1716  151.2686 -33.90307 23/11/2015                       5
## 1717  151.2686 -33.90307 11/11/2015                       6
## 1718  151.2686 -33.90307 24/10/2015                       4
## 1719  151.2686 -33.90307 18/10/2015                      11
## 1720  151.2686 -33.90307 05/11/2015                     390
## 1721  151.2686 -33.90307 12/10/2015                       0
## 1722  151.2686 -33.90307 08/07/2015                      25
## 1723  151.2686 -33.90307 26/06/2015                       7
## 1724  151.2686 -33.90307 15/07/2015                      13
## 1725  151.2686 -33.90307 21/07/2015                      11
## 1726  151.2686 -33.90307 25/08/2015                      65
## 1727  151.2686 -33.90307 19/08/2015                       1
## 1728  151.2686 -33.90307 11/09/2015                       2
## 1729  151.2686 -33.90307 20/06/2015                      12
## 1730  151.2686 -33.90307 27/07/2015                       1
## 1731  151.2686 -33.90307 09/06/2015                      11
## 1732  151.2686 -33.90307 15/06/2015                       2
## 1733  151.2686 -33.90307 27/05/2015                      NA
## 1734  151.2686 -33.90307 22/05/2015                      46
## 1735  151.2686 -33.90307 17/05/2015                      26
## 1736  151.2686 -33.90307 27/02/2015                       9
## 1737  151.2686 -33.90307 05/03/2015                      41
## 1738  151.2686 -33.90307 01/04/2015                      21
## 1739  151.2686 -33.90307 17/04/2015                      36
## 1740  151.2686 -33.90307 05/01/2015                       1
## 1741  151.2686 -33.90307 11/12/2015                      52
## 1742  151.2686 -33.90307 05/12/2015                       0
## 1743  151.2686 -33.90307 29/12/2015                       1
## 1744  151.2686 -33.90307 17/11/2015                       1
## 1745  151.2686 -33.90307 30/10/2015                       1
## 1746  151.2686 -33.90307 06/10/2015                       2
## 1747  151.2686 -33.90307 17/09/2015                       4
## 1748  151.2686 -33.90307 04/09/2015                      31
## 1749  151.2686 -33.90307 23/09/2015                       2
## 1750  151.2686 -33.90307 29/09/2015                       1
## 1751  151.2686 -33.90307 31/08/2015                       2
## 1752  151.2686 -33.90307 14/08/2015                       1
## 1753  151.2686 -33.90307 31/07/2015                       7
## 1754  151.2686 -33.90307 07/08/2015                       2
## 1755  151.2706 -33.90056 14/08/2015                       0
## 1756  151.2706 -33.90056 07/08/2015                       1
## 1757  151.2706 -33.90056 31/08/2015                       3
## 1758  151.2706 -33.90056 06/10/2015                       1
## 1759  151.2706 -33.90056 29/09/2015                       2
## 1760  151.2706 -33.90056 23/09/2015                      29
## 1761  151.2706 -33.90056 04/09/2015                      42
## 1762  151.2706 -33.90056 17/09/2015                       0
## 1763  151.2706 -33.90056 12/10/2015                       3
## 1764  151.2706 -33.90056 30/10/2015                       0
## 1765  151.2706 -33.90056 05/11/2015                     410
## 1766  151.2706 -33.90056 29/12/2015                       2
## 1767  151.2706 -33.90056 11/12/2015                      16
## 1768  151.2706 -33.90056 05/12/2015                       0
## 1769  151.2706 -33.90056 05/01/2015                       4
## 1770  151.2706 -33.90056 27/02/2015                     300
## 1771  151.2706 -33.90056 22/02/2015                      42
## 1772  151.2706 -33.90056 05/03/2015                       4
## 1773  151.2706 -33.90056 22/05/2015                     900
## 1774  151.2706 -33.90056 17/05/2015                      22
## 1775  151.2706 -33.90056 15/06/2015                       1
## 1776  151.2706 -33.90056 20/06/2015                       3
## 1777  151.2706 -33.90056 09/06/2015                       5
## 1778  151.2706 -33.90056 27/07/2015                       3
## 1779  151.2706 -33.90056 31/07/2015                       5
## 1780  151.2706 -33.90056 11/09/2015                       1
## 1781  151.2706 -33.90056 19/08/2015                       1
## 1782  151.2706 -33.90056 25/08/2015                      42
## 1783  151.2706 -33.90056 21/07/2015                       2
## 1784  151.2706 -33.90056 15/07/2015                       1
## 1785  151.2706 -33.90056 26/06/2015                       5
## 1786  151.2706 -33.90056 08/07/2015                      13
## 1787  151.2706 -33.90056 18/10/2015                       2
## 1788  151.2706 -33.90056 24/10/2015                       2
## 1789  151.2706 -33.90056 11/11/2015                     450
## 1790  151.2706 -33.90056 23/11/2015                       1
## 1791  151.2706 -33.90056 17/11/2015                      15
## 1792  151.2706 -33.90056 29/11/2015                       1
## 1793  151.2706 -33.90056 17/12/2015                      28
## 1794  151.2706 -33.90056 22/12/2015                     690
## 1795  151.2706 -33.90056 21/01/2015                      10
## 1796  151.2706 -33.90056 29/01/2015                       8
## 1797  151.2706 -33.90056 15/01/2015                       1
## 1798  151.2706 -33.90056 14/02/2015                       1
## 1799  151.2706 -33.90056 06/02/2015                       1
## 1800  151.2706 -33.90056 17/03/2015                       7
## 1801  151.2706 -33.90056 09/03/2015                       4
## 1802  151.2706 -33.90056 03/06/2015                      24
## 1803  151.2706 -33.90056 05/05/2015                       2
## 1804  151.2706 -33.90056 11/05/2015                      17
## 1805  151.2706 -33.90056 27/05/2015                       7
## 1806  151.2706 -33.90056 01/04/2015                      43
## 1807  151.2706 -33.90056 25/03/2015                      32
## 1808  151.2706 -33.90056 17/04/2015                      10
## 1809  151.2706 -33.90056 09/04/2015                       4
## 1810  151.2706 -33.90056 27/04/2015                      20
## 1811  151.2706 -33.90056 02/07/2015                       5
## 1812  151.2675 -33.91449 04/01/2016                       8
## 1813  151.2675 -33.91449 28/01/2016                       4
## 1814  151.2675 -33.91449 21/02/2016                     110
## 1815  151.2675 -33.91449 27/02/2016                       4
## 1816  151.2675 -33.91449 04/03/2016                       3
## 1817  151.2675 -33.91449 22/03/2016                      12
## 1818  151.2675 -33.91449 04/04/2016                     130
## 1819  151.2675 -33.91449 29/03/2016                      15
## 1820  151.2675 -33.91449 20/04/2016                       3
## 1821  151.2675 -33.91449 04/05/2016                       8
## 1822  151.2675 -33.91449 17/05/2016                       1
## 1823  151.2675 -33.91449 03/06/2016                       1
## 1824  151.2675 -33.91449 21/06/2016                       9
## 1825  151.2675 -33.91449 28/06/2016                       1
## 1826  151.2675 -33.91449 08/07/2016                      35
## 1827  151.2675 -33.91449 21/07/2016                      15
## 1828  151.2675 -33.91449 27/07/2016                       2
## 1829  151.2675 -33.91449 02/08/2016                       3
## 1830  151.2675 -33.91449 09/08/2016                       2
## 1831  151.2675 -33.91449 15/08/2016                       0
## 1832  151.2675 -33.91449 26/08/2016                       0
## 1833  151.2675 -33.91449 10/01/2016                       3
## 1834  151.2675 -33.91449 16/01/2016                       3
## 1835  151.2675 -33.91449 22/01/2016                      10
## 1836  151.2675 -33.91449 03/02/2016                       7
## 1837  151.2675 -33.91449 09/02/2016                       1
## 1838  151.2675 -33.91449 15/02/2016                       3
## 1839  151.2675 -33.91449 10/03/2016                       0
## 1840  151.2675 -33.91449 16/03/2016                      24
## 1841  151.2675 -33.91449 08/04/2016                      11
## 1842  151.2675 -33.91449 15/04/2016                       9
## 1843  151.2675 -33.91449 28/04/2016                       0
## 1844  151.2675 -33.91449 10/05/2016                       4
## 1845  151.2675 -33.91449 23/05/2016                       0
## 1846  151.2675 -33.91449 09/06/2016                     120
## 1847  151.2675 -33.91449 16/06/2016                       5
## 1848  151.2675 -33.91449 05/07/2016                      11
## 1849  151.2675 -33.91449 15/07/2016                       2
## 1850  151.2675 -33.91449 19/08/2016                       1
## 1851  151.2675 -33.91449 07/09/2016                       1
## 1852  151.2675 -33.91449 14/09/2016                       1
## 1853  151.2675 -33.91449 12/10/2016                       0
## 1854  151.2675 -33.91449 25/10/2016                      11
## 1855  151.2675 -33.91449 31/10/2016                       2
## 1856  151.2675 -33.91449 05/11/2016                       0
## 1857  151.2675 -33.91449 17/11/2016                       2
## 1858  151.2675 -33.91449 01/09/2016                       1
## 1859  151.2675 -33.91449 20/09/2016                       0
## 1860  151.2675 -33.91449 26/09/2016                       3
## 1861  151.2675 -33.91449 30/09/2016                       0
## 1862  151.2675 -33.91449 18/10/2016                       1
## 1863  151.2675 -33.91449 10/11/2016                       3
## 1864  151.2675 -33.91449 05/12/2016                       0
## 1865  151.2675 -33.91449 12/12/2016                       1
## 1866  151.2675 -33.91449 23/11/2016                       1
## 1867  151.2675 -33.91449 30/11/2016                       0
## 1868  151.2675 -33.91449 16/12/2016                      50
## 1869  151.2675 -33.91449 22/12/2016                       5
## 1870  151.2675 -33.91449 29/12/2016                       4
## 1871  151.2582 -33.92076 22/12/2016                      21
## 1872  151.2582 -33.92076 16/12/2016                    1200
## 1873  151.2582 -33.92076 29/12/2016                      66
## 1874  151.2582 -33.92076 12/12/2016                      NA
## 1875  151.2582 -33.92076 23/11/2016                      23
## 1876  151.2582 -33.92076 30/11/2016                      46
## 1877  151.2582 -33.92076 05/12/2016                      40
## 1878  151.2582 -33.92076 10/11/2016                      37
## 1879  151.2582 -33.92076 05/11/2016                       6
## 1880  151.2582 -33.92076 25/10/2016                       3
## 1881  151.2582 -33.92076 31/10/2016                       5
## 1882  151.2582 -33.92076 07/09/2016                       0
## 1883  151.2582 -33.92076 17/11/2016                      16
## 1884  151.2582 -33.92076 12/10/2016                       5
## 1885  151.2582 -33.92076 18/10/2016                       1
## 1886  151.2582 -33.92076 14/09/2016                      33
## 1887  151.2582 -33.92076 20/09/2016                       8
## 1888  151.2582 -33.92076 26/09/2016                       6
## 1889  151.2582 -33.92076 30/09/2016                       0
## 1890  151.2582 -33.92076 01/09/2016                       0
## 1891  151.2582 -33.92076 19/08/2016                       2
## 1892  151.2582 -33.92076 27/07/2016                       6
## 1893  151.2582 -33.92076 08/07/2016                      30
## 1894  151.2582 -33.92076 24/06/2016                       4
## 1895  151.2582 -33.92076 16/06/2016                       3
## 1896  151.2582 -33.92076 09/06/2016                     130
## 1897  151.2582 -33.92076 23/06/2016                       3
## 1898  151.2582 -33.92076 23/05/2016                      16
## 1899  151.2582 -33.92076 10/05/2016                      40
## 1900  151.2582 -33.92076 28/04/2016                       5
## 1901  151.2582 -33.92076 04/05/2016                       6
## 1902  151.2582 -33.92076 15/04/2016                      41
## 1903  151.2582 -33.92076 20/04/2016                      25
## 1904  151.2582 -33.92076 08/04/2016                      17
## 1905  151.2582 -33.92076 10/03/2016                      18
## 1906  151.2582 -33.92076 15/02/2016                      10
## 1907  151.2582 -33.92076 27/02/2016                      17
## 1908  151.2582 -33.92076 04/03/2016                       8
## 1909  151.2582 -33.92076 09/02/2016                      10
## 1910  151.2582 -33.92076 16/01/2016                      18
## 1911  151.2582 -33.92076 10/01/2016                       8
## 1912  151.2582 -33.92076 26/08/2016                       5
## 1913  151.2582 -33.92076 15/08/2016                       3
## 1914  151.2582 -33.92076 09/08/2016                      16
## 1915  151.2582 -33.92076 02/08/2016                       3
## 1916  151.2582 -33.92076 21/07/2016                      61
## 1917  151.2582 -33.92076 15/07/2016                       1
## 1918  151.2582 -33.92076 28/06/2016                       4
## 1919  151.2582 -33.92076 22/06/2016                       9
## 1920  151.2582 -33.92076 05/07/2016                      28
## 1921  151.2582 -33.92076 21/06/2016                     140
## 1922  151.2582 -33.92076 20/06/2016                      22
## 1923  151.2582 -33.92076 03/06/2016                      15
## 1924  151.2582 -33.92076 17/05/2016                       1
## 1925  151.2582 -33.92076 29/03/2016                      20
## 1926  151.2582 -33.92076 04/04/2016                     450
## 1927  151.2582 -33.92076 22/03/2016                      21
## 1928  151.2582 -33.92076 16/03/2016                      71
## 1929  151.2582 -33.92076 21/02/2016                     780
## 1930  151.2582 -33.92076 28/01/2016                      15
## 1931  151.2582 -33.92076 22/01/2016                      58
## 1932  151.2582 -33.92076 03/02/2016                      10
## 1933  151.2582 -33.92076 04/01/2016                      26
## 1934  151.2646 -33.91565 04/01/2016                      20
## 1935  151.2646 -33.91565 16/01/2016                       0
## 1936  151.2646 -33.91565 27/02/2016                       5
## 1937  151.2646 -33.91565 15/02/2016                       0
## 1938  151.2646 -33.91565 21/02/2016                     990
## 1939  151.2646 -33.91565 04/03/2016                       0
## 1940  151.2646 -33.91565 22/03/2016                      17
## 1941  151.2646 -33.91565 29/03/2016                       5
## 1942  151.2646 -33.91565 20/04/2016                       3
## 1943  151.2646 -33.91565 15/04/2016                       0
## 1944  151.2646 -33.91565 10/05/2016                       1
## 1945  151.2646 -33.91565 04/05/2016                       0
## 1946  151.2646 -33.91565 23/05/2016                       2
## 1947  151.2646 -33.91565 09/06/2016                     120
## 1948  151.2646 -33.91565 16/06/2016                       1
## 1949  151.2646 -33.91565 21/07/2016                       9
## 1950  151.2646 -33.91565 28/06/2016                       1
## 1951  151.2646 -33.91565 09/08/2016                      16
## 1952  151.2646 -33.91565 02/08/2016                       0
## 1953  151.2646 -33.91565 27/07/2016                       0
## 1954  151.2646 -33.91565 15/08/2016                       0
## 1955  151.2646 -33.91565 26/08/2016                       0
## 1956  151.2646 -33.91565 10/01/2016                       1
## 1957  151.2646 -33.91565 22/01/2016                      13
## 1958  151.2646 -33.91565 03/02/2016                       7
## 1959  151.2646 -33.91565 09/02/2016                       1
## 1960  151.2646 -33.91565 28/01/2016                       3
## 1961  151.2646 -33.91565 10/03/2016                      12
## 1962  151.2646 -33.91565 16/03/2016                      16
## 1963  151.2646 -33.91565 08/04/2016                       7
## 1964  151.2646 -33.91565 04/04/2016                      92
## 1965  151.2646 -33.91565 28/04/2016                       2
## 1966  151.2646 -33.91565 17/05/2016                       0
## 1967  151.2646 -33.91565 03/06/2016                       0
## 1968  151.2646 -33.91565 21/06/2016                      89
## 1969  151.2646 -33.91565 05/07/2016                       6
## 1970  151.2646 -33.91565 15/07/2016                       0
## 1971  151.2646 -33.91565 08/07/2016                      27
## 1972  151.2646 -33.91565 19/08/2016                       0
## 1973  151.2646 -33.91565 14/09/2016                       1
## 1974  151.2646 -33.91565 26/09/2016                       1
## 1975  151.2646 -33.91565 17/11/2016                       0
## 1976  151.2646 -33.91565 31/10/2016                       1
## 1977  151.2646 -33.91565 01/09/2016                       2
## 1978  151.2646 -33.91565 07/09/2016                       0
## 1979  151.2646 -33.91565 20/09/2016                       2
## 1980  151.2646 -33.91565 18/10/2016                       1
## 1981  151.2646 -33.91565 30/09/2016                       3
## 1982  151.2646 -33.91565 12/10/2016                       2
## 1983  151.2646 -33.91565 25/10/2016                       4
## 1984  151.2646 -33.91565 05/11/2016                       1
## 1985  151.2646 -33.91565 10/11/2016                       2
## 1986  151.2646 -33.91565 05/12/2016                       0
## 1987  151.2646 -33.91565 30/11/2016                       3
## 1988  151.2646 -33.91565 23/11/2016                       0
## 1989  151.2646 -33.91565 16/12/2016                     810
## 1990  151.2646 -33.91565 12/12/2016                       0
## 1991  151.2646 -33.91565 22/12/2016                       0
## 1992  151.2646 -33.91565 29/12/2016                       3
## 1993  151.2515 -33.98012 22/12/2016                       8
## 1994  151.2515 -33.98012 29/12/2016                      15
## 1995  151.2515 -33.98012 05/12/2016                       7
## 1996  151.2515 -33.98012 17/11/2016                       4
## 1997  151.2515 -33.98012 23/11/2016                       1
## 1998  151.2515 -33.98012 30/11/2016                       7
## 1999  151.2515 -33.98012 12/12/2016                       0
## 2000  151.2515 -33.98012 16/12/2016                     100
## 2001  151.2515 -33.98012 10/11/2016                       5
## 2002  151.2515 -33.98012 18/10/2016                       1
## 2003  151.2515 -33.98012 30/09/2016                       2
## 2004  151.2515 -33.98012 26/09/2016                       2
## 2005  151.2515 -33.98012 20/09/2016                      17
## 2006  151.2515 -33.98012 12/10/2016                       1
## 2007  151.2515 -33.98012 14/09/2016                     160
## 2008  151.2515 -33.98012 01/09/2016                       6
## 2009  151.2515 -33.98012 31/10/2016                      23
## 2010  151.2515 -33.98012 05/11/2016                       0
## 2011  151.2515 -33.98012 25/10/2016                       5
## 2012  151.2515 -33.98012 07/09/2016                       1
## 2013  151.2515 -33.98012 19/08/2016                       3
## 2014  151.2515 -33.98012 08/07/2016                       7
## 2015  151.2515 -33.98012 15/07/2016                       0
## 2016  151.2515 -33.98012 27/07/2016                       7
## 2017  151.2515 -33.98012 16/06/2016                       6
## 2018  151.2515 -33.98012 09/06/2016                      55
## 2019  151.2515 -33.98012 23/05/2016                       6
## 2020  151.2515 -33.98012 10/05/2016                      66
## 2021  151.2515 -33.98012 04/04/2016                     840
## 2022  151.2515 -33.98012 22/03/2016                      19
## 2023  151.2515 -33.98012 29/03/2016                       5
## 2024  151.2515 -33.98012 21/02/2016                      69
## 2025  151.2515 -33.98012 10/03/2016                       6
## 2026  151.2515 -33.98012 16/03/2016                      31
## 2027  151.2515 -33.98012 22/01/2016                      29
## 2028  151.2515 -33.98012 28/01/2016                       4
## 2029  151.2515 -33.98012 03/02/2016                       4
## 2030  151.2515 -33.98012 04/01/2016                       4
## 2031  151.2515 -33.98012 26/08/2016                       4
## 2032  151.2515 -33.98012 15/08/2016                       1
## 2033  151.2515 -33.98012 21/07/2016                      59
## 2034  151.2515 -33.98012 09/08/2016                       4
## 2035  151.2515 -33.98012 02/08/2016                       0
## 2036  151.2515 -33.98012 05/07/2016                      63
## 2037  151.2515 -33.98012 21/06/2016                       7
## 2038  151.2515 -33.98012 28/06/2016                       4
## 2039  151.2515 -33.98012 03/06/2016                      33
## 2040  151.2515 -33.98012 17/05/2016                       1
## 2041  151.2515 -33.98012 28/04/2016                       5
## 2042  151.2515 -33.98012 04/05/2016                      51
## 2043  151.2515 -33.98012 15/04/2016                      11
## 2044  151.2515 -33.98012 20/04/2016                       8
## 2045  151.2515 -33.98012 08/04/2016                       6
## 2046  151.2515 -33.98012 27/02/2016                       8
## 2047  151.2515 -33.98012 04/03/2016                       3
## 2048  151.2515 -33.98012 15/02/2016                       0
## 2049  151.2515 -33.98012 09/02/2016                      12
## 2050  151.2515 -33.98012 10/01/2016                      35
## 2051  151.2515 -33.98012 16/01/2016                       2
## 2052  151.2522 -33.96436 16/01/2016                       3
## 2053  151.2522 -33.96436 10/01/2016                      31
## 2054  151.2522 -33.96436 03/02/2016                       6
## 2055  151.2522 -33.96436 09/02/2016                      70
## 2056  151.2522 -33.96436 15/02/2016                       0
## 2057  151.2522 -33.96436 27/02/2016                       9
## 2058  151.2522 -33.96436 04/03/2016                      11
## 2059  151.2522 -33.96436 10/03/2016                     180
## 2060  151.2522 -33.96436 16/03/2016                     190
## 2061  151.2522 -33.96436 28/04/2016                      24
## 2062  151.2522 -33.96436 15/04/2016                      19
## 2063  151.2522 -33.96436 08/04/2016                      95
## 2064  151.2522 -33.96436 04/05/2016                      86
## 2065  151.2522 -33.96436 10/05/2016                      98
## 2066  151.2522 -33.96436 23/05/2016                      44
## 2067  151.2522 -33.96436 09/06/2016                      51
## 2068  151.2522 -33.96436 22/06/2016                      11
## 2069  151.2522 -33.96436 16/06/2016                       7
## 2070  151.2522 -33.96436 20/06/2016                     290
## 2071  151.2522 -33.96436 08/07/2016                      16
## 2072  151.2522 -33.96436 02/08/2016                      56
## 2073  151.2522 -33.96436 27/07/2016                      17
## 2074  151.2522 -33.96436 15/08/2016                       0
## 2075  151.2522 -33.96436 19/08/2016                      15
## 2076  151.2522 -33.96436 04/01/2016                       3
## 2077  151.2522 -33.96436 22/01/2016                     170
## 2078  151.2522 -33.96436 28/01/2016                       5
## 2079  151.2522 -33.96436 22/03/2016                      40
## 2080  151.2522 -33.96436 21/02/2016                      34
## 2081  151.2522 -33.96436 29/03/2016                      25
## 2082  151.2522 -33.96436 04/04/2016                     750
## 2083  151.2522 -33.96436 20/04/2016                       2
## 2084  151.2522 -33.96436 17/05/2016                       2
## 2085  151.2522 -33.96436 23/06/2016                      53
## 2086  151.2522 -33.96436 03/06/2016                    1200
## 2087  151.2522 -33.96436 21/07/2016                      69
## 2088  151.2522 -33.96436 15/07/2016                       1
## 2089  151.2522 -33.96436 28/06/2016                       7
## 2090  151.2522 -33.96436 05/07/2016                     190
## 2091  151.2522 -33.96436 24/06/2016                      26
## 2092  151.2522 -33.96436 21/06/2016                      30
## 2093  151.2522 -33.96436 09/08/2016                       1
## 2094  151.2522 -33.96436 07/09/2016                       2
## 2095  151.2522 -33.96436 26/08/2016                       7
## 2096  151.2522 -33.96436 25/10/2016                      12
## 2097  151.2522 -33.96436 05/11/2016                       1
## 2098  151.2522 -33.96436 10/11/2016                       7
## 2099  151.2522 -33.96436 01/09/2016                       4
## 2100  151.2522 -33.96436 20/09/2016                     130
## 2101  151.2522 -33.96436 14/09/2016                      10
## 2102  151.2522 -33.96436 12/10/2016                       0
## 2103  151.2522 -33.96436 18/10/2016                       9
## 2104  151.2522 -33.96436 26/09/2016                       0
## 2105  151.2522 -33.96436 30/09/2016                       6
## 2106  151.2522 -33.96436 31/10/2016                      22
## 2107  151.2522 -33.96436 30/11/2016                      67
## 2108  151.2522 -33.96436 17/11/2016                      45
## 2109  151.2522 -33.96436 23/11/2016                       1
## 2110  151.2522 -33.96436 12/12/2016                      53
## 2111  151.2522 -33.96436 16/12/2016                    1400
## 2112  151.2522 -33.96436 22/12/2016                       3
## 2113  151.2522 -33.96436 05/12/2016                       9
## 2114  151.2522 -33.96436 29/12/2016                       9
## 2115  151.2572 -33.94879 12/12/2016                       5
## 2116  151.2572 -33.94879 29/12/2016                      10
## 2117  151.2572 -33.94879 30/11/2016                       0
## 2118  151.2572 -33.94879 22/12/2016                       2
## 2119  151.2572 -33.94879 16/12/2016                     690
## 2120  151.2572 -33.94879 23/11/2016                       0
## 2121  151.2572 -33.94879 05/12/2016                      37
## 2122  151.2572 -33.94879 05/11/2016                       0
## 2123  151.2572 -33.94879 17/11/2016                       7
## 2124  151.2572 -33.94879 31/10/2016                       8
## 2125  151.2572 -33.94879 25/10/2016                       5
## 2126  151.2572 -33.94879 07/09/2016                       0
## 2127  151.2572 -33.94879 10/11/2016                       4
## 2128  151.2572 -33.94879 18/10/2016                       3
## 2129  151.2572 -33.94879 12/10/2016                       0
## 2130  151.2572 -33.94879 14/09/2016                      16
## 2131  151.2572 -33.94879 20/09/2016                       1
## 2132  151.2572 -33.94879 30/09/2016                       4
## 2133  151.2572 -33.94879 26/09/2016                       1
## 2134  151.2572 -33.94879 26/08/2016                       2
## 2135  151.2572 -33.94879 01/09/2016                       1
## 2136  151.2572 -33.94879 15/08/2016                       3
## 2137  151.2572 -33.94879 02/08/2016                       1
## 2138  151.2572 -33.94879 09/08/2016                      10
## 2139  151.2572 -33.94879 08/07/2016                       2
## 2140  151.2572 -33.94879 27/07/2016                       1
## 2141  151.2572 -33.94879 09/06/2016                     320
## 2142  151.2572 -33.94879 16/06/2016                       6
## 2143  151.2572 -33.94879 23/05/2016                       3
## 2144  151.2572 -33.94879 10/05/2016                      16
## 2145  151.2572 -33.94879 08/04/2016                       8
## 2146  151.2572 -33.94879 20/04/2016                       6
## 2147  151.2572 -33.94879 15/04/2016                       9
## 2148  151.2572 -33.94879 04/05/2016                       4
## 2149  151.2572 -33.94879 28/04/2016                       2
## 2150  151.2572 -33.94879 15/02/2016                       1
## 2151  151.2572 -33.94879 04/03/2016                       0
## 2152  151.2572 -33.94879 27/02/2016                       1
## 2153  151.2572 -33.94879 09/02/2016                       0
## 2154  151.2572 -33.94879 16/01/2016                       1
## 2155  151.2572 -33.94879 19/08/2016                       1
## 2156  151.2572 -33.94879 21/07/2016                      16
## 2157  151.2572 -33.94879 15/07/2016                       1
## 2158  151.2572 -33.94879 21/06/2016                      56
## 2159  151.2572 -33.94879 28/06/2016                      12
## 2160  151.2572 -33.94879 05/07/2016                       2
## 2161  151.2572 -33.94879 03/06/2016                      11
## 2162  151.2572 -33.94879 17/05/2016                      22
## 2163  151.2572 -33.94879 22/03/2016                      12
## 2164  151.2572 -33.94879 04/04/2016                     110
## 2165  151.2572 -33.94879 29/03/2016                      13
## 2166  151.2572 -33.94879 10/03/2016                      60
## 2167  151.2572 -33.94879 16/03/2016                       3
## 2168  151.2572 -33.94879 21/02/2016                      19
## 2169  151.2572 -33.94879 03/02/2016                       7
## 2170  151.2572 -33.94879 22/01/2016                      20
## 2171  151.2572 -33.94879 28/01/2016                       2
## 2172  151.2572 -33.94879 10/01/2016                       2
## 2173  151.2572 -33.94879 04/01/2016                      10
## 2174  151.2572 -33.95161 04/01/2016                       4
## 2175  151.2572 -33.95161 10/01/2016                       3
## 2176  151.2572 -33.95161 28/01/2016                       0
## 2177  151.2572 -33.95161 22/01/2016                      19
## 2178  151.2572 -33.95161 03/02/2016                       2
## 2179  151.2572 -33.95161 16/03/2016                      21
## 2180  151.2572 -33.95161 10/03/2016                      16
## 2181  151.2572 -33.95161 08/04/2016                       5
## 2182  151.2572 -33.95161 04/04/2016                       3
## 2183  151.2572 -33.95161 17/05/2016                       9
## 2184  151.2572 -33.95161 10/05/2016                      17
## 2185  151.2572 -33.95161 23/05/2016                       0
## 2186  151.2572 -33.95161 09/06/2016                     110
## 2187  151.2572 -33.95161 05/07/2016                       2
## 2188  151.2572 -33.95161 15/07/2016                       0
## 2189  151.2572 -33.95161 08/07/2016                       4
## 2190  151.2572 -33.95161 19/08/2016                       0
## 2191  151.2572 -33.95161 16/01/2016                       1
## 2192  151.2572 -33.95161 09/02/2016                       1
## 2193  151.2572 -33.95161 27/02/2016                       0
## 2194  151.2572 -33.95161 04/03/2016                       0
## 2195  151.2572 -33.95161 15/02/2016                       0
## 2196  151.2572 -33.95161 21/02/2016                       9
## 2197  151.2572 -33.95161 22/03/2016                      11
## 2198  151.2572 -33.95161 28/04/2016                       0
## 2199  151.2572 -33.95161 04/05/2016                      11
## 2200  151.2572 -33.95161 15/04/2016                       3
## 2201  151.2572 -33.95161 20/04/2016                       9
## 2202  151.2572 -33.95161 29/03/2016                      17
## 2203  151.2572 -33.95161 03/06/2016                       1
## 2204  151.2572 -33.95161 16/06/2016                      12
## 2205  151.2572 -33.95161 21/06/2016                      14
## 2206  151.2572 -33.95161 27/07/2016                       2
## 2207  151.2572 -33.95161 21/07/2016                      12
## 2208  151.2572 -33.95161 28/06/2016                       3
## 2209  151.2572 -33.95161 09/08/2016                      17
## 2210  151.2572 -33.95161 02/08/2016                       0
## 2211  151.2572 -33.95161 15/08/2016                       0
## 2212  151.2572 -33.95161 01/09/2016                       1
## 2213  151.2572 -33.95161 26/08/2016                       1
## 2214  151.2572 -33.95161 26/09/2016                       0
## 2215  151.2572 -33.95161 30/09/2016                       1
## 2216  151.2572 -33.95161 20/09/2016                       0
## 2217  151.2572 -33.95161 12/10/2016                       0
## 2218  151.2572 -33.95161 18/10/2016                       6
## 2219  151.2572 -33.95161 10/11/2016                       6
## 2220  151.2572 -33.95161 07/09/2016                       0
## 2221  151.2572 -33.95161 14/09/2016                      61
## 2222  151.2572 -33.95161 25/10/2016                       2
## 2223  151.2572 -33.95161 31/10/2016                       3
## 2224  151.2572 -33.95161 17/11/2016                       2
## 2225  151.2572 -33.95161 05/11/2016                       1
## 2226  151.2572 -33.95161 23/11/2016                       0
## 2227  151.2572 -33.95161 30/11/2016                       0
## 2228  151.2572 -33.95161 16/12/2016                     130
## 2229  151.2572 -33.95161 22/12/2016                       2
## 2230  151.2572 -33.95161 05/12/2016                      26
## 2231  151.2572 -33.95161 29/12/2016                      22
## 2232  151.2572 -33.95161 12/12/2016                      28
## 2233  151.2582 -33.95354 29/12/2016                      42
## 2234  151.2582 -33.95354 05/12/2016                       0
## 2235  151.2582 -33.95354 22/12/2016                      17
## 2236  151.2582 -33.95354 16/12/2016                     600
## 2237  151.2582 -33.95354 12/12/2016                      16
## 2238  151.2582 -33.95354 30/11/2016                       1
## 2239  151.2582 -33.95354 23/11/2016                       0
## 2240  151.2582 -33.95354 05/11/2016                       3
## 2241  151.2582 -33.95354 17/11/2016                      14
## 2242  151.2582 -33.95354 31/10/2016                       6
## 2243  151.2582 -33.95354 12/10/2016                       0
## 2244  151.2582 -33.95354 14/09/2016                     120
## 2245  151.2582 -33.95354 10/11/2016                      18
## 2246  151.2582 -33.95354 18/10/2016                       2
## 2247  151.2582 -33.95354 25/10/2016                       3
## 2248  151.2582 -33.95354 20/09/2016                       5
## 2249  151.2582 -33.95354 30/09/2016                      60
## 2250  151.2582 -33.95354 26/09/2016                       8
## 2251  151.2582 -33.95354 26/08/2016                       8
## 2252  151.2582 -33.95354 01/09/2016                       3
## 2253  151.2582 -33.95354 07/09/2016                       2
## 2254  151.2582 -33.95354 15/08/2016                       3
## 2255  151.2582 -33.95354 02/08/2016                       4
## 2256  151.2582 -33.95354 09/08/2016                       0
## 2257  151.2582 -33.95354 28/06/2016                       6
## 2258  151.2582 -33.95354 05/07/2016                       2
## 2259  151.2582 -33.95354 21/07/2016                      85
## 2260  151.2582 -33.95354 21/06/2016                      20
## 2261  151.2582 -33.95354 03/06/2016                    1600
## 2262  151.2582 -33.95354 17/05/2016                      16
## 2263  151.2582 -33.95354 29/03/2016                      32
## 2264  151.2582 -33.95354 04/04/2016                     200
## 2265  151.2582 -33.95354 20/04/2016                       9
## 2266  151.2582 -33.95354 04/05/2016                       7
## 2267  151.2582 -33.95354 22/03/2016                      23
## 2268  151.2582 -33.95354 21/02/2016                       8
## 2269  151.2582 -33.95354 15/02/2016                       0
## 2270  151.2582 -33.95354 04/03/2016                       0
## 2271  151.2582 -33.95354 27/02/2016                       2
## 2272  151.2582 -33.95354 04/01/2016                       2
## 2273  151.2582 -33.95354 19/08/2016                       3
## 2274  151.2582 -33.95354 27/07/2016                      29
## 2275  151.2582 -33.95354 08/07/2016                      10
## 2276  151.2582 -33.95354 15/07/2016                       0
## 2277  151.2582 -33.95354 16/06/2016                       8
## 2278  151.2582 -33.95354 09/06/2016                     110
## 2279  151.2582 -33.95354 23/05/2016                       3
## 2280  151.2582 -33.95354 10/05/2016                       9
## 2281  151.2582 -33.95354 08/04/2016                      14
## 2282  151.2582 -33.95354 15/04/2016                       2
## 2283  151.2582 -33.95354 28/04/2016                       3
## 2284  151.2582 -33.95354 10/03/2016                       2
## 2285  151.2582 -33.95354 16/03/2016                     210
## 2286  151.2582 -33.95354 03/02/2016                      12
## 2287  151.2582 -33.95354 09/02/2016                       5
## 2288  151.2582 -33.95354 22/01/2016                      65
## 2289  151.2582 -33.95354 28/01/2016                      12
## 2290  151.2582 -33.95354 10/01/2016                      35
## 2291  151.2582 -33.95354 16/01/2016                      21
## 2292  151.2776 -33.89151 16/01/2016                       7
## 2293  151.2776 -33.89151 22/01/2016                      19
## 2294  151.2776 -33.89151 10/01/2016                      63
## 2295  151.2776 -33.89151 03/02/2016                      47
## 2296  151.2776 -33.89151 09/02/2016                       8
## 2297  151.2776 -33.89151 16/03/2016                      17
## 2298  151.2776 -33.89151 10/03/2016                       8
## 2299  151.2776 -33.89151 27/02/2016                      10
## 2300  151.2776 -33.89151 15/02/2016                       1
## 2301  151.2776 -33.89151 28/04/2016                       0
## 2302  151.2776 -33.89151 15/04/2016                       3
## 2303  151.2776 -33.89151 08/04/2016                      13
## 2304  151.2776 -33.89151 10/05/2016                       2
## 2305  151.2776 -33.89151 23/05/2016                       4
## 2306  151.2776 -33.89151 09/06/2016                      24
## 2307  151.2776 -33.89151 16/06/2016                       1
## 2308  151.2776 -33.89151 05/07/2016                       3
## 2309  151.2776 -33.89151 15/07/2016                       1
## 2310  151.2776 -33.89151 08/07/2016                      82
## 2311  151.2776 -33.89151 19/08/2016                       0
## 2312  151.2776 -33.89151 04/01/2016                      33
## 2313  151.2776 -33.89151 28/01/2016                      21
## 2314  151.2776 -33.89151 04/03/2016                       0
## 2315  151.2776 -33.89151 21/02/2016                     180
## 2316  151.2776 -33.89151 22/03/2016                      17
## 2317  151.2776 -33.89151 04/05/2016                       0
## 2318  151.2776 -33.89151 20/04/2016                      12
## 2319  151.2776 -33.89151 29/03/2016                      10
## 2320  151.2776 -33.89151 04/04/2016                     130
## 2321  151.2776 -33.89151 17/05/2016                       1
## 2322  151.2776 -33.89151 03/06/2016                       4
## 2323  151.2776 -33.89151 21/06/2016                     110
## 2324  151.2776 -33.89151 27/07/2016                       0
## 2325  151.2776 -33.89151 02/08/2016                       0
## 2326  151.2776 -33.89151 21/07/2016                      24
## 2327  151.2776 -33.89151 28/06/2016                      43
## 2328  151.2776 -33.89151 09/08/2016                       4
## 2329  151.2776 -33.89151 15/08/2016                      14
## 2330  151.2776 -33.89151 26/08/2016                       1
## 2331  151.2776 -33.89151 01/09/2016                       1
## 2332  151.2776 -33.89151 07/09/2016                       0
## 2333  151.2776 -33.89151 30/09/2016                       3
## 2334  151.2776 -33.89151 20/09/2016                       4
## 2335  151.2776 -33.89151 25/10/2016                      21
## 2336  151.2776 -33.89151 10/11/2016                      18
## 2337  151.2776 -33.89151 05/11/2016                      34
## 2338  151.2776 -33.89151 14/09/2016                       5
## 2339  151.2776 -33.89151 12/10/2016                       0
## 2340  151.2776 -33.89151 26/09/2016                       6
## 2341  151.2776 -33.89151 31/10/2016                       4
## 2342  151.2776 -33.89151 18/10/2016                       2
## 2343  151.2776 -33.89151 17/11/2016                       0
## 2344  151.2776 -33.89151 23/11/2016                       0
## 2345  151.2776 -33.89151 30/11/2016                       6
## 2346  151.2776 -33.89151 12/12/2016                       0
## 2347  151.2776 -33.89151 16/12/2016                     110
## 2348  151.2776 -33.89151 22/12/2016                       6
## 2349  151.2776 -33.89151 05/12/2016                       0
## 2350  151.2776 -33.89151 29/12/2016                       5
## 2351  151.2686 -33.90307 29/12/2016                       8
## 2352  151.2686 -33.90307 22/12/2016                       2
## 2353  151.2686 -33.90307 16/12/2016                     840
## 2354  151.2686 -33.90307 05/12/2016                      24
## 2355  151.2686 -33.90307 23/11/2016                      15
## 2356  151.2686 -33.90307 12/12/2016                       2
## 2357  151.2686 -33.90307 30/11/2016                      25
## 2358  151.2686 -33.90307 10/11/2016                      10
## 2359  151.2686 -33.90307 12/10/2016                       6
## 2360  151.2686 -33.90307 18/10/2016                       7
## 2361  151.2686 -33.90307 20/09/2016                       1
## 2362  151.2686 -33.90307 26/09/2016                       3
## 2363  151.2686 -33.90307 30/09/2016                       2
## 2364  151.2686 -33.90307 14/09/2016                      17
## 2365  151.2686 -33.90307 05/11/2016                       0
## 2366  151.2686 -33.90307 17/11/2016                       2
## 2367  151.2686 -33.90307 01/09/2016                       1
## 2368  151.2686 -33.90307 25/10/2016                       4
## 2369  151.2686 -33.90307 31/10/2016                       5
## 2370  151.2686 -33.90307 26/08/2016                       0
## 2371  151.2686 -33.90307 07/09/2016                       1
## 2372  151.2686 -33.90307 21/07/2016                      31
## 2373  151.2686 -33.90307 09/08/2016                      10
## 2374  151.2686 -33.90307 28/06/2016                      61
## 2375  151.2686 -33.90307 05/07/2016                       5
## 2376  151.2686 -33.90307 15/07/2016                       2
## 2377  151.2686 -33.90307 21/06/2016                      84
## 2378  151.2686 -33.90307 03/06/2016                       5
## 2379  151.2686 -33.90307 17/05/2016                      10
## 2380  151.2686 -33.90307 29/03/2016                       7
## 2381  151.2686 -33.90307 04/04/2016                     660
## 2382  151.2686 -33.90307 22/03/2016                      29
## 2383  151.2686 -33.90307 16/03/2016                      62
## 2384  151.2686 -33.90307 21/02/2016                    1100
## 2385  151.2686 -33.90307 10/03/2016                       0
## 2386  151.2686 -33.90307 28/01/2016                      21
## 2387  151.2686 -33.90307 03/02/2016                       0
## 2388  151.2686 -33.90307 04/01/2016                      83
## 2389  151.2686 -33.90307 10/01/2016                       5
## 2390  151.2686 -33.90307 22/01/2016                      36
## 2391  151.2686 -33.90307 19/08/2016                       0
## 2392  151.2686 -33.90307 02/08/2016                       3
## 2393  151.2686 -33.90307 27/07/2016                       3
## 2394  151.2686 -33.90307 15/08/2016                       1
## 2395  151.2686 -33.90307 08/07/2016                      25
## 2396  151.2686 -33.90307 09/06/2016                      74
## 2397  151.2686 -33.90307 16/06/2016                       1
## 2398  151.2686 -33.90307 23/05/2016                       3
## 2399  151.2686 -33.90307 04/05/2016                       0
## 2400  151.2686 -33.90307 10/05/2016                       6
## 2401  151.2686 -33.90307 08/04/2016                       2
## 2402  151.2686 -33.90307 28/04/2016                     250
## 2403  151.2686 -33.90307 15/04/2016                      12
## 2404  151.2686 -33.90307 20/04/2016                       3
## 2405  151.2686 -33.90307 15/02/2016                       2
## 2406  151.2686 -33.90307 27/02/2016                       6
## 2407  151.2686 -33.90307 04/03/2016                      30
## 2408  151.2686 -33.90307 09/02/2016                       7
## 2409  151.2686 -33.90307 16/01/2016                       4
## 2410  151.2706 -33.90056 16/01/2016                       5
## 2411  151.2706 -33.90056 10/01/2016                      10
## 2412  151.2706 -33.90056 09/02/2016                       0
## 2413  151.2706 -33.90056 04/03/2016                       0
## 2414  151.2706 -33.90056 10/03/2016                       5
## 2415  151.2706 -33.90056 27/02/2016                       5
## 2416  151.2706 -33.90056 15/02/2016                       3
## 2417  151.2706 -33.90056 20/04/2016                       8
## 2418  151.2706 -33.90056 28/04/2016                       8
## 2419  151.2706 -33.90056 15/04/2016                      10
## 2420  151.2706 -33.90056 08/04/2016                       2
## 2421  151.2706 -33.90056 04/05/2016                       0
## 2422  151.2706 -33.90056 10/05/2016                       5
## 2423  151.2706 -33.90056 23/05/2016                       2
## 2424  151.2706 -33.90056 16/06/2016                       2
## 2425  151.2706 -33.90056 09/06/2016                      54
## 2426  151.2706 -33.90056 08/07/2016                      34
## 2427  151.2706 -33.90056 27/07/2016                       3
## 2428  151.2706 -33.90056 04/01/2016                      92
## 2429  151.2706 -33.90056 01/09/2016                       4
## 2430  151.2706 -33.90056 19/08/2016                       0
## 2431  151.2706 -33.90056 22/01/2016                      31
## 2432  151.2706 -33.90056 03/02/2016                      14
## 2433  151.2706 -33.90056 28/01/2016                      28
## 2434  151.2706 -33.90056 21/02/2016                    1000
## 2435  151.2706 -33.90056 16/03/2016                      22
## 2436  151.2706 -33.90056 22/03/2016                      29
## 2437  151.2706 -33.90056 04/04/2016                     870
## 2438  151.2706 -33.90056 29/03/2016                       2
## 2439  151.2706 -33.90056 03/06/2016                       3
## 2440  151.2706 -33.90056 17/05/2016                       1
## 2441  151.2706 -33.90056 21/06/2016                     140
## 2442  151.2706 -33.90056 15/07/2016                       1
## 2443  151.2706 -33.90056 21/07/2016                      63
## 2444  151.2706 -33.90056 02/08/2016                       8
## 2445  151.2706 -33.90056 05/07/2016                      37
## 2446  151.2706 -33.90056 28/06/2016                      57
## 2447  151.2706 -33.90056 09/08/2016                      16
## 2448  151.2706 -33.90056 26/08/2016                       4
## 2449  151.2706 -33.90056 15/08/2016                       0
## 2450  151.2706 -33.90056 07/09/2016                       0
## 2451  151.2706 -33.90056 31/10/2016                       5
## 2452  151.2706 -33.90056 25/10/2016                       6
## 2453  151.2706 -33.90056 10/11/2016                      10
## 2454  151.2706 -33.90056 20/09/2016                       0
## 2455  151.2706 -33.90056 14/09/2016                      12
## 2456  151.2706 -33.90056 12/10/2016                       6
## 2457  151.2706 -33.90056 26/09/2016                       2
## 2458  151.2706 -33.90056 30/09/2016                       5
## 2459  151.2706 -33.90056 18/10/2016                       2
## 2460  151.2706 -33.90056 17/11/2016                       5
## 2461  151.2706 -33.90056 12/12/2016                       3
## 2462  151.2706 -33.90056 30/11/2016                       4
## 2463  151.2706 -33.90056 23/11/2016                       2
## 2464  151.2706 -33.90056 16/12/2016                     270
## 2465  151.2706 -33.90056 22/12/2016                       4
## 2466  151.2706 -33.90056 29/12/2016                       1
## 2467  151.2706 -33.90056 05/12/2016                       0
## 2468  151.2675 -33.91449 23/01/2017                       3
## 2469  151.2675 -33.91449 30/01/2017                       8
## 2470  151.2675 -33.91449 04/02/2017                       2
## 2471  151.2675 -33.91449 15/02/2017                      12
## 2472  151.2675 -33.91449 21/02/2017                       3
## 2473  151.2675 -33.91449 27/10/2017                      24
## 2474  151.2675 -33.91449 09/11/2017                       1
## 2475  151.2675 -33.91449 08/12/2017                       3
## 2476  151.2675 -33.91449 20/12/2017                       2
## 2477  151.2675 -33.91449 05/01/2017                       1
## 2478  151.2675 -33.91449 11/01/2017                       5
## 2479  151.2675 -33.91449 17/01/2017                       2
## 2480  151.2675 -33.91449 09/02/2017                      10
## 2481  151.2675 -33.91449 09/03/2017                       7
## 2482  151.2675 -33.91449 07/04/2017                      16
## 2483  151.2675 -33.91449 21/04/2017                       6
## 2484  151.2675 -33.91449 03/11/2017                       8
## 2485  151.2675 -33.91449 15/11/2017                       2
## 2486  151.2675 -33.91449 21/11/2017                       0
## 2487  151.2675 -33.91449 27/11/2017                       3
## 2488  151.2675 -33.91449 04/12/2017                       9
## 2489  151.2675 -33.91449 14/12/2017                       2
## 2490  151.2675 -33.91449 28/12/2017                       0
## 2491  151.2675 -33.91449 27/02/2017                      28
## 2492  151.2675 -33.91449 03/03/2017                      30
## 2493  151.2675 -33.91449 16/03/2017                      15
## 2494  151.2675 -33.91449 22/03/2017                     100
## 2495  151.2675 -33.91449 28/03/2017                       4
## 2496  151.2675 -33.91449 03/04/2017                      32
## 2497  151.2675 -33.91449 13/04/2017                       0
## 2498  151.2675 -33.91449 28/04/2017                       5
## 2499  151.2675 -33.91449 10/05/2017                       0
## 2500  151.2675 -33.91449 16/05/2017                       2
## 2501  151.2675 -33.91449 22/05/2017                      12
## 2502  151.2675 -33.91449 08/06/2017                      68
## 2503  151.2675 -33.91449 30/06/2017                       1
## 2504  151.2675 -33.91449 11/07/2017                       0
## 2505  151.2675 -33.91449 28/07/2017                       7
## 2506  151.2675 -33.91449 09/08/2017                       2
## 2507  151.2675 -33.91449 29/08/2017                       0
## 2508  151.2675 -33.91449 01/09/2017                       3
## 2509  151.2675 -33.91449 07/09/2017                       4
## 2510  151.2675 -33.91449 19/09/2017                       0
## 2511  151.2675 -33.91449 04/05/2017                       5
## 2512  151.2675 -33.91449 29/05/2017                       0
## 2513  151.2675 -33.91449 01/06/2017                       4
## 2514  151.2675 -33.91449 14/06/2017                       5
## 2515  151.2675 -33.91449 20/06/2017                       9
## 2516  151.2675 -33.91449 26/06/2017                       0
## 2517  151.2675 -33.91449 17/07/2017                       1
## 2518  151.2675 -33.91449 24/07/2017                       1
## 2519  151.2675 -33.91449 03/08/2017                       1
## 2520  151.2675 -33.91449 16/08/2017                       1
## 2521  151.2675 -33.91449 22/08/2017                       4
## 2522  151.2675 -33.91449 13/09/2017                       0
## 2523  151.2675 -33.91449 25/09/2017                       1
## 2524  151.2675 -33.91449 29/09/2017                       0
## 2525  151.2675 -33.91449 05/10/2017                       0
## 2526  151.2675 -33.91449 11/10/2017                       3
## 2527  151.2675 -33.91449 17/10/2017                       0
## 2528  151.2675 -33.91449 23/10/2017                       7
## 2529  151.2582 -33.92076 23/10/2017                      11
## 2530  151.2582 -33.92076 17/10/2017                       4
## 2531  151.2582 -33.92076 11/10/2017                       2
## 2532  151.2582 -33.92076 05/10/2017                       5
## 2533  151.2582 -33.92076 25/09/2017                       0
## 2534  151.2582 -33.92076 19/09/2017                       1
## 2535  151.2582 -33.92076 13/09/2017                       1
## 2536  151.2582 -33.92076 01/09/2017                       1
## 2537  151.2582 -33.92076 03/08/2017                      12
## 2538  151.2582 -33.92076 17/07/2017                       6
## 2539  151.2582 -33.92076 14/06/2017                      13
## 2540  151.2582 -33.92076 20/06/2017                      30
## 2541  151.2582 -33.92076 01/06/2017                       4
## 2542  151.2582 -33.92076 08/06/2017                      76
## 2543  151.2582 -33.92076 29/05/2017                      10
## 2544  151.2582 -33.92076 10/05/2017                      20
## 2545  151.2582 -33.92076 16/05/2017                      61
## 2546  151.2582 -33.92076 22/05/2017                      60
## 2547  151.2582 -33.92076 04/05/2017                      37
## 2548  151.2582 -33.92076 09/05/2017                       4
## 2549  151.2582 -33.92076 28/04/2017                       4
## 2550  151.2582 -33.92076 29/09/2017                       0
## 2551  151.2582 -33.92076 07/09/2017                       3
## 2552  151.2582 -33.92076 29/08/2017                       1
## 2553  151.2582 -33.92076 16/08/2017                       1
## 2554  151.2582 -33.92076 22/08/2017                       2
## 2555  151.2582 -33.92076 09/08/2017                       5
## 2556  151.2582 -33.92076 28/07/2017                       7
## 2557  151.2582 -33.92076 24/07/2017                      96
## 2558  151.2582 -33.92076 26/06/2017                       6
## 2559  151.2582 -33.92076 30/06/2017                       2
## 2560  151.2582 -33.92076 11/07/2017                       0
## 2561  151.2582 -33.92076 13/04/2017                      20
## 2562  151.2582 -33.92076 21/04/2017                       2
## 2563  151.2582 -33.92076 03/04/2017                      80
## 2564  151.2582 -33.92076 07/04/2017                      24
## 2565  151.2582 -33.92076 28/03/2017                      10
## 2566  151.2582 -33.92076 22/03/2017                      14
## 2567  151.2582 -33.92076 03/03/2017                     140
## 2568  151.2582 -33.92076 09/03/2017                      12
## 2569  151.2582 -33.92076 20/12/2017                       4
## 2570  151.2582 -33.92076 08/12/2017                       5
## 2571  151.2582 -33.92076 04/12/2017                      69
## 2572  151.2582 -33.92076 21/11/2017                      11
## 2573  151.2582 -33.92076 03/11/2017                       8
## 2574  151.2582 -33.92076 09/11/2017                      18
## 2575  151.2582 -33.92076 15/11/2017                       0
## 2576  151.2582 -33.92076 16/03/2017                      30
## 2577  151.2582 -33.92076 21/02/2017                       7
## 2578  151.2582 -33.92076 27/02/2017                      38
## 2579  151.2582 -33.92076 11/01/2017                      42
## 2580  151.2582 -33.92076 05/01/2017                      49
## 2581  151.2582 -33.92076 28/12/2017                       6
## 2582  151.2582 -33.92076 17/01/2017                      16
## 2583  151.2582 -33.92076 30/01/2017                      42
## 2584  151.2582 -33.92076 14/12/2017                      12
## 2585  151.2582 -33.92076 27/11/2017                       3
## 2586  151.2582 -33.92076 27/10/2017                      60
## 2587  151.2582 -33.92076 09/02/2017                      16
## 2588  151.2582 -33.92076 15/02/2017                      19
## 2589  151.2582 -33.92076 04/02/2017                      39
## 2590  151.2582 -33.92076 23/01/2017                       5
## 2591  151.2646 -33.91565 23/01/2017                       0
## 2592  151.2646 -33.91565 09/02/2017                      18
## 2593  151.2646 -33.91565 04/02/2017                       3
## 2594  151.2646 -33.91565 27/10/2017                      20
## 2595  151.2646 -33.91565 15/02/2017                      12
## 2596  151.2646 -33.91565 09/11/2017                       4
## 2597  151.2646 -33.91565 20/12/2017                       0
## 2598  151.2646 -33.91565 30/01/2017                       1
## 2599  151.2646 -33.91565 28/12/2017                       2
## 2600  151.2646 -33.91565 05/01/2017                       2
## 2601  151.2646 -33.91565 17/01/2017                       0
## 2602  151.2646 -33.91565 11/01/2017                     260
## 2603  151.2646 -33.91565 21/02/2017                       0
## 2604  151.2646 -33.91565 09/03/2017                       4
## 2605  151.2646 -33.91565 16/03/2017                      19
## 2606  151.2646 -33.91565 07/04/2017                      40
## 2607  151.2646 -33.91565 03/11/2017                       1
## 2608  151.2646 -33.91565 21/04/2017                       2
## 2609  151.2646 -33.91565 21/11/2017                       1
## 2610  151.2646 -33.91565 15/11/2017                       1
## 2611  151.2646 -33.91565 04/12/2017                      42
## 2612  151.2646 -33.91565 27/11/2017                       1
## 2613  151.2646 -33.91565 14/12/2017                       4
## 2614  151.2646 -33.91565 08/12/2017                       9
## 2615  151.2646 -33.91565 03/03/2017                      56
## 2616  151.2646 -33.91565 27/02/2017                     150
## 2617  151.2646 -33.91565 22/03/2017                       6
## 2618  151.2646 -33.91565 28/03/2017                       8
## 2619  151.2646 -33.91565 13/04/2017                       9
## 2620  151.2646 -33.91565 03/04/2017                      50
## 2621  151.2646 -33.91565 28/04/2017                       9
## 2622  151.2646 -33.91565 22/05/2017                       4
## 2623  151.2646 -33.91565 30/06/2017                       3
## 2624  151.2646 -33.91565 08/06/2017                      22
## 2625  151.2646 -33.91565 24/07/2017                       3
## 2626  151.2646 -33.91565 11/07/2017                       0
## 2627  151.2646 -33.91565 28/07/2017                       0
## 2628  151.2646 -33.91565 09/08/2017                       2
## 2629  151.2646 -33.91565 29/08/2017                       6
## 2630  151.2646 -33.91565 07/09/2017                       5
## 2631  151.2646 -33.91565 10/05/2017                       2
## 2632  151.2646 -33.91565 04/05/2017                       2
## 2633  151.2646 -33.91565 29/09/2017                       0
## 2634  151.2646 -33.91565 29/05/2017                       2
## 2635  151.2646 -33.91565 01/06/2017                       1
## 2636  151.2646 -33.91565 14/06/2017                      12
## 2637  151.2646 -33.91565 16/05/2017                       0
## 2638  151.2646 -33.91565 20/06/2017                       2
## 2639  151.2646 -33.91565 17/07/2017                       0
## 2640  151.2646 -33.91565 26/06/2017                       2
## 2641  151.2646 -33.91565 03/08/2017                       3
## 2642  151.2646 -33.91565 16/08/2017                       0
## 2643  151.2646 -33.91565 22/08/2017                       1
## 2644  151.2646 -33.91565 13/09/2017                       3
## 2645  151.2646 -33.91565 25/09/2017                       0
## 2646  151.2646 -33.91565 01/09/2017                       1
## 2647  151.2646 -33.91565 19/09/2017                       2
## 2648  151.2646 -33.91565 05/10/2017                       1
## 2649  151.2646 -33.91565 11/10/2017                       1
## 2650  151.2646 -33.91565 17/10/2017                       1
## 2651  151.2646 -33.91565 23/10/2017                      18
## 2652  151.2515 -33.98012 23/10/2017                       6
## 2653  151.2515 -33.98012 05/10/2017                       1
## 2654  151.2515 -33.98012 25/09/2017                       2
## 2655  151.2515 -33.98012 29/09/2017                       0
## 2656  151.2515 -33.98012 13/09/2017                       2
## 2657  151.2515 -33.98012 19/09/2017                       0
## 2658  151.2515 -33.98012 16/08/2017                       0
## 2659  151.2515 -33.98012 22/08/2017                       0
## 2660  151.2515 -33.98012 03/08/2017                      45
## 2661  151.2515 -33.98012 20/06/2017                       3
## 2662  151.2515 -33.98012 26/06/2017                      10
## 2663  151.2515 -33.98012 17/07/2017                       0
## 2664  151.2515 -33.98012 11/07/2017                       1
## 2665  151.2515 -33.98012 14/06/2017                      14
## 2666  151.2515 -33.98012 01/06/2017                       3
## 2667  151.2515 -33.98012 11/10/2017                       1
## 2668  151.2515 -33.98012 17/10/2017                       0
## 2669  151.2515 -33.98012 21/04/2017                       0
## 2670  151.2515 -33.98012 29/08/2017                       0
## 2671  151.2515 -33.98012 01/09/2017                       0
## 2672  151.2515 -33.98012 07/09/2017                      16
## 2673  151.2515 -33.98012 09/08/2017                       4
## 2674  151.2515 -33.98012 28/07/2017                       6
## 2675  151.2515 -33.98012 24/07/2017                       3
## 2676  151.2515 -33.98012 08/06/2017                      20
## 2677  151.2515 -33.98012 29/05/2017                       1
## 2678  151.2515 -33.98012 30/06/2017                       2
## 2679  151.2515 -33.98012 22/05/2017                       8
## 2680  151.2515 -33.98012 16/05/2017                       8
## 2681  151.2515 -33.98012 10/05/2017                       3
## 2682  151.2515 -33.98012 28/04/2017                       9
## 2683  151.2515 -33.98012 13/04/2017                      22
## 2684  151.2515 -33.98012 04/05/2017                       7
## 2685  151.2515 -33.98012 16/03/2017                      48
## 2686  151.2515 -33.98012 27/02/2017                     270
## 2687  151.2515 -33.98012 28/12/2017                       5
## 2688  151.2515 -33.98012 14/12/2017                       0
## 2689  151.2515 -33.98012 27/11/2017                       2
## 2690  151.2515 -33.98012 21/11/2017                       7
## 2691  151.2515 -33.98012 07/04/2017                       3
## 2692  151.2515 -33.98012 28/03/2017                      23
## 2693  151.2515 -33.98012 03/04/2017                       5
## 2694  151.2515 -33.98012 09/03/2017                       1
## 2695  151.2515 -33.98012 22/03/2017                      46
## 2696  151.2515 -33.98012 27/10/2017                      48
## 2697  151.2515 -33.98012 03/03/2017                     200
## 2698  151.2515 -33.98012 09/02/2017                      34
## 2699  151.2515 -33.98012 04/02/2017                       9
## 2700  151.2515 -33.98012 20/12/2017                      46
## 2701  151.2515 -33.98012 23/01/2017                       7
## 2702  151.2515 -33.98012 17/01/2017                       6
## 2703  151.2515 -33.98012 08/12/2017                       3
## 2704  151.2515 -33.98012 04/12/2017                      56
## 2705  151.2515 -33.98012 15/11/2017                       2
## 2706  151.2515 -33.98012 09/11/2017                       1
## 2707  151.2515 -33.98012 03/11/2017                      23
## 2708  151.2515 -33.98012 21/02/2017                       2
## 2709  151.2515 -33.98012 15/02/2017                       6
## 2710  151.2515 -33.98012 30/01/2017                       7
## 2711  151.2515 -33.98012 05/01/2017                       9
## 2712  151.2515 -33.98012 11/01/2017                      47
## 2713  151.2522 -33.96436 11/01/2017                     310
## 2714  151.2522 -33.96436 17/01/2017                       7
## 2715  151.2522 -33.96436 05/01/2017                       0
## 2716  151.2522 -33.96436 30/01/2017                      30
## 2717  151.2522 -33.96436 21/02/2017                       2
## 2718  151.2522 -33.96436 03/11/2017                      21
## 2719  151.2522 -33.96436 09/11/2017                       4
## 2720  151.2522 -33.96436 21/11/2017                      32
## 2721  151.2522 -33.96436 15/11/2017                       5
## 2722  151.2522 -33.96436 04/12/2017                     180
## 2723  151.2522 -33.96436 20/12/2017                      49
## 2724  151.2522 -33.96436 08/12/2017                       7
## 2725  151.2522 -33.96436 23/01/2017                       0
## 2726  151.2522 -33.96436 04/02/2017                       1
## 2727  151.2522 -33.96436 09/02/2017                      11
## 2728  151.2522 -33.96436 25/10/2017                      42
## 2729  151.2522 -33.96436 15/02/2017                       9
## 2730  151.2522 -33.96436 27/10/2017                     170
## 2731  151.2522 -33.96436 03/03/2017                     230
## 2732  151.2522 -33.96436 22/03/2017                      46
## 2733  151.2522 -33.96436 28/03/2017                     900
## 2734  151.2522 -33.96436 07/04/2017                      27
## 2735  151.2522 -33.96436 03/04/2017                      14
## 2736  151.2522 -33.96436 27/11/2017                       1
## 2737  151.2522 -33.96436 13/04/2017                      16
## 2738  151.2522 -33.96436 14/12/2017                      21
## 2739  151.2522 -33.96436 28/12/2017                       1
## 2740  151.2522 -33.96436 27/02/2017                     300
## 2741  151.2522 -33.96436 16/03/2017                       2
## 2742  151.2522 -33.96436 09/03/2017                      29
## 2743  151.2522 -33.96436 04/05/2017                      25
## 2744  151.2522 -33.96436 28/04/2017                      27
## 2745  151.2522 -33.96436 10/05/2017                      29
## 2746  151.2522 -33.96436 22/05/2017                      60
## 2747  151.2522 -33.96436 16/05/2017                      26
## 2748  151.2522 -33.96436 30/06/2017                      11
## 2749  151.2522 -33.96436 14/06/2017                      16
## 2750  151.2522 -33.96436 29/05/2017                      50
## 2751  151.2522 -33.96436 01/06/2017                      20
## 2752  151.2522 -33.96436 08/06/2017                      60
## 2753  151.2522 -33.96436 28/07/2017                      33
## 2754  151.2522 -33.96436 09/08/2017                      11
## 2755  151.2522 -33.96436 29/08/2017                       0
## 2756  151.2522 -33.96436 07/09/2017                       3
## 2757  151.2522 -33.96436 19/09/2017                       0
## 2758  151.2522 -33.96436 01/09/2017                       5
## 2759  151.2522 -33.96436 17/10/2017                       0
## 2760  151.2522 -33.96436 23/10/2017                      10
## 2761  151.2522 -33.96436 21/04/2017                       4
## 2762  151.2522 -33.96436 11/10/2017                      10
## 2763  151.2522 -33.96436 05/10/2017                       3
## 2764  151.2522 -33.96436 20/06/2017                     110
## 2765  151.2522 -33.96436 24/07/2017                      15
## 2766  151.2522 -33.96436 17/07/2017                      12
## 2767  151.2522 -33.96436 11/07/2017                      17
## 2768  151.2522 -33.96436 26/06/2017                      32
## 2769  151.2522 -33.96436 03/08/2017                      17
## 2770  151.2522 -33.96436 22/08/2017                       2
## 2771  151.2522 -33.96436 16/08/2017                       4
## 2772  151.2522 -33.96436 13/09/2017                       0
## 2773  151.2522 -33.96436 29/09/2017                       0
## 2774  151.2522 -33.96436 25/09/2017                       6
## 2775  151.2572 -33.94879 11/10/2017                       2
## 2776  151.2572 -33.94879 29/08/2017                       0
## 2777  151.2572 -33.94879 07/09/2017                       2
## 2778  151.2572 -33.94879 01/09/2017                       0
## 2779  151.2572 -33.94879 09/08/2017                       0
## 2780  151.2572 -33.94879 28/07/2017                      13
## 2781  151.2572 -33.94879 17/10/2017                       2
## 2782  151.2572 -33.94879 11/07/2017                       0
## 2783  151.2572 -33.94879 30/06/2017                       3
## 2784  151.2572 -33.94879 24/07/2017                      12
## 2785  151.2572 -33.94879 08/06/2017                      12
## 2786  151.2572 -33.94879 29/05/2017                       7
## 2787  151.2572 -33.94879 10/05/2017                       0
## 2788  151.2572 -33.94879 22/05/2017                     210
## 2789  151.2572 -33.94879 16/05/2017                       5
## 2790  151.2572 -33.94879 05/10/2017                       3
## 2791  151.2572 -33.94879 23/10/2017                       3
## 2792  151.2572 -33.94879 28/04/2017                       0
## 2793  151.2572 -33.94879 04/05/2017                      41
## 2794  151.2572 -33.94879 13/09/2017                       5
## 2795  151.2572 -33.94879 25/09/2017                       1
## 2796  151.2572 -33.94879 29/09/2017                       0
## 2797  151.2572 -33.94879 19/09/2017                       9
## 2798  151.2572 -33.94879 22/08/2017                       0
## 2799  151.2572 -33.94879 16/08/2017                       3
## 2800  151.2572 -33.94879 17/07/2017                       4
## 2801  151.2572 -33.94879 03/08/2017                       6
## 2802  151.2572 -33.94879 14/06/2017                       6
## 2803  151.2572 -33.94879 01/06/2017                       0
## 2804  151.2572 -33.94879 20/06/2017                       7
## 2805  151.2572 -33.94879 26/06/2017                       4
## 2806  151.2572 -33.94879 28/03/2017                      11
## 2807  151.2572 -33.94879 22/03/2017                      28
## 2808  151.2572 -33.94879 21/04/2017                       0
## 2809  151.2572 -33.94879 07/04/2017                       6
## 2810  151.2572 -33.94879 03/04/2017                      20
## 2811  151.2572 -33.94879 03/03/2017                      73
## 2812  151.2572 -33.94879 09/03/2017                       1
## 2813  151.2572 -33.94879 08/12/2017                       1
## 2814  151.2572 -33.94879 20/12/2017                      27
## 2815  151.2572 -33.94879 03/11/2017                      16
## 2816  151.2572 -33.94879 15/11/2017                       0
## 2817  151.2572 -33.94879 09/11/2017                       0
## 2818  151.2572 -33.94879 04/12/2017                      20
## 2819  151.2572 -33.94879 13/04/2017                      10
## 2820  151.2572 -33.94879 16/03/2017                      18
## 2821  151.2572 -33.94879 27/02/2017                      14
## 2822  151.2572 -33.94879 15/02/2017                       1
## 2823  151.2572 -33.94879 21/02/2017                       1
## 2824  151.2572 -33.94879 30/01/2017                       0
## 2825  151.2572 -33.94879 28/12/2017                       6
## 2826  151.2572 -33.94879 05/01/2017                       7
## 2827  151.2572 -33.94879 11/01/2017                      50
## 2828  151.2572 -33.94879 14/12/2017                       0
## 2829  151.2572 -33.94879 27/11/2017                       0
## 2830  151.2572 -33.94879 21/11/2017                       9
## 2831  151.2572 -33.94879 27/10/2017                      15
## 2832  151.2572 -33.94879 09/02/2017                       8
## 2833  151.2572 -33.94879 04/02/2017                       4
## 2834  151.2572 -33.94879 23/01/2017                       1
## 2835  151.2572 -33.94879 17/01/2017                       0
## 2836  151.2572 -33.95161 17/01/2017                       0
## 2837  151.2572 -33.95161 05/01/2017                       0
## 2838  151.2572 -33.95161 09/02/2017                      10
## 2839  151.2572 -33.95161 03/11/2017                       3
## 2840  151.2572 -33.95161 21/11/2017                      17
## 2841  151.2572 -33.95161 27/11/2017                       0
## 2842  151.2572 -33.95161 04/12/2017                      20
## 2843  151.2572 -33.95161 14/12/2017                       1
## 2844  151.2572 -33.95161 11/01/2017                      60
## 2845  151.2572 -33.95161 30/01/2017                       4
## 2846  151.2572 -33.95161 04/02/2017                       3
## 2847  151.2572 -33.95161 23/01/2017                       4
## 2848  151.2572 -33.95161 21/02/2017                       2
## 2849  151.2572 -33.95161 15/02/2017                       0
## 2850  151.2572 -33.95161 27/02/2017                      16
## 2851  151.2572 -33.95161 27/10/2017                      28
## 2852  151.2572 -33.95161 28/12/2017                       1
## 2853  151.2572 -33.95161 03/03/2017                      36
## 2854  151.2572 -33.95161 16/03/2017                      25
## 2855  151.2572 -33.95161 22/03/2017                      36
## 2856  151.2572 -33.95161 28/03/2017                       5
## 2857  151.2572 -33.95161 13/04/2017                      10
## 2858  151.2572 -33.95161 09/11/2017                       0
## 2859  151.2572 -33.95161 15/11/2017                       0
## 2860  151.2572 -33.95161 20/12/2017                      21
## 2861  151.2572 -33.95161 08/12/2017                       2
## 2862  151.2572 -33.95161 09/03/2017                       0
## 2863  151.2572 -33.95161 03/04/2017                      16
## 2864  151.2572 -33.95161 07/04/2017                       9
## 2865  151.2572 -33.95161 21/04/2017                       0
## 2866  151.2572 -33.95161 29/05/2017                       2
## 2867  151.2572 -33.95161 04/05/2017                       2
## 2868  151.2572 -33.95161 20/06/2017                       6
## 2869  151.2572 -33.95161 01/06/2017                       0
## 2870  151.2572 -33.95161 14/06/2017                      11
## 2871  151.2572 -33.95161 03/08/2017                       3
## 2872  151.2572 -33.95161 17/07/2017                       1
## 2873  151.2572 -33.95161 19/09/2017                      13
## 2874  151.2572 -33.95161 29/09/2017                       0
## 2875  151.2572 -33.95161 25/09/2017                      13
## 2876  151.2572 -33.95161 13/09/2017                       1
## 2877  151.2572 -33.95161 01/09/2017                       0
## 2878  151.2572 -33.95161 28/04/2017                      37
## 2879  151.2572 -33.95161 23/10/2017                       4
## 2880  151.2572 -33.95161 05/10/2017                       0
## 2881  151.2572 -33.95161 11/10/2017                       1
## 2882  151.2572 -33.95161 17/10/2017                       0
## 2883  151.2572 -33.95161 16/05/2017                       9
## 2884  151.2572 -33.95161 22/05/2017                      16
## 2885  151.2572 -33.95161 10/05/2017                       3
## 2886  151.2572 -33.95161 08/06/2017                      14
## 2887  151.2572 -33.95161 24/07/2017                       2
## 2888  151.2572 -33.95161 30/06/2017                       2
## 2889  151.2572 -33.95161 11/07/2017                       4
## 2890  151.2572 -33.95161 26/06/2017                      27
## 2891  151.2572 -33.95161 28/07/2017                       2
## 2892  151.2572 -33.95161 09/08/2017                       0
## 2893  151.2572 -33.95161 16/08/2017                       1
## 2894  151.2572 -33.95161 22/08/2017                       0
## 2895  151.2572 -33.95161 07/09/2017                       0
## 2896  151.2572 -33.95161 29/08/2017                       1
## 2897  151.2582 -33.95354 29/08/2017                       0
## 2898  151.2582 -33.95354 13/09/2017                       0
## 2899  151.2582 -33.95354 22/08/2017                       5
## 2900  151.2582 -33.95354 16/08/2017                       4
## 2901  151.2582 -33.95354 03/08/2017                     160
## 2902  151.2582 -33.95354 26/06/2017                     100
## 2903  151.2582 -33.95354 30/06/2017                       1
## 2904  151.2582 -33.95354 24/07/2017                       3
## 2905  151.2582 -33.95354 08/06/2017                      96
## 2906  151.2582 -33.95354 20/06/2017                      62
## 2907  151.2582 -33.95354 22/05/2017                      16
## 2908  151.2582 -33.95354 17/10/2017                       0
## 2909  151.2582 -33.95354 11/10/2017                       5
## 2910  151.2582 -33.95354 05/10/2017                       0
## 2911  151.2582 -33.95354 23/10/2017                      34
## 2912  151.2582 -33.95354 28/04/2017                       2
## 2913  151.2582 -33.95354 01/09/2017                       0
## 2914  151.2582 -33.95354 07/09/2017                       2
## 2915  151.2582 -33.95354 25/09/2017                       1
## 2916  151.2582 -33.95354 29/09/2017                       0
## 2917  151.2582 -33.95354 19/09/2017                       0
## 2918  151.2582 -33.95354 17/07/2017                       0
## 2919  151.2582 -33.95354 28/07/2017                       2
## 2920  151.2582 -33.95354 09/08/2017                       5
## 2921  151.2582 -33.95354 14/06/2017                     120
## 2922  151.2582 -33.95354 01/06/2017                       0
## 2923  151.2582 -33.95354 11/07/2017                       2
## 2924  151.2582 -33.95354 04/05/2017                       6
## 2925  151.2582 -33.95354 10/05/2017                       0
## 2926  151.2582 -33.95354 29/05/2017                      15
## 2927  151.2582 -33.95354 16/05/2017                       3
## 2928  151.2582 -33.95354 21/04/2017                       2
## 2929  151.2582 -33.95354 07/04/2017                      10
## 2930  151.2582 -33.95354 16/03/2017                      34
## 2931  151.2582 -33.95354 09/03/2017                       9
## 2932  151.2582 -33.95354 20/12/2017                       1
## 2933  151.2582 -33.95354 28/12/2017                       1
## 2934  151.2582 -33.95354 09/11/2017                      21
## 2935  151.2582 -33.95354 13/04/2017                      80
## 2936  151.2582 -33.95354 03/04/2017                     720
## 2937  151.2582 -33.95354 28/03/2017                      31
## 2938  151.2582 -33.95354 22/03/2017                      42
## 2939  151.2582 -33.95354 03/03/2017                     190
## 2940  151.2582 -33.95354 27/10/2017                     900
## 2941  151.2582 -33.95354 27/02/2017                      50
## 2942  151.2582 -33.95354 15/02/2017                      10
## 2943  151.2582 -33.95354 23/01/2017                       4
## 2944  151.2582 -33.95354 04/02/2017                       3
## 2945  151.2582 -33.95354 14/12/2017                       7
## 2946  151.2582 -33.95354 08/12/2017                       1
## 2947  151.2582 -33.95354 04/12/2017                      13
## 2948  151.2582 -33.95354 27/11/2017                       2
## 2949  151.2582 -33.95354 21/11/2017                       6
## 2950  151.2582 -33.95354 15/11/2017                       3
## 2951  151.2582 -33.95354 03/11/2017                      13
## 2952  151.2582 -33.95354 09/02/2017                      26
## 2953  151.2582 -33.95354 21/02/2017                       2
## 2954  151.2582 -33.95354 05/01/2017                       0
## 2955  151.2582 -33.95354 17/01/2017                       0
## 2956  151.2582 -33.95354 11/01/2017                      22
## 2957  151.2582 -33.95354 30/01/2017                      15
## 2958  151.2776 -33.89151 30/01/2017                       3
## 2959  151.2776 -33.89151 17/01/2017                       0
## 2960  151.2776 -33.89151 05/01/2017                       3
## 2961  151.2776 -33.89151 11/01/2017                      15
## 2962  151.2776 -33.89151 21/02/2017                       2
## 2963  151.2776 -33.89151 03/11/2017                      10
## 2964  151.2776 -33.89151 15/11/2017                       1
## 2965  151.2776 -33.89151 21/11/2017                       3
## 2966  151.2776 -33.89151 27/11/2017                       6
## 2967  151.2776 -33.89151 04/12/2017                     130
## 2968  151.2776 -33.89151 14/12/2017                       1
## 2969  151.2776 -33.89151 08/12/2017                       3
## 2970  151.2776 -33.89151 04/02/2017                       2
## 2971  151.2776 -33.89151 23/01/2017                       5
## 2972  151.2776 -33.89151 27/10/2017                      60
## 2973  151.2776 -33.89151 15/02/2017                      27
## 2974  151.2776 -33.89151 09/02/2017                      24
## 2975  151.2776 -33.89151 03/03/2017                     110
## 2976  151.2776 -33.89151 27/02/2017                      19
## 2977  151.2776 -33.89151 28/03/2017                      17
## 2978  151.2776 -33.89151 22/03/2017                      28
## 2979  151.2776 -33.89151 03/04/2017                      42
## 2980  151.2776 -33.89151 13/04/2017                      25
## 2981  151.2776 -33.89151 09/11/2017                       2
## 2982  151.2776 -33.89151 20/12/2017                       1
## 2983  151.2776 -33.89151 28/12/2017                       1
## 2984  151.2776 -33.89151 09/03/2017                       1
## 2985  151.2776 -33.89151 16/03/2017                      20
## 2986  151.2776 -33.89151 07/04/2017                       6
## 2987  151.2776 -33.89151 28/04/2017                      14
## 2988  151.2776 -33.89151 16/05/2017                       0
## 2989  151.2776 -33.89151 29/05/2017                       0
## 2990  151.2776 -33.89151 10/05/2017                       2
## 2991  151.2776 -33.89151 04/05/2017                       1
## 2992  151.2776 -33.89151 21/04/2017                       5
## 2993  151.2776 -33.89151 17/07/2017                       1
## 2994  151.2776 -33.89151 26/06/2017                       5
## 2995  151.2776 -33.89151 20/06/2017                       4
## 2996  151.2776 -33.89151 01/06/2017                       4
## 2997  151.2776 -33.89151 14/06/2017                      15
## 2998  151.2776 -33.89151 16/08/2017                       0
## 2999  151.2776 -33.89151 22/08/2017                      10
## 3000  151.2776 -33.89151 03/08/2017                      13
## 3001  151.2776 -33.89151 13/09/2017                       3
## 3002  151.2776 -33.89151 05/10/2017                       1
## 3003  151.2776 -33.89151 25/09/2017                       1
## 3004  151.2776 -33.89151 19/09/2017                      20
## 3005  151.2776 -33.89151 01/09/2017                       2
## 3006  151.2776 -33.89151 11/10/2017                      17
## 3007  151.2776 -33.89151 23/10/2017                      14
## 3008  151.2776 -33.89151 17/10/2017                       1
## 3009  151.2776 -33.89151 22/05/2017                       8
## 3010  151.2776 -33.89151 08/06/2017                      44
## 3011  151.2776 -33.89151 28/07/2017                       6
## 3012  151.2776 -33.89151 24/07/2017                       2
## 3013  151.2776 -33.89151 11/07/2017                      10
## 3014  151.2776 -33.89151 30/06/2017                      19
## 3015  151.2776 -33.89151 09/08/2017                       1
## 3016  151.2776 -33.89151 07/09/2017                      14
## 3017  151.2776 -33.89151 29/08/2017                       0
## 3018  151.2776 -33.89151 29/09/2017                       0
## 3019  151.2686 -33.90307 05/10/2017                       3
## 3020  151.2686 -33.90307 17/10/2017                       1
## 3021  151.2686 -33.90307 13/09/2017                       5
## 3022  151.2686 -33.90307 29/08/2017                       2
## 3023  151.2686 -33.90307 22/08/2017                       3
## 3024  151.2686 -33.90307 03/08/2017                      16
## 3025  151.2686 -33.90307 16/08/2017                       2
## 3026  151.2686 -33.90307 23/10/2017                      11
## 3027  151.2686 -33.90307 29/09/2017                       0
## 3028  151.2686 -33.90307 26/06/2017                       7
## 3029  151.2686 -33.90307 30/06/2017                      17
## 3030  151.2686 -33.90307 24/07/2017                      13
## 3031  151.2686 -33.90307 20/06/2017                      13
## 3032  151.2686 -33.90307 01/06/2017                       3
## 3033  151.2686 -33.90307 11/10/2017                       7
## 3034  151.2686 -33.90307 25/09/2017                       4
## 3035  151.2686 -33.90307 04/05/2017                       9
## 3036  151.2686 -33.90307 01/09/2017                       3
## 3037  151.2686 -33.90307 07/09/2017                      12
## 3038  151.2686 -33.90307 19/09/2017                      22
## 3039  151.2686 -33.90307 09/08/2017                       0
## 3040  151.2686 -33.90307 28/07/2017                       2
## 3041  151.2686 -33.90307 17/07/2017                       2
## 3042  151.2686 -33.90307 08/06/2017                      35
## 3043  151.2686 -33.90307 14/06/2017                      30
## 3044  151.2686 -33.90307 29/05/2017                       4
## 3045  151.2686 -33.90307 11/07/2017                       1
## 3046  151.2686 -33.90307 13/04/2017                       7
## 3047  151.2686 -33.90307 28/04/2017                       4
## 3048  151.2686 -33.90307 10/05/2017                       0
## 3049  151.2686 -33.90307 22/05/2017                      20
## 3050  151.2686 -33.90307 16/05/2017                       1
## 3051  151.2686 -33.90307 27/02/2017                      27
## 3052  151.2686 -33.90307 16/03/2017                      34
## 3053  151.2686 -33.90307 03/03/2017                     130
## 3054  151.2686 -33.90307 28/12/2017                       1
## 3055  151.2686 -33.90307 14/12/2017                       2
## 3056  151.2686 -33.90307 27/11/2017                       6
## 3057  151.2686 -33.90307 21/04/2017                       8
## 3058  151.2686 -33.90307 21/11/2017                       4
## 3059  151.2686 -33.90307 07/04/2017                       9
## 3060  151.2686 -33.90307 28/03/2017                      32
## 3061  151.2686 -33.90307 03/04/2017                     180
## 3062  151.2686 -33.90307 09/03/2017                       7
## 3063  151.2686 -33.90307 22/03/2017                      26
## 3064  151.2686 -33.90307 27/10/2017                      21
## 3065  151.2686 -33.90307 04/02/2017                      10
## 3066  151.2686 -33.90307 09/02/2017                      60
## 3067  151.2686 -33.90307 23/01/2017                       4
## 3068  151.2686 -33.90307 17/01/2017                       2
## 3069  151.2686 -33.90307 08/12/2017                       4
## 3070  151.2686 -33.90307 20/12/2017                       2
## 3071  151.2686 -33.90307 04/12/2017                     110
## 3072  151.2686 -33.90307 15/11/2017                       2
## 3073  151.2686 -33.90307 09/11/2017                       4
## 3074  151.2686 -33.90307 03/11/2017                       7
## 3075  151.2686 -33.90307 15/02/2017                       7
## 3076  151.2686 -33.90307 21/02/2017                       8
## 3077  151.2686 -33.90307 05/01/2017                       9
## 3078  151.2686 -33.90307 11/01/2017                      41
## 3079  151.2686 -33.90307 30/01/2017                       8
## 3080  151.2706 -33.90056 30/01/2017                       5
## 3081  151.2706 -33.90056 17/01/2017                       0
## 3082  151.2706 -33.90056 11/01/2017                      12
## 3083  151.2706 -33.90056 05/01/2017                       3
## 3084  151.2706 -33.90056 21/02/2017                       2
## 3085  151.2706 -33.90056 03/11/2017                       8
## 3086  151.2706 -33.90056 09/11/2017                       3
## 3087  151.2706 -33.90056 15/11/2017                       2
## 3088  151.2706 -33.90056 04/12/2017                      65
## 3089  151.2706 -33.90056 20/12/2017                      28
## 3090  151.2706 -33.90056 08/12/2017                       0
## 3091  151.2706 -33.90056 23/01/2017                       1
## 3092  151.2706 -33.90056 04/02/2017                       1
## 3093  151.2706 -33.90056 27/10/2017                      25
## 3094  151.2706 -33.90056 09/02/2017                      15
## 3095  151.2706 -33.90056 15/02/2017                      35
## 3096  151.2706 -33.90056 03/03/2017                     390
## 3097  151.2706 -33.90056 09/03/2017                       3
## 3098  151.2706 -33.90056 28/03/2017                      21
## 3099  151.2706 -33.90056 22/03/2017                     200
## 3100  151.2706 -33.90056 07/04/2017                      15
## 3101  151.2706 -33.90056 03/04/2017                     110
## 3102  151.2706 -33.90056 27/11/2017                       0
## 3103  151.2706 -33.90056 21/04/2017                       7
## 3104  151.2706 -33.90056 21/11/2017                       0
## 3105  151.2706 -33.90056 14/12/2017                       0
## 3106  151.2706 -33.90056 28/12/2017                       0
## 3107  151.2706 -33.90056 27/02/2017                      15
## 3108  151.2706 -33.90056 16/03/2017                      18
## 3109  151.2706 -33.90056 28/04/2017                       3
## 3110  151.2706 -33.90056 13/04/2017                       5
## 3111  151.2706 -33.90056 16/05/2017                       1
## 3112  151.2706 -33.90056 22/05/2017                      14
## 3113  151.2706 -33.90056 29/05/2017                       3
## 3114  151.2706 -33.90056 10/05/2017                       0
## 3115  151.2706 -33.90056 04/05/2017                       6
## 3116  151.2706 -33.90056 17/07/2017                       0
## 3117  151.2706 -33.90056 20/06/2017                       7
## 3118  151.2706 -33.90056 01/06/2017                       4
## 3119  151.2706 -33.90056 08/06/2017                      54
## 3120  151.2706 -33.90056 14/06/2017                      45
## 3121  151.2706 -33.90056 03/08/2017                      11
## 3122  151.2706 -33.90056 13/09/2017                       4
## 3123  151.2706 -33.90056 25/09/2017                       0
## 3124  151.2706 -33.90056 05/10/2017                       0
## 3125  151.2706 -33.90056 01/09/2017                       3
## 3126  151.2706 -33.90056 19/09/2017                      26
## 3127  151.2706 -33.90056 11/10/2017                       4
## 3128  151.2706 -33.90056 17/10/2017                       1
## 3129  151.2706 -33.90056 23/10/2017                      17
## 3130  151.2706 -33.90056 28/07/2017                       2
## 3131  151.2706 -33.90056 24/07/2017                       9
## 3132  151.2706 -33.90056 26/06/2017                       1
## 3133  151.2706 -33.90056 30/06/2017                      27
## 3134  151.2706 -33.90056 11/07/2017                       0
## 3135  151.2706 -33.90056 16/08/2017                       0
## 3136  151.2706 -33.90056 09/08/2017                       1
## 3137  151.2706 -33.90056 22/08/2017                       3
## 3138  151.2706 -33.90056 29/08/2017                       0
## 3139  151.2706 -33.90056 07/09/2017                       7
## 3140  151.2706 -33.90056 29/09/2017                       1
## 3141  151.2675 -33.91449 19/09/2018                       1
## 3142  151.2675 -33.91449 28/09/2018                       2
## 3143  151.2675 -33.91449 05/10/2018                      34
## 3144  151.2675 -33.91449 11/10/2018                      NA
## 3145  151.2675 -33.91449 16/10/2018                      NA
## 3146  151.2675 -33.91449 03/01/2018                       1
## 3147  151.2675 -33.91449 09/01/2018                      71
## 3148  151.2675 -33.91449 15/01/2018                      30
## 3149  151.2675 -33.91449 25/01/2018                       6
## 3150  151.2675 -33.91449 13/02/2018                       2
## 3151  151.2675 -33.91449 20/03/2018                       5
## 3152  151.2675 -33.91449 26/03/2018                      23
## 3153  151.2675 -33.91449 10/04/2018                       8
## 3154  151.2675 -33.91449 16/04/2018                       1
## 3155  151.2675 -33.91449 27/04/2018                      32
## 3156  151.2675 -33.91449 07/05/2018                       5
## 3157  151.2675 -33.91449 11/05/2018                       3
## 3158  151.2675 -33.91449 23/05/2018                       2
## 3159  151.2675 -33.91449 29/05/2018                       5
## 3160  151.2675 -33.91449 10/07/2018                      24
## 3161  151.2675 -33.91449 01/08/2018                       3
## 3162  151.2675 -33.91449 14/08/2018                       0
## 3163  151.2675 -33.91449 24/08/2018                       2
## 3164  151.2675 -33.91449 12/09/2018                       3
## 3165  151.2675 -33.91449 24/09/2018                       6
## 3166  151.2675 -33.91449 19/01/2018                      30
## 3167  151.2675 -33.91449 01/02/2018                       3
## 3168  151.2675 -33.91449 07/02/2018                       0
## 3169  151.2675 -33.91449 19/02/2018                       0
## 3170  151.2675 -33.91449 25/02/2018                      23
## 3171  151.2675 -33.91449 02/03/2018                      46
## 3172  151.2675 -33.91449 08/03/2018                       0
## 3173  151.2675 -33.91449 14/03/2018                      45
## 3174  151.2675 -33.91449 03/04/2018                      NA
## 3175  151.2675 -33.91449 20/04/2018                      NA
## 3176  151.2675 -33.91449 02/05/2018                       3
## 3177  151.2675 -33.91449 17/05/2018                      12
## 3178  151.2675 -33.91449 04/06/2018                       0
## 3179  151.2675 -33.91449 08/06/2018                      21
## 3180  151.2675 -33.91449 14/06/2018                       3
## 3181  151.2675 -33.91449 21/06/2018                       6
## 3182  151.2675 -33.91449 27/06/2018                       9
## 3183  151.2675 -33.91449 04/07/2018                       2
## 3184  151.2675 -33.91449 16/07/2018                       2
## 3185  151.2675 -33.91449 20/07/2018                       0
## 3186  151.2675 -33.91449 26/07/2018                       0
## 3187  151.2675 -33.91449 08/08/2018                       2
## 3188  151.2675 -33.91449 21/08/2018                       2
## 3189  151.2675 -33.91449 30/08/2018                      10
## 3190  151.2675 -33.91449 05/09/2018                       1
## 3191  151.2582 -33.92076 30/08/2018                       9
## 3192  151.2582 -33.92076 21/08/2018                       3
## 3193  151.2582 -33.92076 16/07/2018                       4
## 3194  151.2582 -33.92076 20/07/2018                       6
## 3195  151.2582 -33.92076 08/06/2018                      15
## 3196  151.2582 -33.92076 23/05/2018                       6
## 3197  151.2582 -33.92076 07/05/2018                       4
## 3198  151.2582 -33.92076 20/04/2018                       8
## 3199  151.2582 -33.92076 16/04/2018                       0
## 3200  151.2582 -33.92076 08/03/2018                       0
## 3201  151.2582 -33.92076 20/03/2018                       5
## 3202  151.2582 -33.92076 14/03/2018                      45
## 3203  151.2582 -33.92076 02/03/2018                      45
## 3204  151.2582 -33.92076 25/02/2018                      23
## 3205  151.2582 -33.92076 19/02/2018                       6
## 3206  151.2582 -33.92076 07/02/2018                       5
## 3207  151.2582 -33.92076 25/01/2018                       3
## 3208  151.2582 -33.92076 11/10/2018                      NA
## 3209  151.2582 -33.92076 16/10/2018                      NA
## 3210  151.2582 -33.92076 05/10/2018                      47
## 3211  151.2582 -33.92076 19/09/2018                      18
## 3212  151.2582 -33.92076 05/09/2018                      11
## 3213  151.2582 -33.92076 24/08/2018                      65
## 3214  151.2582 -33.92076 14/08/2018                       1
## 3215  151.2582 -33.92076 01/08/2018                       5
## 3216  151.2582 -33.92076 08/08/2018                       0
## 3217  151.2582 -33.92076 26/07/2018                       0
## 3218  151.2582 -33.92076 27/06/2018                      15
## 3219  151.2582 -33.92076 10/07/2018                      31
## 3220  151.2582 -33.92076 14/06/2018                      11
## 3221  151.2582 -33.92076 21/06/2018                      38
## 3222  151.2582 -33.92076 04/07/2018                       3
## 3223  151.2582 -33.92076 11/05/2018                       8
## 3224  151.2582 -33.92076 04/06/2018                      14
## 3225  151.2582 -33.92076 29/05/2018                       0
## 3226  151.2582 -33.92076 17/05/2018                       8
## 3227  151.2582 -33.92076 02/05/2018                      22
## 3228  151.2582 -33.92076 27/04/2018                       2
## 3229  151.2582 -33.92076 26/03/2018                      26
## 3230  151.2582 -33.92076 10/04/2018                       8
## 3231  151.2582 -33.92076 03/04/2018                       6
## 3232  151.2582 -33.92076 13/02/2018                      61
## 3233  151.2582 -33.92076 01/02/2018                      42
## 3234  151.2582 -33.92076 15/01/2018                      12
## 3235  151.2582 -33.92076 19/01/2018                       3
## 3236  151.2582 -33.92076 09/01/2018                     360
## 3237  151.2582 -33.92076 03/01/2018                      21
## 3238  151.2582 -33.92076 28/09/2018                       0
## 3239  151.2582 -33.92076 24/09/2018                       2
## 3240  151.2582 -33.92076 12/09/2018                       8
## 3241  151.2646 -33.91565 19/09/2018                       0
## 3242  151.2646 -33.91565 12/09/2018                       2
## 3243  151.2646 -33.91565 28/09/2018                       0
## 3244  151.2646 -33.91565 11/10/2018                      NA
## 3245  151.2646 -33.91565 05/10/2018                     140
## 3246  151.2646 -33.91565 03/01/2018                      15
## 3247  151.2646 -33.91565 09/01/2018                      52
## 3248  151.2646 -33.91565 15/01/2018                     340
## 3249  151.2646 -33.91565 19/01/2018                       1
## 3250  151.2646 -33.91565 01/02/2018                      24
## 3251  151.2646 -33.91565 13/02/2018                       2
## 3252  151.2646 -33.91565 26/03/2018                       7
## 3253  151.2646 -33.91565 20/03/2018                      53
## 3254  151.2646 -33.91565 10/04/2018                       1
## 3255  151.2646 -33.91565 27/04/2018                       1
## 3256  151.2646 -33.91565 02/05/2018                       0
## 3257  151.2646 -33.91565 11/05/2018                       2
## 3258  151.2646 -33.91565 29/05/2018                       2
## 3259  151.2646 -33.91565 21/06/2018                      16
## 3260  151.2646 -33.91565 27/06/2018                      11
## 3261  151.2646 -33.91565 14/06/2018                       3
## 3262  151.2646 -33.91565 10/07/2018                      23
## 3263  151.2646 -33.91565 04/07/2018                       2
## 3264  151.2646 -33.91565 01/08/2018                       0
## 3265  151.2646 -33.91565 26/07/2018                       0
## 3266  151.2646 -33.91565 14/08/2018                       0
## 3267  151.2646 -33.91565 24/08/2018                      11
## 3268  151.2646 -33.91565 24/09/2018                       1
## 3269  151.2646 -33.91565 16/10/2018                      NA
## 3270  151.2646 -33.91565 07/02/2018                       8
## 3271  151.2646 -33.91565 25/01/2018                       1
## 3272  151.2646 -33.91565 19/02/2018                       1
## 3273  151.2646 -33.91565 25/02/2018                       2
## 3274  151.2646 -33.91565 02/03/2018                      33
## 3275  151.2646 -33.91565 14/03/2018                      20
## 3276  151.2646 -33.91565 08/03/2018                       2
## 3277  151.2646 -33.91565 20/04/2018                       1
## 3278  151.2646 -33.91565 03/04/2018                       4
## 3279  151.2646 -33.91565 16/04/2018                      49
## 3280  151.2646 -33.91565 07/05/2018                       0
## 3281  151.2646 -33.91565 17/05/2018                       2
## 3282  151.2646 -33.91565 23/05/2018                       0
## 3283  151.2646 -33.91565 08/06/2018                       8
## 3284  151.2646 -33.91565 04/06/2018                       2
## 3285  151.2646 -33.91565 16/07/2018                       0
## 3286  151.2646 -33.91565 20/07/2018                       0
## 3287  151.2646 -33.91565 21/08/2018                       0
## 3288  151.2646 -33.91565 30/08/2018                       3
## 3289  151.2646 -33.91565 05/09/2018                       0
## 3290  151.2646 -33.91565 08/08/2018                       0
## 3291  151.2515 -33.98012 01/08/2018                      15
## 3292  151.2515 -33.98012 08/08/2018                       2
## 3293  151.2515 -33.98012 14/08/2018                       3
## 3294  151.2515 -33.98012 21/08/2018                       0
## 3295  151.2515 -33.98012 05/09/2018                       0
## 3296  151.2515 -33.98012 26/07/2018                       4
## 3297  151.2515 -33.98012 27/06/2018                       6
## 3298  151.2515 -33.98012 04/07/2018                       2
## 3299  151.2515 -33.98012 10/07/2018                       9
## 3300  151.2515 -33.98012 29/05/2018                       3
## 3301  151.2515 -33.98012 04/06/2018                       5
## 3302  151.2515 -33.98012 14/06/2018                      19
## 3303  151.2515 -33.98012 21/06/2018                      26
## 3304  151.2515 -33.98012 17/05/2018                       4
## 3305  151.2515 -33.98012 11/05/2018                       4
## 3306  151.2515 -33.98012 02/05/2018                      26
## 3307  151.2515 -33.98012 27/04/2018                      79
## 3308  151.2515 -33.98012 03/04/2018                      15
## 3309  151.2515 -33.98012 26/03/2018                       1
## 3310  151.2515 -33.98012 25/02/2018                       3
## 3311  151.2515 -33.98012 13/02/2018                      19
## 3312  151.2515 -33.98012 19/01/2018                      33
## 3313  151.2515 -33.98012 01/02/2018                      19
## 3314  151.2515 -33.98012 09/01/2018                    2100
## 3315  151.2515 -33.98012 15/01/2018                      50
## 3316  151.2515 -33.98012 12/09/2018                       7
## 3317  151.2515 -33.98012 24/09/2018                       7
## 3318  151.2515 -33.98012 28/09/2018                       2
## 3319  151.2515 -33.98012 30/08/2018                       1
## 3320  151.2515 -33.98012 24/08/2018                      54
## 3321  151.2515 -33.98012 20/07/2018                       3
## 3322  151.2515 -33.98012 16/07/2018                      16
## 3323  151.2515 -33.98012 08/06/2018                      13
## 3324  151.2515 -33.98012 23/05/2018                       0
## 3325  151.2515 -33.98012 07/05/2018                       4
## 3326  151.2515 -33.98012 20/04/2018                       0
## 3327  151.2515 -33.98012 20/03/2018                       3
## 3328  151.2515 -33.98012 16/04/2018                      54
## 3329  151.2515 -33.98012 10/04/2018                       2
## 3330  151.2515 -33.98012 19/02/2018                       2
## 3331  151.2515 -33.98012 02/03/2018                      76
## 3332  151.2515 -33.98012 08/03/2018                       2
## 3333  151.2515 -33.98012 14/03/2018                      18
## 3334  151.2515 -33.98012 25/01/2018                       1
## 3335  151.2515 -33.98012 07/02/2018                       0
## 3336  151.2515 -33.98012 03/01/2018                      10
## 3337  151.2515 -33.98012 05/10/2018                     110
## 3338  151.2515 -33.98012 19/09/2018                       3
## 3339  151.2515 -33.98012 16/10/2018                      NA
## 3340  151.2515 -33.98012 11/10/2018                      NA
## 3341  151.2522 -33.96436 11/10/2018                      NA
## 3342  151.2522 -33.96436 19/09/2018                       3
## 3343  151.2522 -33.96436 07/02/2018                       1
## 3344  151.2522 -33.96436 25/01/2018                       1
## 3345  151.2522 -33.96436 16/10/2018                      NA
## 3346  151.2522 -33.96436 14/03/2018                      26
## 3347  151.2522 -33.96436 02/03/2018                      40
## 3348  151.2522 -33.96436 08/03/2018                       1
## 3349  151.2522 -33.96436 19/02/2018                      33
## 3350  151.2522 -33.96436 25/02/2018                       6
## 3351  151.2522 -33.96436 20/03/2018                      17
## 3352  151.2522 -33.96436 16/04/2018                     260
## 3353  151.2522 -33.96436 20/04/2018                      90
## 3354  151.2522 -33.96436 07/05/2018                      16
## 3355  151.2522 -33.96436 23/05/2018                       5
## 3356  151.2522 -33.96436 08/06/2018                      10
## 3357  151.2522 -33.96436 16/07/2018                       3
## 3358  151.2522 -33.96436 20/07/2018                       5
## 3359  151.2522 -33.96436 21/08/2018                       0
## 3360  151.2522 -33.96436 30/08/2018                       9
## 3361  151.2522 -33.96436 12/09/2018                      24
## 3362  151.2522 -33.96436 05/10/2018                      54
## 3363  151.2522 -33.96436 24/09/2018                      40
## 3364  151.2522 -33.96436 09/01/2018                     110
## 3365  151.2522 -33.96436 15/01/2018                       9
## 3366  151.2522 -33.96436 28/09/2018                      52
## 3367  151.2522 -33.96436 03/01/2018                      65
## 3368  151.2522 -33.96436 19/01/2018                      27
## 3369  151.2522 -33.96436 01/02/2018                      50
## 3370  151.2522 -33.96436 13/02/2018                     320
## 3371  151.2522 -33.96436 26/03/2018                      32
## 3372  151.2522 -33.96436 03/04/2018                     130
## 3373  151.2522 -33.96436 10/04/2018                      12
## 3374  151.2522 -33.96436 27/04/2018                       9
## 3375  151.2522 -33.96436 02/05/2018                       3
## 3376  151.2522 -33.96436 11/05/2018                      38
## 3377  151.2522 -33.96436 17/05/2018                      10
## 3378  151.2522 -33.96436 21/06/2018                      14
## 3379  151.2522 -33.96436 14/06/2018                       3
## 3380  151.2522 -33.96436 04/06/2018                      13
## 3381  151.2522 -33.96436 29/05/2018                      12
## 3382  151.2522 -33.96436 04/07/2018                      22
## 3383  151.2522 -33.96436 27/06/2018                       7
## 3384  151.2522 -33.96436 26/07/2018                       4
## 3385  151.2522 -33.96436 10/07/2018                     160
## 3386  151.2522 -33.96436 05/09/2018                      17
## 3387  151.2522 -33.96436 24/08/2018                      10
## 3388  151.2522 -33.96436 14/08/2018                      42
## 3389  151.2522 -33.96436 08/08/2018                       0
## 3390  151.2522 -33.96436 01/08/2018                      11
## 3391  151.2572 -33.94879 30/08/2018                       8
## 3392  151.2572 -33.94879 24/08/2018                      48
## 3393  151.2572 -33.94879 20/07/2018                       6
## 3394  151.2572 -33.94879 23/05/2018                       0
## 3395  151.2572 -33.94879 08/06/2018                      21
## 3396  151.2572 -33.94879 07/05/2018                       4
## 3397  151.2572 -33.94879 20/04/2018                       7
## 3398  151.2572 -33.94879 10/04/2018                       1
## 3399  151.2572 -33.94879 16/04/2018                       6
## 3400  151.2572 -33.94879 08/03/2018                       0
## 3401  151.2572 -33.94879 14/03/2018                       7
## 3402  151.2572 -33.94879 20/03/2018                       1
## 3403  151.2572 -33.94879 19/02/2018                       0
## 3404  151.2572 -33.94879 02/03/2018                       0
## 3405  151.2572 -33.94879 07/02/2018                       0
## 3406  151.2572 -33.94879 03/01/2018                      22
## 3407  151.2572 -33.94879 16/10/2018                      NA
## 3408  151.2572 -33.94879 11/10/2018                      NA
## 3409  151.2572 -33.94879 25/01/2018                       2
## 3410  151.2572 -33.94879 28/09/2018                       2
## 3411  151.2572 -33.94879 05/10/2018                       9
## 3412  151.2572 -33.94879 19/09/2018                       1
## 3413  151.2572 -33.94879 05/09/2018                       3
## 3414  151.2572 -33.94879 21/08/2018                       0
## 3415  151.2572 -33.94879 14/08/2018                       0
## 3416  151.2572 -33.94879 26/07/2018                       0
## 3417  151.2572 -33.94879 01/08/2018                       1
## 3418  151.2572 -33.94879 08/08/2018                       1
## 3419  151.2572 -33.94879 16/07/2018                       1
## 3420  151.2572 -33.94879 27/06/2018                       3
## 3421  151.2572 -33.94879 10/07/2018                      23
## 3422  151.2572 -33.94879 14/06/2018                       3
## 3423  151.2572 -33.94879 21/06/2018                      28
## 3424  151.2572 -33.94879 04/07/2018                       6
## 3425  151.2572 -33.94879 11/05/2018                       4
## 3426  151.2572 -33.94879 29/05/2018                       0
## 3427  151.2572 -33.94879 04/06/2018                      10
## 3428  151.2572 -33.94879 17/05/2018                       1
## 3429  151.2572 -33.94879 02/05/2018                       2
## 3430  151.2572 -33.94879 27/04/2018                       0
## 3431  151.2572 -33.94879 03/04/2018                      NA
## 3432  151.2572 -33.94879 26/03/2018                       4
## 3433  151.2572 -33.94879 25/02/2018                      25
## 3434  151.2572 -33.94879 13/02/2018                       1
## 3435  151.2572 -33.94879 01/02/2018                      50
## 3436  151.2572 -33.94879 09/01/2018                     110
## 3437  151.2572 -33.94879 15/01/2018                      10
## 3438  151.2572 -33.94879 19/01/2018                       1
## 3439  151.2572 -33.94879 12/09/2018                       0
## 3440  151.2572 -33.94879 24/09/2018                       1
## 3441  151.2572 -33.95161 24/09/2018                       1
## 3442  151.2572 -33.95161 12/09/2018                       0
## 3443  151.2572 -33.95161 19/01/2018                       2
## 3444  151.2572 -33.95161 09/01/2018                     300
## 3445  151.2572 -33.95161 01/02/2018                      46
## 3446  151.2572 -33.95161 07/02/2018                       0
## 3447  151.2572 -33.95161 19/02/2018                       1
## 3448  151.2572 -33.95161 25/02/2018                      11
## 3449  151.2572 -33.95161 02/03/2018                       5
## 3450  151.2572 -33.95161 14/03/2018                      13
## 3451  151.2572 -33.95161 03/04/2018                       6
## 3452  151.2572 -33.95161 20/04/2018                       2
## 3453  151.2572 -33.95161 02/05/2018                       6
## 3454  151.2572 -33.95161 17/05/2018                       1
## 3455  151.2572 -33.95161 04/06/2018                       6
## 3456  151.2572 -33.95161 08/06/2018                       4
## 3457  151.2572 -33.95161 04/07/2018                      12
## 3458  151.2572 -33.95161 21/06/2018                      14
## 3459  151.2572 -33.95161 14/06/2018                       1
## 3460  151.2572 -33.95161 27/06/2018                       0
## 3461  151.2572 -33.95161 16/07/2018                       2
## 3462  151.2572 -33.95161 20/07/2018                       1
## 3463  151.2572 -33.95161 08/08/2018                       0
## 3464  151.2572 -33.95161 26/07/2018                       2
## 3465  151.2572 -33.95161 21/08/2018                       1
## 3466  151.2572 -33.95161 30/08/2018                       7
## 3467  151.2572 -33.95161 05/09/2018                       0
## 3468  151.2572 -33.95161 19/09/2018                       3
## 3469  151.2572 -33.95161 05/10/2018                       9
## 3470  151.2572 -33.95161 28/09/2018                       0
## 3471  151.2572 -33.95161 25/01/2018                       1
## 3472  151.2572 -33.95161 15/01/2018                      10
## 3473  151.2572 -33.95161 11/10/2018                      NA
## 3474  151.2572 -33.95161 16/10/2018                      NA
## 3475  151.2572 -33.95161 03/01/2018                      18
## 3476  151.2572 -33.95161 13/02/2018                       3
## 3477  151.2572 -33.95161 20/03/2018                       3
## 3478  151.2572 -33.95161 26/03/2018                       8
## 3479  151.2572 -33.95161 08/03/2018                       1
## 3480  151.2572 -33.95161 16/04/2018                       8
## 3481  151.2572 -33.95161 10/04/2018                       8
## 3482  151.2572 -33.95161 27/04/2018                       3
## 3483  151.2572 -33.95161 07/05/2018                       3
## 3484  151.2572 -33.95161 11/05/2018                       0
## 3485  151.2572 -33.95161 23/05/2018                       1
## 3486  151.2572 -33.95161 29/05/2018                       0
## 3487  151.2572 -33.95161 10/07/2018                      21
## 3488  151.2572 -33.95161 24/08/2018                      45
## 3489  151.2572 -33.95161 01/08/2018                       0
## 3490  151.2572 -33.95161 14/08/2018                      11
## 3491  151.2582 -33.95354 14/08/2018                       0
## 3492  151.2582 -33.95354 01/08/2018                       1
## 3493  151.2582 -33.95354 24/08/2018                      27
## 3494  151.2582 -33.95354 10/07/2018                      76
## 3495  151.2582 -33.95354 27/06/2018                      18
## 3496  151.2582 -33.95354 26/07/2018                       0
## 3497  151.2582 -33.95354 29/05/2018                     200
## 3498  151.2582 -33.95354 21/06/2018                      24
## 3499  151.2582 -33.95354 11/05/2018                       1
## 3500  151.2582 -33.95354 27/04/2018                       2
## 3501  151.2582 -33.95354 02/05/2018                       4
## 3502  151.2582 -33.95354 10/04/2018                      31
## 3503  151.2582 -33.95354 26/03/2018                      15
## 3504  151.2582 -33.95354 20/03/2018                       0
## 3505  151.2582 -33.95354 13/02/2018                      13
## 3506  151.2582 -33.95354 01/02/2018                      52
## 3507  151.2582 -33.95354 03/01/2018                      17
## 3508  151.2582 -33.95354 09/01/2018                    1600
## 3509  151.2582 -33.95354 11/10/2018                      NA
## 3510  151.2582 -33.95354 15/01/2018                       4
## 3511  151.2582 -33.95354 19/01/2018                      10
## 3512  151.2582 -33.95354 28/09/2018                       0
## 3513  151.2582 -33.95354 05/10/2018                    1300
## 3514  151.2582 -33.95354 19/09/2018                       5
## 3515  151.2582 -33.95354 12/09/2018                      50
## 3516  151.2582 -33.95354 05/09/2018                      26
## 3517  151.2582 -33.95354 30/08/2018                      15
## 3518  151.2582 -33.95354 21/08/2018                       0
## 3519  151.2582 -33.95354 08/08/2018                       3
## 3520  151.2582 -33.95354 20/07/2018                       6
## 3521  151.2582 -33.95354 16/07/2018                       5
## 3522  151.2582 -33.95354 14/06/2018                      33
## 3523  151.2582 -33.95354 04/07/2018                       9
## 3524  151.2582 -33.95354 08/06/2018                    1700
## 3525  151.2582 -33.95354 04/06/2018                      19
## 3526  151.2582 -33.95354 23/05/2018                       0
## 3527  151.2582 -33.95354 17/05/2018                       4
## 3528  151.2582 -33.95354 07/05/2018                      10
## 3529  151.2582 -33.95354 20/04/2018                       0
## 3530  151.2582 -33.95354 16/04/2018                       6
## 3531  151.2582 -33.95354 03/04/2018                      18
## 3532  151.2582 -33.95354 14/03/2018                      30
## 3533  151.2582 -33.95354 02/03/2018                       6
## 3534  151.2582 -33.95354 08/03/2018                       1
## 3535  151.2582 -33.95354 25/02/2018                      13
## 3536  151.2582 -33.95354 19/02/2018                       1
## 3537  151.2582 -33.95354 07/02/2018                       1
## 3538  151.2582 -33.95354 25/01/2018                       0
## 3539  151.2582 -33.95354 24/09/2018                      29
## 3540  151.2582 -33.95354 16/10/2018                      NA
## 3541  151.2776 -33.89151 16/10/2018                      NA
## 3542  151.2776 -33.89151 19/09/2018                       2
## 3543  151.2776 -33.89151 07/02/2018                      12
## 3544  151.2776 -33.89151 25/01/2018                      12
## 3545  151.2776 -33.89151 19/02/2018                       9
## 3546  151.2776 -33.89151 02/03/2018                       4
## 3547  151.2776 -33.89151 25/02/2018                       2
## 3548  151.2776 -33.89151 08/03/2018                       0
## 3549  151.2776 -33.89151 14/03/2018                      27
## 3550  151.2776 -33.89151 20/03/2018                       4
## 3551  151.2776 -33.89151 03/04/2018                       3
## 3552  151.2776 -33.89151 16/04/2018                       2
## 3553  151.2776 -33.89151 20/04/2018                       8
## 3554  151.2776 -33.89151 07/05/2018                      10
## 3555  151.2776 -33.89151 23/05/2018                       1
## 3556  151.2776 -33.89151 17/05/2018                       2
## 3557  151.2776 -33.89151 08/06/2018                       6
## 3558  151.2776 -33.89151 04/06/2018                       3
## 3559  151.2776 -33.89151 20/07/2018                       5
## 3560  151.2776 -33.89151 16/07/2018                       2
## 3561  151.2776 -33.89151 08/08/2018                       0
## 3562  151.2776 -33.89151 21/08/2018                       2
## 3563  151.2776 -33.89151 30/08/2018                       0
## 3564  151.2776 -33.89151 12/09/2018                       0
## 3565  151.2776 -33.89151 05/09/2018                       1
## 3566  151.2776 -33.89151 24/09/2018                       1
## 3567  151.2776 -33.89151 11/10/2018                      NA
## 3568  151.2776 -33.89151 05/10/2018                     130
## 3569  151.2776 -33.89151 28/09/2018                       2
## 3570  151.2776 -33.89151 01/02/2018                      48
## 3571  151.2776 -33.89151 19/01/2018                       2
## 3572  151.2776 -33.89151 15/01/2018                     250
## 3573  151.2776 -33.89151 03/01/2018                      12
## 3574  151.2776 -33.89151 09/01/2018                     200
## 3575  151.2776 -33.89151 13/02/2018                     120
## 3576  151.2776 -33.89151 26/03/2018                      17
## 3577  151.2776 -33.89151 10/04/2018                       3
## 3578  151.2776 -33.89151 02/05/2018                       3
## 3579  151.2776 -33.89151 27/04/2018                       8
## 3580  151.2776 -33.89151 11/05/2018                      11
## 3581  151.2776 -33.89151 21/06/2018                      21
## 3582  151.2776 -33.89151 27/06/2018                      16
## 3583  151.2776 -33.89151 14/06/2018                      21
## 3584  151.2776 -33.89151 29/05/2018                      NA
## 3585  151.2776 -33.89151 01/08/2018                       1
## 3586  151.2776 -33.89151 26/07/2018                       1
## 3587  151.2776 -33.89151 04/07/2018                      NA
## 3588  151.2776 -33.89151 10/07/2018                      28
## 3589  151.2776 -33.89151 24/08/2018                      39
## 3590  151.2776 -33.89151 14/08/2018                       1
## 3591  151.2686 -33.90307 08/08/2018                       0
## 3592  151.2686 -33.90307 21/08/2018                       0
## 3593  151.2686 -33.90307 01/08/2018                       0
## 3594  151.2686 -33.90307 05/09/2018                       1
## 3595  151.2686 -33.90307 04/07/2018                       5
## 3596  151.2686 -33.90307 10/07/2018                      28
## 3597  151.2686 -33.90307 16/07/2018                       1
## 3598  151.2686 -33.90307 27/06/2018                       7
## 3599  151.2686 -33.90307 26/07/2018                       1
## 3600  151.2686 -33.90307 29/05/2018                       5
## 3601  151.2686 -33.90307 08/06/2018                      12
## 3602  151.2686 -33.90307 04/06/2018                       4
## 3603  151.2686 -33.90307 14/06/2018                      24
## 3604  151.2686 -33.90307 21/06/2018                      24
## 3605  151.2686 -33.90307 11/05/2018                       9
## 3606  151.2686 -33.90307 17/05/2018                       1
## 3607  151.2686 -33.90307 27/04/2018                       3
## 3608  151.2686 -33.90307 02/05/2018                       4
## 3609  151.2686 -33.90307 26/03/2018                      32
## 3610  151.2686 -33.90307 03/04/2018                       3
## 3611  151.2686 -33.90307 14/03/2018                       7
## 3612  151.2686 -33.90307 13/02/2018                      14
## 3613  151.2686 -33.90307 07/02/2018                       1
## 3614  151.2686 -33.90307 01/02/2018                      30
## 3615  151.2686 -33.90307 25/02/2018                      10
## 3616  151.2686 -33.90307 02/03/2018                      32
## 3617  151.2686 -33.90307 09/01/2018                    1400
## 3618  151.2686 -33.90307 15/01/2018                      72
## 3619  151.2686 -33.90307 19/01/2018                       3
## 3620  151.2686 -33.90307 24/09/2018                       3
## 3621  151.2686 -33.90307 12/09/2018                       3
## 3622  151.2686 -33.90307 30/08/2018                       4
## 3623  151.2686 -33.90307 24/08/2018                      56
## 3624  151.2686 -33.90307 14/08/2018                       0
## 3625  151.2686 -33.90307 20/07/2018                       3
## 3626  151.2686 -33.90307 23/05/2018                       2
## 3627  151.2686 -33.90307 07/05/2018                      10
## 3628  151.2686 -33.90307 20/04/2018                      14
## 3629  151.2686 -33.90307 16/04/2018                       0
## 3630  151.2686 -33.90307 10/04/2018                       0
## 3631  151.2686 -33.90307 20/03/2018                       5
## 3632  151.2686 -33.90307 08/03/2018                       7
## 3633  151.2686 -33.90307 19/02/2018                       1
## 3634  151.2686 -33.90307 25/01/2018                       5
## 3635  151.2686 -33.90307 19/09/2018                       6
## 3636  151.2686 -33.90307 28/09/2018                       3
## 3637  151.2686 -33.90307 11/10/2018                      NA
## 3638  151.2686 -33.90307 16/10/2018                      NA
## 3639  151.2686 -33.90307 03/01/2018                      29
## 3640  151.2686 -33.90307 05/10/2018                     200
## 3641  151.2706 -33.90056 11/10/2018                      NA
## 3642  151.2706 -33.90056 16/10/2018                      NA
## 3643  151.2706 -33.90056 05/10/2018                      76
## 3644  151.2706 -33.90056 19/09/2018                       7
## 3645  151.2706 -33.90056 07/02/2018                       1
## 3646  151.2706 -33.90056 25/01/2018                       4
## 3647  151.2706 -33.90056 25/02/2018                       1
## 3648  151.2706 -33.90056 02/03/2018                      10
## 3649  151.2706 -33.90056 19/02/2018                       3
## 3650  151.2706 -33.90056 08/03/2018                       0
## 3651  151.2706 -33.90056 20/03/2018                       4
## 3652  151.2706 -33.90056 14/03/2018                      32
## 3653  151.2706 -33.90056 16/04/2018                       0
## 3654  151.2706 -33.90056 20/04/2018                       7
## 3655  151.2706 -33.90056 07/05/2018                       2
## 3656  151.2706 -33.90056 23/05/2018                       1
## 3657  151.2706 -33.90056 08/06/2018                       5
## 3658  151.2706 -33.90056 16/07/2018                       3
## 3659  151.2706 -33.90056 20/07/2018                       1
## 3660  151.2706 -33.90056 21/08/2018                       2
## 3661  151.2706 -33.90056 30/08/2018                       4
## 3662  151.2706 -33.90056 12/09/2018                       0
## 3663  151.2706 -33.90056 24/09/2018                       0
## 3664  151.2706 -33.90056 28/09/2018                       0
## 3665  151.2706 -33.90056 01/02/2018                      35
## 3666  151.2706 -33.90056 15/01/2018                     110
## 3667  151.2706 -33.90056 19/01/2018                       3
## 3668  151.2706 -33.90056 09/01/2018                     100
## 3669  151.2706 -33.90056 03/01/2018                      16
## 3670  151.2706 -33.90056 13/02/2018                       4
## 3671  151.2706 -33.90056 26/03/2018                      27
## 3672  151.2706 -33.90056 03/04/2018                       2
## 3673  151.2706 -33.90056 10/04/2018                       3
## 3674  151.2706 -33.90056 02/05/2018                       6
## 3675  151.2706 -33.90056 27/04/2018                       0
## 3676  151.2706 -33.90056 17/05/2018                       1
## 3677  151.2706 -33.90056 11/05/2018                      20
## 3678  151.2706 -33.90056 27/06/2018                       9
## 3679  151.2706 -33.90056 21/06/2018                     140
## 3680  151.2706 -33.90056 14/06/2018                       2
## 3681  151.2706 -33.90056 04/06/2018                       5
## 3682  151.2706 -33.90056 29/05/2018                       1
## 3683  151.2706 -33.90056 01/08/2018                       0
## 3684  151.2706 -33.90056 26/07/2018                       2
## 3685  151.2706 -33.90056 04/07/2018                       2
## 3686  151.2706 -33.90056 10/07/2018                      40
## 3687  151.2706 -33.90056 05/09/2018                       0
## 3688  151.2706 -33.90056 24/08/2018                      51
## 3689  151.2706 -33.90056 08/08/2018                       1
## 3690  151.2706 -33.90056 14/08/2018                       0
```

```r
glimpse(sydneybeaches)
```

```
## Rows: 3,690
## Columns: 8
## $ BeachId                 <dbl> 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25…
## $ Region                  <chr> "Sydney City Ocean Beaches", "Sydney City Ocea…
## $ Council                 <chr> "Randwick Council", "Randwick Council", "Randw…
## $ Site                    <chr> "Clovelly Beach", "Clovelly Beach", "Clovelly …
## $ Longitude               <dbl> 151.2675, 151.2675, 151.2675, 151.2675, 151.26…
## $ Latitude                <dbl> -33.91449, -33.91449, -33.91449, -33.91449, -3…
## $ Date                    <chr> "02/01/2013", "06/01/2013", "12/01/2013", "18/…
## $ Enterococci..cfu.100ml. <int> 19, 3, 2, 13, 8, 7, 11, 97, 3, 0, 6, 0, 1, 8, …
```

```r
summary(sydneybeaches)
```

```
##     BeachId         Region            Council              Site          
##  Min.   :22.00   Length:3690        Length:3690        Length:3690       
##  1st Qu.:24.00   Class :character   Class :character   Class :character  
##  Median :26.00   Mode  :character   Mode  :character   Mode  :character  
##  Mean   :25.87                                                           
##  3rd Qu.:27.40                                                           
##  Max.   :29.00                                                           
##                                                                          
##    Longitude        Latitude          Date           Enterococci..cfu.100ml.
##  Min.   :151.3   Min.   :-33.98   Length:3690        Min.   :   0.00        
##  1st Qu.:151.3   1st Qu.:-33.95   Class :character   1st Qu.:   1.00        
##  Median :151.3   Median :-33.92   Mode  :character   Median :   5.00        
##  Mean   :151.3   Mean   :-33.93                      Mean   :  33.92        
##  3rd Qu.:151.3   3rd Qu.:-33.90                      3rd Qu.:  17.00        
##  Max.   :151.3   Max.   :-33.89                      Max.   :4900.00        
##                                                      NA's   :29
```



If you want to try `here`, first notice the output when you load the `here` library. It gives you information on the current working directory. You can then use it to easily and intuitively load files.

```r
library(here)
```

The quotes show the folder structure from the root directory.

```r
sydneybeaches <-read_csv(here("lab8", "data", "sydneybeaches.csv")) %>% janitor::clean_names()
```

```
## Rows: 3690 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): Region, Council, Site, Date
## dbl (4): BeachId, Longitude, Latitude, Enterococci (cfu/100ml)
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

2. Are these data "tidy" per the definitions of the tidyverse? How do you know? Are they in wide or long format?

tidy, long format

3. We are only interested in the variables site, date, and enterococci_cfu_100ml. Make a new object focused on these variables only. Name the object `sydneybeaches_long`

```r
sydneybeaches_long <- sydneybeaches %>% 
  select(site, date, enterococci_cfu_100ml)
sydneybeaches_long
```

```
## # A tibble: 3,690 × 3
##    site           date       enterococci_cfu_100ml
##    <chr>          <chr>                      <dbl>
##  1 Clovelly Beach 02/01/2013                    19
##  2 Clovelly Beach 06/01/2013                     3
##  3 Clovelly Beach 12/01/2013                     2
##  4 Clovelly Beach 18/01/2013                    13
##  5 Clovelly Beach 30/01/2013                     8
##  6 Clovelly Beach 05/02/2013                     7
##  7 Clovelly Beach 11/02/2013                    11
##  8 Clovelly Beach 23/02/2013                    97
##  9 Clovelly Beach 07/03/2013                     3
## 10 Clovelly Beach 25/03/2013                     0
## # … with 3,680 more rows
```



4. Pivot the data such that the dates are column names and each beach only appears once. Name the object `sydneybeaches_wide`


```r
sydneybeaches_wide <- sydneybeaches_long %>% 
  pivot_wider(
              names_from = "date",
              values_from = "enterococci_cfu_100ml")
sydneybeaches_wide
```

```
## # A tibble: 11 × 345
##    site  02/01…¹ 06/01…² 12/01…³ 18/01…⁴ 30/01…⁵ 05/02…⁶ 11/02…⁷ 23/02…⁸ 07/03…⁹
##    <chr>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1 Clov…      19       3       2      13       8       7      11      97       3
##  2 Coog…      15       4      17      18      22       2     110     630      11
##  3 Gord…      NA      NA      NA      NA      NA      NA      NA      NA      NA
##  4 Litt…       9       3      72       1      44       7     150     330      31
##  5 Mala…       2       4     390      15      13      13     140     390       6
##  6 Maro…       1       1      20       2      11       0       4      60       1
##  7 Sout…       1       0      33       2      13       0      30      92      13
##  8 Sout…      12       2     110      13     100     630      79     570      69
##  9 Bond…       3       1       2       1       6       5     600      67       1
## 10 Bron…       4       2      38       3      25       2      38     780       8
## 11 Tama…       1       0       7      22      23       3      13      90       3
## # … with 335 more variables: `25/03/2013` <dbl>, `02/04/2013` <dbl>,
## #   `12/04/2013` <dbl>, `18/04/2013` <dbl>, `24/04/2013` <dbl>,
## #   `01/05/2013` <dbl>, `20/05/2013` <dbl>, `31/05/2013` <dbl>,
## #   `06/06/2013` <dbl>, `12/06/2013` <dbl>, `24/06/2013` <dbl>,
## #   `06/07/2013` <dbl>, `18/07/2013` <dbl>, `24/07/2013` <dbl>,
## #   `08/08/2013` <dbl>, `22/08/2013` <dbl>, `29/08/2013` <dbl>,
## #   `24/01/2013` <dbl>, `17/02/2013` <dbl>, `01/03/2013` <dbl>, …
```


5. Pivot the data back so that the dates are data and not column names.


```r
sydneybeaches_wide %>% 
  pivot_longer(-site, 
               names_to = "dates",
               values_to = "enterococci_cfu_100ml")
```

```
## # A tibble: 3,784 × 3
##    site           dates      enterococci_cfu_100ml
##    <chr>          <chr>                      <dbl>
##  1 Clovelly Beach 02/01/2013                    19
##  2 Clovelly Beach 06/01/2013                     3
##  3 Clovelly Beach 12/01/2013                     2
##  4 Clovelly Beach 18/01/2013                    13
##  5 Clovelly Beach 30/01/2013                     8
##  6 Clovelly Beach 05/02/2013                     7
##  7 Clovelly Beach 11/02/2013                    11
##  8 Clovelly Beach 23/02/2013                    97
##  9 Clovelly Beach 07/03/2013                     3
## 10 Clovelly Beach 25/03/2013                     0
## # … with 3,774 more rows
```


6. We haven't dealt much with dates yet, but separate the date into columns day, month, and year. Do this on the `sydneybeaches_long` data.


```r
sydneybeaches_long_date <- sydneybeaches_long %>% 
  separate("date", into= c("month", "day", "year"), sep = "/")
sydneybeaches_long_date
```

```
## # A tibble: 3,690 × 5
##    site           month day   year  enterococci_cfu_100ml
##    <chr>          <chr> <chr> <chr>                 <dbl>
##  1 Clovelly Beach 02    01    2013                     19
##  2 Clovelly Beach 06    01    2013                      3
##  3 Clovelly Beach 12    01    2013                      2
##  4 Clovelly Beach 18    01    2013                     13
##  5 Clovelly Beach 30    01    2013                      8
##  6 Clovelly Beach 05    02    2013                      7
##  7 Clovelly Beach 11    02    2013                     11
##  8 Clovelly Beach 23    02    2013                     97
##  9 Clovelly Beach 07    03    2013                      3
## 10 Clovelly Beach 25    03    2013                      0
## # … with 3,680 more rows
```


7. What is the average `enterococci_cfu_100ml` by year for each beach. Think about which data you will use- long or wide.


```r
avg_cfu_by_year_for_beach <- 
  sydneybeaches_long_date %>% 
  group_by(site, year) %>% 
  summarize(avg_enterococci_cfu_100ml = mean(enterococci_cfu_100ml, na.rm = T)) %>% 
  arrange(site)
```

```
## `summarise()` has grouped output by 'site'. You can override using the
## `.groups` argument.
```

```r
avg_cfu_by_year_for_beach
```

```
## # A tibble: 66 × 3
## # Groups:   site [11]
##    site         year  avg_enterococci_cfu_100ml
##    <chr>        <chr>                     <dbl>
##  1 Bondi Beach  2013                       32.2
##  2 Bondi Beach  2014                       11.1
##  3 Bondi Beach  2015                       14.3
##  4 Bondi Beach  2016                       19.4
##  5 Bondi Beach  2017                       13.2
##  6 Bondi Beach  2018                       22.9
##  7 Bronte Beach 2013                       26.8
##  8 Bronte Beach 2014                       17.5
##  9 Bronte Beach 2015                       23.6
## 10 Bronte Beach 2016                       61.3
## # … with 56 more rows
```


8. Make the output from question 7 easier to read by pivoting it to wide format.


```r
avg_cfu_by_year_for_beach_wide <-
  avg_cfu_by_year_for_beach %>% 
  pivot_wider(names_from = year, 
              values_from = avg_enterococci_cfu_100ml)
avg_cfu_by_year_for_beach_wide
```

```
## # A tibble: 11 × 7
## # Groups:   site [11]
##    site                    `2013` `2014` `2015` `2016` `2017` `2018`
##    <chr>                    <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
##  1 Bondi Beach              32.2   11.1   14.3    19.4  13.2   22.9 
##  2 Bronte Beach             26.8   17.5   23.6    61.3  16.8   43.4 
##  3 Clovelly Beach            9.28  13.8    8.82   11.3   7.93  10.6 
##  4 Coogee Beach             39.7   52.6   40.3    59.5  20.7   21.6 
##  5 Gordons Bay (East)       24.8   16.7   36.2    39.0  13.7   17.6 
##  6 Little Bay Beach        122.    19.5   25.5    31.2  18.2   59.1 
##  7 Malabar Beach           101.    54.5   66.9    91.0  49.8   38.0 
##  8 Maroubra Beach           47.1    9.23  14.5    26.6  11.6    9.21
##  9 South Maroubra Beach     39.3   14.9    8.25   10.7   8.26  12.5 
## 10 South Maroubra Rockpool  96.4   40.6   47.3    59.3  46.9  112.  
## 11 Tamarama Beach           29.7   39.6   57.0    50.3  20.4   15.5
```


9. What was the most polluted beach in 2018?


```r
sydneybeaches_long_date %>% 
  filter(year == "2018") %>% 
  select(site, year, enterococci_cfu_100ml) %>% 
  slice_max(enterococci_cfu_100ml, n=1)
```

```
## # A tibble: 1 × 3
##   site             year  enterococci_cfu_100ml
##   <chr>            <chr>                 <dbl>
## 1 Little Bay Beach 2018                   2100
```


10. Please complete the class project survey at: [BIS 15L Group Project](https://forms.gle/H2j69Z3ZtbLH3efW6)


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
