#Reproduciple Research: Peer Assesment 1


```r
library(lattice)
```


Loading the data:


```r
activityData <- activity <- read.csv("activity.csv")
```
### What is the total number of steps taken each day?
Calculate total number of steps taken per day.

```r
totalSteps <- aggregate(steps ~ date, data = activityData, FUN = sum)
```
Make histogram of the total number of steps taken each day.

```r
barplot(totalSteps$steps, names.arg = totalSteps$date, xlab = "Date", ylab = "Steps")
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png) 


Calculate mean and median of the total number of steps taken per day.

```r
mean(totalSteps$steps)
```

```
## [1] 10766.19
```

```r
median(totalSteps$steps)
```

```
## [1] 10765
```
### What is the average daily pattern?
A time series of plot of 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

```r
stepsAverage <- aggregate(steps ~ interval, data = activityData, FUN = mean)
plot(stepsAverage, type = "l")
```

![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8-1.png) 
Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
stepsAverage$interval[which.max(stepsAverage$steps)]
```

```
## [1] 835
```
###Imputing missing values
Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

```r
sum(is.na(activityData))
```

```
## [1] 2304
```
Fill missing values by using mean for the 5 minutes interval.

```r
imputeData <- activityData 
for (i in 1:nrow(imputeData)) {
    if (is.na(imputeData$steps[i])) {
        imputeData$steps[i] <- stepsAverage[which(imputeData$interval[i] == stepsAverage$interval), ]$steps
    }
}
```
Make sure that missing values have been imputed.

```r
sum(is.na(imputeData))
```

```
## [1] 0
```
Make new data set for filled data averages.

```r
totalStepsImp <- aggregate(steps ~ date, data = imputeData, FUN = sum)
```
Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

```r
barplot(totalStepsImp$steps, names.arg = totalStepsImp$date, xlab = "Date", ylab = "Steps")
```

![plot of chunk unnamed-chunk-14](figure/unnamed-chunk-14-1.png) 

Calculate mean and median of the total number of steps taken per day for the imputed data.

```r
mean(totalSteps$steps)
```

```
## [1] 10766.19
```

```r
median(totalSteps$steps)
```

```
## [1] 10765
```
Noticable differences can not be interpreted from the histogram or from mean or median values for imputed data, when compared to the results of first part of the assignment.
### Are there differences in activity patterns between weekdays and weekends?
A new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.

```r
imputeData$weekday = weekdays(as.Date(imputeData$date, format = "%Y-%m-%d"))
imputeData$weekday.type = factor(ifelse(imputeData$weekday == "Sunday" | imputeData$weekday == 
    "Saturday", "weekend", "weekday"), levels = c("weekday", "weekend"))
```
Panel plot containing average number of steps taken, averaged across all weekday days or weekend days. Dunno why the weekend part (top) of plot is not showing...in R Studio shows ok.

```r
stepsAverageNew <- aggregate(steps ~ interval + weekday.type, data = imputeData, mean)
```

```r
xyplot(steps ~ interval | weekday.type, stepsAverageNew, type = "l", layout = c(1, 2), 
    xlab = "Interval", ylab = "Number of steps")
```

![plot of chunk unnamed-chunk-20](figure/unnamed-chunk-20-1.png) 
knit2htlm("##Reproduciple Research: Peer Assesment 1


```r
library(lattice)
```


Loading the data:


```r
activityData <- activity <- read.csv("activity.csv")
```
### What is the total number of steps taken each day?
Calculate total number of steps taken per day.

```r
totalSteps <- aggregate(steps ~ date, data = activityData, FUN = sum)
```
Make histogram of the total number of steps taken each day.

```r
barplot(totalSteps$steps, names.arg = totalSteps$date, xlab = "Date", ylab = "Steps")
```

![plot of chunk unnamed-chunk-24](figure/unnamed-chunk-24-1.png) 


Calculate mean and median of the total number of steps taken per day.

```r
mean(totalSteps$steps)
```

```
## [1] 10766.19
```

```r
median(totalSteps$steps)
```

```
## [1] 10765
```
### What is the average daily pattern?
A time series of plot of 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

```r
stepsAverage <- aggregate(steps ~ interval, data = activityData, FUN = mean)
plot(stepsAverage, type = "l")
```

![plot of chunk unnamed-chunk-28](figure/unnamed-chunk-28-1.png) 
Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
stepsAverage$interval[which.max(stepsAverage$steps)]
```

```
## [1] 835
```
###Imputing missing values
Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

```r
sum(is.na(activityData))
```

```
## [1] 2304
```
Fill missing values by using mean for the 5 minutes interval.

```r
imputeData <- activityData 
for (i in 1:nrow(imputeData)) {
    if (is.na(imputeData$steps[i])) {
        imputeData$steps[i] <- stepsAverage[which(imputeData$interval[i] == stepsAverage$interval), ]$steps
    }
}
```
Make sure that missing values have been imputed.

```r
sum(is.na(imputeData))
```

```
## [1] 0
```
Make new data set for filled data averages.

```r
totalStepsImp <- aggregate(steps ~ date, data = imputeData, FUN = sum)
```
Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

```r
barplot(totalStepsImp$steps, names.arg = totalStepsImp$date, xlab = "Date", ylab = "Steps")
```

![plot of chunk unnamed-chunk-34](figure/unnamed-chunk-34-1.png) 

Calculate mean and median of the total number of steps taken per day for the imputed data.

```r
mean(totalSteps$steps)
```

```
## [1] 10766.19
```

```r
median(totalSteps$steps)
```

```
## [1] 10765
```
Noticable differences can not be interpreted from the histogram or from mean or median values for imputed data, when compared to the results of first part of the assignment.
### Are there differences in activity patterns between weekdays and weekends?
A new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.

```r
imputeData$weekday = weekdays(as.Date(imputeData$date, format = "%Y-%m-%d"))
imputeData$weekday.type = factor(ifelse(imputeData$weekday == "Sunday" | imputeData$weekday == 
    "Saturday", "weekend", "weekday"), levels = c("weekday", "weekend"))
```
Panel plot containing average number of steps taken, averaged across all weekday days or weekend days. Knitted output is not showing the weekend part (top) of the plot. In R Studio it's ok...

```r
stepsAverageNew <- aggregate(steps ~ interval + weekday.type, data = imputeData, mean)
```

```r
xyplot(steps ~ interval | weekday.type, stepsAverageNew, type = "l", layout = c(1, 2), 
    xlab = "Interval", ylab = "Number of steps")
```

![plot of chunk unnamed-chunk-40](figure/unnamed-chunk-40-1.png) 





