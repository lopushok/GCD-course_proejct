## The original data set

could be found here: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

## Feature Selection for the original data set used in this data cleaning project

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

* tBodyAcc-XYZ
* tGravityAcc-XYZ
* tBodyAccJerk-XYZ
* tBodyGyro-XYZ
* tBodyGyroJerk-XYZ
* tBodyAccMag
* tGravityAccMag
* tBodyAccJerkMag
* tBodyGyroMag
* tBodyGyroJerkMag
* fBodyAcc-XYZ
* fBodyAccJerk-XYZ
* fBodyGyro-XYZ
* fBodyAccMag
* fBodyAccJerkMag
* fBodyGyroMag
* fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

* mean(): Mean value
* std(): Standard deviation
* mad(): Median absolute deviation 
* max(): Largest value in array
* min(): Smallest value in array
* sma(): Signal magnitude area
* energy(): Energy measure. Sum of the squares divided by the number of values. 
* iqr(): Interquartile range 
* entropy(): Signal entropy
* arCoeff(): Autorregresion coefficients with Burg order equal to 4
* correlation(): correlation coefficient between two signals
* maxInds(): index of the frequency component with largest magnitude
* meanFreq(): Weighted average of the frequency components to obtain a mean frequency
* skewness(): skewness of the frequency domain signal 
* kurtosis(): kurtosis of the frequency domain signal 
* bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
* angle(): Angle between to vectors.

## Steps procedeed on data to receive outcome.txt

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names. 
5. From the data set in step 4, creates a second, independent tidy data set ('outcome') with the average of each variable for each activity and each subject.

## Description of the variable names in outcome data set

01\. "activity_name" - factor 1:6 - names of activities performed by 30 subjects of the measurements (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING)<br>
02\. "subject_id" - factor 1:30 - ids for subjects of the measurements

Other 66 variables are means of the measurements called in the column name by activity name and subject id. All numeric.

03\. "tBodyAcc-mean()-X"<br>
04\. "tBodyAcc-mean()-Y"<br>
05\. "tBodyAcc-mean()-Z"<br>
06\. "tBodyAcc-std()-X"<br>
07\. "tBodyAcc-std()-Y"<br>
08\. "tBodyAcc-std()-Z"<br>
09\. "tGravityAcc-mean()-X"<br>
10\. "tGravityAcc-mean()-Y"<br>
11\. "tGravityAcc-mean()-Z"<br>
12\. "tGravityAcc-std()-X"<br>
13\. "tGravityAcc-std()-Y"<br>
14\. "tGravityAcc-std()-Z"<br>
15\. "tBodyAccJerk-mean()-X"<br>
16\. "tBodyAccJerk-mean()-Y"<br>
17\. "tBodyAccJerk-mean()-Z"<br>
18\. "tBodyAccJerk-std()-X"<br>
19\. "tBodyAccJerk-std()-Y"<br>
20\. "tBodyAccJerk-std()-Z"<br>
21\. "tBodyGyro-mean()-X"<br>
22\. "tBodyGyro-mean()-Y" <br>
23\. "tBodyGyro-mean()-Z"<br>
24\. "tBodyGyro-std()-X"<br>
25\. "tBodyGyro-std()-Y"<br>
26\. "tBodyGyro-std()-Z"<br>
27\. "tBodyGyroJerk-mean()-X"<br>
28\. "tBodyGyroJerk-mean()-Y"<br>
29\. "tBodyGyroJerk-mean()-Z" <br>
30\. "tBodyGyroJerk-std()-X"<br>
31\. "tBodyGyroJerk-std()-Y"<br>
32\. "tBodyGyroJerk-std()-Z"<br>
33\. "tBodyAccMag-mean()" <br>
34\. "tBodyAccMag-std()" <br>
35\. "tGravityAccMag-mean()" <br>
36\. "tGravityAccMag-std()" <br>
37\. "tBodyAccJerkMag-mean()"<br>
38\. "tBodyAccJerkMag-std()" <br>
39\. "tBodyGyroMag-mean()" <br>
40\. "tBodyGyroMag-std()" <br>
41\. "tBodyGyroJerkMag-mean()"<br> 
42\. "tBodyGyroJerkMag-std()" <br>
43\. "fBodyAcc-mean()-X" <br>
44\. "fBodyAcc-mean()-Y" <br>
45\. "fBodyAcc-mean()-Z" <br>
46\. "fBodyAcc-std()-X" <br>
47\. "fBodyAcc-std()-Y"<br>
48\. "fBodyAcc-std()-Z" <br>
49\. "fBodyAccJerk-mean()-X"<br> 
50\. "fBodyAccJerk-mean()-Y" <br>
51\. "fBodyAccJerk-mean()-Z" <br>
52\. "fBodyAccJerk-std()-X" <br>
53\. "fBodyAccJerk-std()-Y" <br>
54\. "fBodyAccJerk-std()-Z" <br>
55\. "fBodyGyro-mean()-X"<br>
56\. "fBodyGyro-mean()-Y" <br>
57\. "fBodyGyro-mean()-Z" <br>
58\. "fBodyGyro-std()-X" <br>
59\. "fBodyGyro-std()-Y" <br>
60\. "fBodyGyro-std()-Z" <br>
61\. "fBodyAccMag-mean()" <br>
62\. "fBodyAccMag-std()" <br>
63\. "fBodyBodyAccJerkMag-mean()"<br> 
64\. "fBodyBodyAccJerkMag-std()"<br>
65\. "fBodyBodyGyroMag-mean()"<br>
66\. "fBodyBodyGyroMag-std()" <br>
67\. "fBodyBodyGyroJerkMag-mean()"<br>
68\. "fBodyBodyGyroJerkMag-std()"<br>
