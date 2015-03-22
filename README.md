# Getting and Cleaning Data - course proejct

## Some information about the data set, used in this course project

### Human Activity Recognition Using Smartphones Dataset

**Version 1.0**

Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio, Luca Oneto.
Smartlab - Non Linear Complex Systems Laboratory
DITEN - Università degli Studi di Genova.
Via Opera Pia 11A, I-16145, Genoa, Italy.
activityrecognition@smartlab.ws
www.smartlab.ws

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details. 

### For each record it is provided:

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

### The dataset includes the following files:

- 'README.txt'
- 'features_info.txt': Shows information about the variables used on the feature vector.
- 'features.txt': List of all features.
- 'activity_labels.txt': Links the class labels with their activity name.
- 'train/X_train.txt': Training set.
- 'train/y_train.txt': Training labels.
- 'test/X_test.txt': Test set.
- 'test/y_test.txt': Test labels.

The following files are available for the train and test data. Their descriptions are equivalent. 

- 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 
- 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer X axis in standard gravity units 'g'. Every row shows a 128 element vector. The same description applies for the 'total_acc_x_train.txt' and 'total_acc_z_train.txt' files for the Y and Z axis. 
- 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting the gravity from the total acceleration. 
- 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope for each window sample. The units are radians/second. 

## The course project was to

Create one R script called ``run_analysis.R`` that does the following:

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names. 
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

## The files used for the course project are

- 'features.txt': List of all features.
- 'activity_labels.txt': Links the class labels with their activity name.
- 'train/X_train.txt': Training set.
- 'train/y_train.txt': Training labels.
- 'test/X_test.txt': Test set.
- 'test/y_test.txt': Test lables.
- 'train/subject_train.txt': The subject who performed the activity for each train window sample.
- 'test/subject_test.txt': The subject who performed the activity for each test window sample.

## The steps of the run_analysis.R scipt

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
