# Getting and Cleaning Data - course proejct

1. **Read** all the files we need into different variables:

```
X_train <- read.table("./UCI HAR Dataset/train/X_train.txt")
Y_train <- read.table("./UCI HAR Dataset/train/y_train.txt") 
S_train <- read.table("./UCI HAR Dataset/train/subject_train.txt") 
S_test <- read.table("./UCI HAR Dataset/test/subject_test.txt")
Y_test <- read.table("./UCI HAR Dataset/test/y_test.txt") 
X_test <- read.table("./UCI HAR Dataset/test/X_test.txt") 
column.names <- read.table("./UCI HAR Dataset/features.txt") 
activity.labels <- read.table("./UCI HAR Dataset/activity_labels.txt") 
```

2\. Create one big dataset of 563 variables. First we **cbind** *train* and *test* data sets from three files, than **rbind** them up together: 1:561 from X data set, than Y data set and subject data set:

```
data <- rbind(cbind(X_test, Y_test, S_test), cbind(X_train, Y_train, S_train)) 
```

3\. Then we **separate the column names** we need in our clean data. They are containing *"mean()"* and *"std()"* in their names. Be careful - only *"mean()"*, not *"mean"*, because their are column names with *"meanFreq()"*, that we actually don't need. So first we **subset** the colnames with *"mean()"*, than **cbind** it with colnames with *"std()"* and finally arrange them in right order (on it's number):

```
cn <- column.names[grep("mean()", column.names$V2, fixed=TRUE), ] 
cn <- rbind(cn, column.names[grep("std()", column.names$V2, fixed=TRUE), ]) 
cn <- cn[order(cn$V1),] <br>
```

4\. Next step is to **subset from one big data** we created on step 2 only columns we need (they are on the mean and standard deviation for each measurement - exactly that column names and numbers we received on step 3). So we subset 66 columns with measures we are interested in and the last 2 columns from big data set - they are activity id and subject id.

```
newdata <- data[ , c(cn$V1, 562, 563)] <br>
```

5\. After that we should **set the right columnames** - they are from the data set from our third step.

```
colnames(newdata) <- c(as.character(cn$V2), "activity_name", "subject_id") <br>
```

6\. Then - **set activity names** instead of activity ids. So we **match** our data from 5 step with *activity.labels* data on the *id*.

```
newdata[["activity_name"]] <- activity.labels[match(newdata[["activity_name"]], activity.labels[['V1']] ) , 'V2']
```

7\. And the final step - create the *outcome* data set. With the average of each variable (each column) for each activity name and each subject id.

```
library(plyr)
outcome <- ddply(newdata, c("activity_name", "subject_id"), numcolwise(mean))
```
