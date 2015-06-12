# Reproducible Research: Peer Assessment 1

## Loading and preprocessing the data
- The format of raw data is **data.frame** , so there is no need for preprocessing


```r
rawData <-read.csv("D:/learning software and movies//COURSERA/Reproducible Research/Data For Assignments/activity.csv")
```
## What is mean total number of steps taken per day?
- First, aggregating the total number of steps per day

```r
totalStepsPerDay <- aggregate(rawData$steps, by=list(date=rawData$date),FUN=sum,na.rm=TRUE)
```

- After that, drawing the histogram

```r
hist(totalStepsPerDay$x, 
     breaks=nrow(totalStepsPerDay),
     main = paste("Histogram of Total Steps Per Day"),
     xlab = "Total Steps Per Day")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

- Finally, calculating the mean and median

```r
meanTotal <- mean(totalStepsPerDay$x)
medianTotal <- median(totalStepsPerDay$x)
```
**mean**

```
## [1] 9354.23
```

**median**

```
## [1] 10395
```

## What is the average daily activity pattern?
- Finding the daily activity pattern for intervals and plotting the results

```r
dailyActivity <- aggregate(rawData$steps, by=list(interval=rawData$interval),FUN=mean,na.r=TRUE)
plot(dailyActivity$interval,dailyActivity$x,type="l",xlab = "Daily Interval",ylab = "Average Steps for All Days")
```

![](PA1_template_files/figure-html/unnamed-chunk-7-1.png) 

- Now, finding the the interval with maximum number of taken steps

```r
maxDailyInterval <- dailyActivity[which.max( dailyActivity$x ),1]
```
**The Interval**

```
## [1] 835
```
## Imputing missing values

- Calculate and report the total number of missing values in the dataset

```r
sum(is.na(rawData))
```

```
## [1] 2304
```

- Devise a strategy for filling in all of the missing values in the dataset.

      - **mean for that 5-minute interval**

## Are there differences in activity patterns between weekdays and weekends?
