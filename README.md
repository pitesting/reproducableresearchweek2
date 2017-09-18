
reproducableresearchweek2

It is now possible to collect a large amount of data about personal movement using activity monitoring devices such as a Fitbit, Nike Fuelband, or Jawbone Up. These type of devices are part of the "quantified self" movement -- a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. But these data remain under-utilized both because the raw data are hard to obtain and there is a lack of statistical methods and software for processing and interpreting the data.

This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.


__Code for reading in the dataset and/or processing the data__
See line 23 of the Rscript File: 
*> activity  <- read.csv("./activity.csv", stringsAsFactors = F)*

__Histogram of the total number of steps taken each day__
See RPlot01.png
Line 78 onwards

__Mean and median number of steps taken each day__
See line 109 onwards of the Rscript File
mean(sum_data$total)
median(sum_data$total)
These formulas gives a mean and median of __10766 and 10766__ respectively.

__Time series plot of the average number of steps taken__
See line 140 onwards
Also RPlot02.png

__The 5-minute interval that, on average, contains the maximum number of steps__
170 onwards in Rscrip file 
The number of NA’s is 2304.

__Code to describe and show a strategy for imputing missing data__
Lines 68 onwards

__Histogram of the total number of steps taken each day after missing values are imputed__
Rplot03.png
Lines 68 onwards

__Panel plot comparing the average number of steps taken per 5-minute interval across weekdays and weekends__
Lines 249 Onwards
RPlot04.png
msbi2 <- aggregate(act$steps, by=list(act$interval, act$wday),mean)
names(msbi2) <- c("interval", "wday", "steps")
xyplot(steps ~ interval | wday, msbi2, type = "l", layout = c(1,2),
       xlab = "5-Minute Interval", ylab = "Number of Steps")

__All of the R code needed to reproduce the results (numbers, plots, etc.) in the report__
Rscript File 



Workings Below
Question 
Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)
Clear the workspace
rm(sum_data)

Compute the means of steps accross all days for each interval
mean_data <- aggregate(activity$steps, 
                       by=list(activity$interval), 
                       FUN=mean, 
                       na.rm=TRUE)

Rename the attributes
names(mean_data) <- c("interval", "mean")

head(mean_data)
Compute the time series plot
plot(mean_data$interval, 
     mean_data$mean, 
     type="l", 
     col="blue", 
     lwd=2, 
     xlab="Interval [minutes]", 
     ylab="Average number of steps", 
     main="Time-series of the average number of steps per intervals\n(NA removed)")



Question 2
Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?
The 5-minute interval that contains the maximum of steps, on average across all days, is 835.

The number of NA’s is 2304.


Make a histogram of the total number of steps taken each day and calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?
Compute the total number of steps each day (NA values removed)
sum_data <- aggregate(activity$steps, by=list(activity$date), FUN=sum)

Rename the attributes
names(sum_data) <- c("date", "total")

Compute the histogram of the total number of steps each day
hist(sum_data$total, 
     breaks=seq(from=0, to=25000, by=2500),
     col="blue", 
     xlab="Total number of steps", 
     ylim=c(0, 30), 
     main="Histogram of the total number of steps taken each day\n(NA replaced by mean value)")
     
__The mean and median are computed like__

mean(sum_data$total)
median(sum_data$total)
These formulas gives a mean and median of __10766 and 10766__ respectively.

These values differ greatly from the estimates from the first part of the assignment. The impact of imputing the missing values is to have more data, hence to obtain a bigger mean and median value.
