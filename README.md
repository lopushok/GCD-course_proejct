# Getting and Cleaning Data - course proejct


X_train <- read.table("./UCI HAR Dataset/train/X_train.txt")
Y_train <- read.table("./UCI HAR Dataset/train/y_train.txt")
S_train <- read.table("./UCI HAR Dataset/train/subject_train.txt")
S_test <- read.table("./UCI HAR Dataset/test/subject_test.txt")
Y_test <- read.table("./UCI HAR Dataset/test/y_test.txt")
X_test <- read.table("./UCI HAR Dataset/test/X_test.txt")
column.names <- read.table("./UCI HAR Dataset/features.txt")
activity.labels <- read.table("./UCI HAR Dataset/activity_labels.txt")

 # we've read all the files we need

data <- rbind(cbind(X_test, Y_test, S_test), cbind(X_train, Y_train, S_train)) # creating one big dataset with 563 variables

cn <- column.names[grep("mean()", column.names$V2, fixed=TRUE), ]
cn <- rbind(cn, column.names[grep("std()", column.names$V2, fixed=TRUE), ]) # only column names, we need
cn <- cn[order(cn$V1),] # in rigth order

newdata <- data[ , c(cn$V1, 562, 563)] # subsetting only variables on mean and std + activity and subject

colnames(newdata) <- c(as.character(cn$V2), "activity_name", "subject_id") # setting column names

newdata[["activity_name"]] <- activity.labels[match(newdata[["activity_name"]], activity.labels[['V1']] ) , 'V2']

 # replacing activity id with activity name

library(plyr)

outcome <- ddply(newdata, c("activity_name", "subject_id"), numcolwise(mean))

