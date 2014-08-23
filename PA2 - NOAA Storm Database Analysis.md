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
#data<-read.csv("data/repdata-data-StormData.csv.bz2",nrows=5000)
data<-read.csv(bzfile("data/repdata-data-StormData.csv.bz2"),header=TRUE, nrows=5000)
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

head(stormData)
```

```
##    EVTYPE FATALITIES INJURIES PROPDMG CROPDMG
## 1 TORNADO          0       15   25000       0
## 2 TORNADO          0        0    2500       0
## 3 TORNADO          0        2   25000       0
## 4 TORNADO          0        2    2500       0
## 5 TORNADO          0        2    2500       0
## 6 TORNADO          0        6    2500       0
```

## Results
