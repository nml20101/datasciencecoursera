---
title: "Peer Assessment 1 - Reproducible Reseach"
author: "Naida Lacevic"
date: "Thursday, August 14, 2014"
output: html_document
---
Analysis code for the assignment


```r
library(knitr)
library(markdown)
library(plyr)
library(lattice)
library(reshape2)

if(!file.exists("./data")){dir.create("./data")}
fileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
download.file(fileUrl, destfile = "./data/Dataset.zip", method="curl", mode="wb" )
```

```
## Warning: running command 'curl  "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"  -o "./data/Dataset.zip"' had status 127
## Warning: download had nonzero exit status
```

```r
dateDownloaded <- date()
print(dateDownloaded)
```

```
## [1] "Sat Aug 16 17:46:36 2014"
```

```r
zipfile <- "./data/Dataset.zip"
unzip(zipfile)
```
Loading and preprocessing the data

```r
activityData <- read.csv("activity.csv",stringsAsFactors=FALSE)
```
Part 1: What is mean total number of steps taken per day?

1. Make a histogram of the total number of steps taken each day

```r
total_step_day <- aggregate(steps ~ date, data = activityData, sum)
png(file="plot1.png", width=480, height=480)
barplot(total_step_day[,2], xlab = "Total Number of Steps", ylab="Frequency")
dev.off()
```

```
## pdf 
##   2
```
2. Calculate and report the mean and median total number of steps taken per day


```r
mean_spd <- mean(total_step_day[,2])
mean_spd
```

```
## [1] 10766
```

```r
median_spd <- median(total_step_day[,2])
median_spd
```

```
## [1] 10765
```


Part 2: What is the average daily activity pattern?

1. Make a time series plot of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
cdata <- ddply(activityData, c("interval"), summarise,mean = mean(steps, na.rm=TRUE))
png(file="plot2.png", width=480, height=480)
plot(cdata[,1], cdata[,2], type="l", ylab = "Mean Number of Steps", xlab="Interval")
dev.off()
```

```
## pdf 
##   2
```

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
max_int <- cdata[which.max(cdata[,2]),1]
```
The interval with maximum number of steps is 835.

Part 3: Imputing missing values

1. Calculate and report the total number of missing values
in the dataset (i.e. the total number of rows with NAs)


```r
n_na <- table(is.na(activityData$steps))
n_na[2]
```

```
## TRUE 
## 2304
```
The total number of rows with NAs is 2304.

2. Devise a strategy for filling in all of the missing values in the dataset.

I'll use mean value for a given interval and replace NA that correspond 
to that interval:

Get indices which contain NA in steps


```r
inan1 <- which(is.na(activityData$step))
```
Get intervals for indices which have NA in steps

```r
intnan1 <- activityData$interval[inan1]
```
Get list of indices of mean values corresponding to list of intervals that have NA in steps

```r
milst1 <- match(intnan1,cdata$interval)
```
Get mean values for intervals

```r
meanmilst1 <- cdata$mean[milst1]
```
Copy data

```r
adat2 <- activityData
```
Set step values which were previously NA to means

```r
adat2$steps[inan1] <- meanmilst1
```
3. Create a new dataset that is equal to the original dataset but with the missing data filled in.

The new set dataset is stored in adat2 dataframe.

4. Make a histogram of the total number of steps taken each day and calculate and report the mean and median total number of steps taken per day.


```r
total_step_day_2 <- aggregate(steps ~ date, data = adat2, sum)
png(file="plot3.png", width=480, height=480)
barplot(total_step_day_2[,2],xlab = "Total Number of Steps", ylab="Frequency" )
dev.off()
```

```
## pdf 
##   2
```

```r
mean_spd_2 <- mean(total_step_day_2[,2])
mean_spd_2
```

```
## [1] 10766
```

```r
median_spd_2 <- median(total_step_day_2[,2])
median_spd_2
```

```
## [1] 10766
```

The difference in mean is 0 and the difference in median 
is 1.1887. So, if we replace NA with 5 min interval means, the mean value is not changing, while median is changing. This is somewhat surprising. 

Part 4. Are there differences in activity patterns between weekdays and weekends?

Create function that returns Weekend or Weekday value as a function of a day

```r
wd1 <- function(day) { if (day %in% c("Monday","Tuesday","Wednesday","Thursday","Friday")) {return("Weekday")} else {return("Weekend")} }
wd1("Tuesday")
```

```
## [1] "Weekday"
```
Create array that contains characters "Weekend" or "Weekday"

```r
col4 <- sapply(weekdays(as.Date(adat2$date)), wd1)
length(col4)
```

```
## [1] 17568
```
Add col4 to adat2 dataframe as a 4th column

```r
adat3 <- cbind(adat2, col4)
```
Subset data sets for weekend and weekday

```r
adat3_weekday <- subset(adat3, col4 == "Weekday")
adat3_weekend <- subset(adat3, col4 == "Weekend")
```
Compute averages like in Part 2, question 1.

```r
cdata_weekend <- ddply(adat3_weekend, c("interval"), 
                       summarise,mean = mean(steps, na.rm=TRUE))
cdata_weekday <- ddply(adat3_weekday, c("interval"), summarise,mean = mean(steps, na.rm=TRUE))
```

Rename column names

```r
colnames(cdata_weekday) <- c("interval", "mean_step_weekday")
colnames(cdata_weekend) <- c("interval", "mean_step_weekend")
```
Merge dataframe, reshape it to plot using lattice system

```r
weekend_v <- rep("Weekend", dim(cdata_weekend)[1])
weekday_v <- rep("Weekday", dim(cdata_weekday)[1])
df4 <- cbind(cdata_weekday,weekday_v)
df5 <- cbind(cdata_weekend,weekend_v)
colnames(df4) <- c("interval", "mean_step", "whatD")
colnames(df5) <- c("interval", "mean_step", "whatD")
total_df <- rbind(df4,df5)
str(total_df)
```

```
## 'data.frame':	576 obs. of  3 variables:
##  $ interval : int  0 5 10 15 20 25 30 35 40 45 ...
##  $ mean_step: num  2.251 0.445 0.173 0.198 0.099 ...
##  $ whatD    : Factor w/ 2 levels "Weekday","Weekend": 1 1 1 1 1 1 1 1 1 1 ...
```
Plot the data using lattice system

```r
png(file="plot4.png", width=480, height=480)
xyplot(total_df$mean_step ~ total_df$interval | total_df$whatD, 
       layout = c(1, 2), type='l', xlab = "Interval", ylab="Average Number of Steps")
dev.off()
```

```
## pdf 
##   2
```
```

