# Reproducible Research: Peer Assessment 2
# Title

synopis synopsis
synopsis synopsis

## Data Processing
We first change the working directory to the repository location and load our datafile.


```r
library(plyr)
library(reshape2)

setwd("~/GitHub/RepData_PeerAssessment2")
#data<-read.csv(bzfile("data/repdata-data-StormData.csv.bz2"),header=TRUE, nrows=200000)
data<-read.csv(bzfile("data/repdata-data-StormData.csv.bz2"),header=TRUE, nrows=300000)
stormData<-data[,c("EVTYPE","FATALITIES","INJURIES","PROPDMG","PROPDMGEXP","CROPDMG","CROPDMGEXP")]

stormData$PROPDMG <- ifelse(stormData$PROPDMGEXP %in% c("k","K"),stormData$PROPDMG * 1000,    
     ifelse(stormData$PROPDMGEXP %in% c("m","M"),stormData$PROPDMG * 1000000,
          ifelse(stormData$PROPDMGEXP %in% c("b","M"),stormData$PROPDMG * 1000000000,  
            stormData$PROPDMG))) 

stormData$CROPDMG <- ifelse(stormData$CROPDMGEXP %in% c("k","K"),stormData$CROPDMG * 1000,
       ifelse(stormData$CROPDMGEXP %in% c("m","M"),stormData$CROPDMG * 1000000,
               ifelse(stormData$CROPDMGEXP %in% c("b","B"),stormData$CROPDMG * 1000000000,
                      stormData$CROPDMG)))


#Remove all unused variables
stormData$PROPDMGEXP<-NULL
stormData$CROPDMGEXP<-NULL

summedStormData<-ddply(stormData,~EVTYPE,summarise,FATALITIES=sum(FATALITIES),INJURIES=sum(INJURIES), PROPDMG=sum(PROPDMG),CROPDMG=sum(CROPDMG))
```

## Results

```r
summedStormData<-arrange(summedStormData,desc(summedStormData$FATALITIES))
#head(summedStormData,10)
data$EVTYPE<-as.character(data$EVTYPE)
data<-summedStormData[1:10,]
data
```

```
##            EVTYPE FATALITIES INJURIES   PROPDMG   CROPDMG
## 1         TORNADO       4184    72196 3.355e+10 1.464e+08
## 2            HEAT        701      878 2.770e+05 4.013e+08
## 3       TSTM WIND        314     3978 5.463e+08 5.015e+07
## 4       LIGHTNING        246     1633 2.452e+08 5.572e+06
## 5     FLASH FLOOD        240      347 2.556e+09 1.643e+08
## 6  EXCESSIVE HEAT        183      613 5.050e+04 0.000e+00
## 7       HEAT WAVE        172      309 1.046e+07 5.550e+06
## 8    EXTREME COLD        112      181 6.313e+07 3.547e+08
## 9           FLOOD        111      113 4.615e+09 1.088e+09
## 10   EXTREME HEAT         96      155 1.150e+05 5.000e+06
```

```r
summedStormData<-arrange(summedStormData,desc(summedStormData$INJURIES))
#head(summedStormData,10)
data$EVTYPE<-as.character(data$EVTYPE)
data<-summedStormData[1:10,]
data
```

```
##                EVTYPE FATALITIES INJURIES   PROPDMG   CROPDMG
## 1             TORNADO       4184    72196 3.355e+10 1.464e+08
## 2           TSTM WIND        314     3978 5.463e+08 5.015e+07
## 3           ICE STORM         23     1800 5.401e+08 5.012e+09
## 4           LIGHTNING        246     1633 2.452e+08 5.572e+06
## 5  THUNDERSTORM WINDS         64      908 1.736e+09 1.907e+08
## 6                HEAT        701      878 2.770e+05 4.013e+08
## 7                HAIL          9      731 1.892e+09 8.938e+08
## 8            BLIZZARD         74      694 4.330e+08 1.050e+08
## 9      EXCESSIVE HEAT        183      613 5.050e+04 0.000e+00
## 10         HEAVY SNOW         62      488 5.488e+08 1.313e+08
```

```r
summedStormData<-arrange(summedStormData,desc(summedStormData$PROPDMG))
#head(summedStormData,10)
data$EVTYPE<-as.character(data$EVTYPE)
data<-summedStormData[1:10,]
data
```

```
##                EVTYPE FATALITIES INJURIES   PROPDMG   CROPDMG
## 1             TORNADO       4184    72196 3.355e+10 1.464e+08
## 2               FLOOD        111      113 4.615e+09 1.088e+09
## 3         FLASH FLOOD        240      347 2.556e+09 1.643e+08
## 4                HAIL          9      731 1.892e+09 8.938e+08
## 5  THUNDERSTORM WINDS         64      908 1.736e+09 1.907e+08
## 6           HURRICANE         37       17 1.503e+09 3.528e+08
## 7          WILD FIRES          3      150 6.241e+08 0.000e+00
## 8          HIGH WINDS         35      302 6.078e+08 4.072e+07
## 9          HEAVY SNOW         62      488 5.488e+08 1.313e+08
## 10          TSTM WIND        314     3978 5.463e+08 5.015e+07
```

```r
summedStormData<-arrange(summedStormData,desc(summedStormData$CROPDMG))
#head(summedStormData,10)
data$EVTYPE<-as.character(data$EVTYPE)
data<-summedStormData[1:10,]
data
```

```
##             EVTYPE FATALITIES INJURIES   PROPDMG   CROPDMG
## 1      RIVER FLOOD          1        2 1.048e+08 5.029e+09
## 2        ICE STORM         23     1800 5.401e+08 5.012e+09
## 3          DROUGHT          0        0 1.354e+08 1.220e+09
## 4            FLOOD        111      113 4.615e+09 1.088e+09
## 5             HAIL          9      731 1.892e+09 8.938e+08
## 6             HEAT        701      878 2.770e+05 4.013e+08
## 7     EXTREME COLD        112      181 6.313e+07 3.547e+08
## 8        HURRICANE         37       17 1.503e+09 3.528e+08
## 9           FREEZE          1        0 5.000e+03 3.090e+08
## 10 DAMAGING FREEZE          0        0 8.000e+06 2.621e+08
```

