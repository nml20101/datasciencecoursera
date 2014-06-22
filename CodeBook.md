## Getting and Cleaning Data Code Book ##
This is a code book that describes data source, the variables, the data, and transformations 
and work that you performed to clean up the data for the class project on Coursera's
Getting and Cleaning Data.
### Data Source ###
The data represents the data
collected from the accelerometers from the Samsung Galaxy S smartphone.
URL is https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 
### Variables ###
Out of 561 variables, we selected
79 based on mean and std requirement. We added activity and subject variables to the tidy data sets, so the total number of variables is 81.

### Observations ###
* Activities contained in activity_labels.txt file. 

	* 1	WALKING
	* 2	WALKING_UPSTAIRS
	* 3	WALKING_DOWNSTAIRS
	* 4	SITTING
	* 5	STANDING
	* 6	LAYING

* Subjects information is contained in subject_train.txt and subject__test.txt files. Subjects are labeled 1 to 30 (integers).
* Variables in the tidy data sets are:
  * 1 activity
  * 2 subject
  * 3 tBodyAcc-mean()-X
  * 4 tBodyAcc-mean()-Y
  * 5 tBodyAcc-mean()-Z
  * 6 tBodyAcc-std()-X
  * 7 tBodyAcc-std()-Y
  * 8 tBodyAcc-std()-Z
  * 9 tGravityAcc-mean()-X
  * 10 tGravityAcc-mean()-Y
  * 11 tGravityAcc-mean()-Z
  * 12 tGravityAcc-std()-X
  * 13 tGravityAcc-std()-Y
  * 14 tGravityAcc-std()-Z
  * 15 tBodyAccJerk-mean()-X
  * 16 tBodyAccJerk-mean()-Y
  * 17 tBodyAccJerk-mean()-Z
  * 18 tBodyAccJerk-std()-X
  * 19 tBodyAccJerk-std()-Y
  * 20 tBodyAccJerk-std()-Z
  * 21 tBodyGyro-mean()-X 
  * 22 tBodyGyro-mean()-Y
  * 23 tBodyGyro-mean()-Z
  * 24 tBodyGyro-std()-X
  * 25 tBodyGyro-std()-Y
  * 26 tBodyGyro-std()-Z
  * 27 tBodyGyroJerk-mean()-X
  * 28 tBodyGyroJerk-mean()-Y
  * 29 tBodyGyroJerk-mean()-Z
  * 30 tBodyGyroJerk-std()-X
  * 31 tBodyGyroJerk-std()-Y
  * 32 tBodyGyroJerk-std()-Z
  * 33 tBodyAccMag-mean()
  * 34 tBodyAccMag-std()
  * 35 tGravityAccMag-mean()
  * 36 tGravityAccMag-std()
  * 37 tBodyAccJerkMag-mean()
  * 38 tBodyAccJerkMag-std()
  * 39 tBodyGyroMag-mean()
  * 40 tBodyGyroMag-std()
  * 41 tBodyGyroJerkMag-mean()
  * 42 tBodyGyroJerkMag-std()
  * 43 fBodyAcc-mean()-X
  * 44 fBodyAcc-mean()-Y
  * 45 fBodyAcc-mean()-Z
  * 46 fBodyAcc-std()-X
  * 47 fBodyAcc-std()-Y
  * 48 fBodyAcc-std()-Z
  * 49 fBodyAcc-meanFreq()-X
  * 50 fBodyAcc-meanFreq()-Y
  * 51 fBodyAcc-meanFreq()-Z
  * 52 fBodyAccJerk-mean()-X
  * 53 fBodyAccJerk-mean()-Y
  * 54 fBodyAccJerk-mean()-Z
  * 55 fBodyAccJerk-std()-X
  * 56 fBodyAccJerk-std()-Y
  * 57 fBodyAccJerk-std()-Z
  * 58 fBodyAccJerk-meanFreq()-X
  * 59 fBodyAccJerk-meanFreq()-Y
  * 60 fBodyAccJerk-meanFreq()-Z
  * 61 fBodyGyro-mean()-X
  * 62 fBodyGyro-mean()-Y
  * 63 fBodyGyro-mean()-Z
  * 64 fBodyGyro-std()-X
  * 65 fBodyGyro-std()-Y
  * 66 fBodyGyro-std()-Z
  * 67 fBodyGyro-meanFreq()-X
  * 68 fBodyGyro-meanFreq()-Y
  * 69 fBodyGyro-meanFreq()-Z
  * 70 fBodyAccMag-mean()
  * 71 fBodyAccMag-std()
  * 72 fBodyAccMag-meanFreq()
  * 73 fBodyBodyAccJerkMag-mean()
  * 74 fBodyBodyAccJerkMag-std()
  * 75 fBodyBodyAccJerkMag-meanFreq()
  * 76 fBodyBodyGyroMag-mean()
  * 77 fBodyBodyGyroMag-std()
  * 78 fBodyBodyGyroMag-meanFreq()
  * 79 fBodyBodyGyroJerkMag-mean()
  * 80 fBodyBodyGyroJerkMag-std()
  * 81 fBodyBodyGyroJerkMag-meanFreq()


### Transformations ###
* Use download.file function to get zip file form the url : https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 
Unzip the zipped file using unzip function
* This will create a directory: “./UCI HAR Dataset” in your current working directory where the run_analysis.R script is saved.
* Read files into data.frames using read.table function
* There are 8 data frames:
 * activityLabels = UCI HAR Dataset/activity_labels.txt
 * features = UCI HAR Dataset/features.txt
 * Xtest = UCI HAR Dataset/test/X_test.txt
 * Xtrain = UCI HAR Dataset/train/X_train.txt
 * subjectTest = UCI HAR Dataset/test/subject_test.txt
 * subjectTrain = UCI HAR Dataset/train/subject_train.txt
 * ytest = UCI HAR Dataset/test/y_test.txt
 * ytrain = UCI HAR Dataset/train/y_train.txt
* Subset features that contain mean or std
* Use grep to select indices in features$V2 (second column) that have mean and std
* Knowing the indices, subset Xtrain and Xtest, and features 
* Covert subsetted features to character values
* Add 2 columns to Xtrain and Xtest: subject (from subjectxxx.txt) and activity (from y(xxx))
* Create labels for new columns by creating a new vector feaSubNew
* Add new labels using colnames function
* Merge data using rbind
* Sort data by subject and activity using order function
* Write tidy data using write.table or write.csv function
 * This data set is called tidyData1.txt
* The next step is to perform mean calculations for the columns by the subject:
 * Use split function to get a list by subject and loop over subject and perform colMeans to get averages for each subject at given activity
 * This produces TidyAverages.txt data set.

## Tidy Data Sets ##
* tidyData1.txt dimension is  10299x81
* TidyAverages.txt dimension is 180x81
 

