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
 * activity
  * subject
  * tBodyAcc-mean()-X
  * tBodyAcc-mean()-Y
  * tBodyAcc-mean()-Z
  * tBodyAcc-std()-X"
  * tBodyAcc-std()-Y"
  * tBodyAcc-std()-Z"
  * tGravityAcc-mean()-X"
  * tGravityAcc-mean()-Y"
  * tGravityAcc-mean()-Z"
  * tGravityAcc-std()-X"
  * tGravityAcc-std()-Y"
  * tGravityAcc-std()-Z"
  * tBodyAccJerk-mean()-X"
  * tBodyAccJerk-mean()-Y"
  * tBodyAccJerk-mean()-Z"
  * tBodyAccJerk-std()-X"
  * tBodyAccJerk-std()-Y"
  * tBodyAccJerk-std()-Z"
  * tBodyGyro-mean()-X" 
  * tBodyGyro-mean()-Y"
  * tBodyGyro-mean()-Z"
  * tBodyGyro-std()-X"
  * tBodyGyro-std()-Y"
  * tBodyGyro-std()-Z"
  * tBodyGyroJerk-mean()-X"
  * tBodyGyroJerk-mean()-Y"
  * tBodyGyroJerk-mean()-Z"
  * tBodyGyroJerk-std()-X"
  * tBodyGyroJerk-std()-Y"
  * tBodyGyroJerk-std()-Z"
  * tBodyAccMag-mean()"
  * tBodyAccMag-std()"
  * tGravityAccMag-mean()"
  * tGravityAccMag-std()
  * tBodyAccJerkMag-mean()"
  * tBodyAccJerkMag-std()"
  * tBodyGyroMag-mean()"
  * tBodyGyroMag-std()"
  * tBodyGyroJerkMag-mean()"
  * tBodyGyroJerkMag-std()"
  * fBodyAcc-mean()-X"
  * fBodyAcc-mean()-Y"
  * fBodyAcc-mean()-Z"
  * fBodyAcc-std()-X"
  * fBodyAcc-std()-Y"
  * fBodyAcc-std()-Z"
  * fBodyAcc-meanFreq()-X"
  * fBodyAcc-meanFreq()-Y"
  * fBodyAcc-meanFreq()-Z"
  * fBodyAccJerk-mean()-X"
  * fBodyAccJerk-mean()-Y"
  * fBodyAccJerk-mean()-Z"
  * fBodyAccJerk-std()-X"
  * fBodyAccJerk-std()-Y"
  * fBodyAccJerk-std()-Z"
  * fBodyAccJerk-meanFreq()-X"
  * fBodyAccJerk-meanFreq()-Y"
  * fBodyAccJerk-meanFreq()-Z"
  * fBodyGyro-mean()-X"
  * fBodyGyro-mean()-Y"
  * fBodyGyro-mean()-Z"
  * fBodyGyro-std()-X"
  * fBodyGyro-std()-Y"
  * fBodyGyro-std()-Z"
  * fBodyGyro-meanFreq()-X"
  * fBodyGyro-meanFreq()-Y"
  * fBodyGyro-meanFreq()-Z"
  * fBodyAccMag-mean()"
  * fBodyAccMag-std()"
  * fBodyAccMag-meanFreq()"
  * fBodyBodyAccJerkMag-mean()"
  * fBodyBodyAccJerkMag-std()"
  * fBodyBodyAccJerkMag-meanFreq()"
  * fBodyBodyGyroMag-mean()"
  * fBodyBodyGyroMag-std()"
  * fBodyBodyGyroMag-meanFreq()"
  * fBodyBodyGyroJerkMag-mean()"
  * fBodyBodyGyroJerkMag-std()"
  * fBodyBodyGyroJerkMag-meanFreq()"


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
Use grep to select indices in features$V2 (second column) that have mean and std
* Knowing the indices, subset Xtrain and Xtest, and features 
Covert subsetted features to charactertidyData1.txt
Add 2 columns to Xtrain and Xtest: subject (from subjectxxx.txt) and activity (from y(xxx))
* Create labels for new columns by creating a new vector feaSubNew
* Add new labels using colnames function
* Merge data using rbind
* Sort data by subject and activity using order function
* Write tidy data using write.table or write.csv function
 * This data set is called  
* The next step is to perform mean calculations for the columns by the subject:
 * Use split function to get a list by subject and loop over subject and perform colMeans to get averages for each subject at given activity
 * This produces TidyAverages.txt data set.

## Tidy Data Sets ##
* tidyData1.txt dimension is  10299x81
* TidyAverages.txt dimension is 180x81
 

