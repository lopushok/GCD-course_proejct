# Getting and Cleaning Data - course proejct

1. **Read** all the files we need into different variables:

X_train <- read.table("./UCI HAR Dataset/train/X_train.txt") <br>
Y_train <- read.table("./UCI HAR Dataset/train/y_train.txt") <br>
S_train <- read.table("./UCI HAR Dataset/train/subject_train.txt") <br>
S_test <- read.table("./UCI HAR Dataset/test/subject_test.txt") <br>
Y_test <- read.table("./UCI HAR Dataset/test/y_test.txt") <br>
X_test <- read.table("./UCI HAR Dataset/test/X_test.txt") <br>
column.names <- read.table("./UCI HAR Dataset/features.txt") <br>
activity.labels <- read.table("./UCI HAR Dataset/activity_labels.txt") <br>

2. Create one big dataset of 563 variables. First we **cbind** *train* and *test* data sets from three files, than **rbind** them up together: 1:561 from X data set, than Y data set and subject data set:

data <- rbind(cbind(X_test, Y_test, S_test), cbind(X_train, Y_train, S_train)) 

3. Than we **separate the column names** we need in our clean data. They are containing *"mean()"* and *"std()"* in their names. Be careful - only *"mean()"*, not *"mean"*, because their are column names with *"meanFreq()"*, that we actually don't need. So first we **subset** the colnames with *"mean()"*, than **cbind** it with colnames with *"std()"* and finally arrange them in right order (on it's number):

cn <- column.names[grep("mean()", column.names$V2, fixed=TRUE), ] <br>
cn <- rbind(cn, column.names[grep("std()", column.names$V2, fixed=TRUE), ]) <br>
cn <- cn[order(cn$V1),] <br>

4. Next step is to **subset from one big data** we created on step 2 only columns we need (they are on the mean and standard deviation for each measurement - exactly that column names and numbers we received on step 3). So we subset 66 columns with measures we are interested in and the last 2 columns from big data set - they are activity id and subject id.

newdata <- data[ , c(cn$V1, 562, 563)] <br>

5. 

colnames(newdata) <- c(as.character(cn$V2), "activity_name", "subject_id") <br>

newdata[["activity_name"]] <- activity.labels[match(newdata[["activity_name"]], activity.labels[['V1']] ) , 'V2']

 # replacing activity id with activity name

library(plyr)

outcome <- ddply(newdata, c("activity_name", "subject_id"), numcolwise(mean))

