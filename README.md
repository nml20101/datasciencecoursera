## Getting and Cleaning Data Class Project  ##

This repository contains README.md, run_analysis.R, CodeBook.md,
tidyData1.txt, and TidyAverages.txt files for the Coursera's course project 
Getting and Cleaning Data.

### Raw Data ###
The raw data represents data
collected from the accelerometers from the Samsung Galaxy S smartphone. It is obtained from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

### Script Details and Output ###
run_analsyis.R does the following tasks (per project's instructions):
Downloads the data from aforementioned website
2. Saves the data in UCI HAR Dataset folder after extracting via unzip
3.	Reads all activity names, subjects, test and train data sets
4.	Extracts only the measurements on the mean and standard deviation for each measurement. 
5.	Merges the training and the test sets to create one data set: tidyData1.txt
6.	Uses descriptive activity names to name the activities in the data set
7.	Appropriately labels the data set with descriptive variable names.
8.	Splits the data by subject for each activity and loops over activities and subjects to create independent tidy data set with the average of each variable for each activity and each subject: TidyAverages.tx


### CodeBook.md Content ###

The CodeBook.md describes the variables, the data, and transformations 
and work that is performed to clean up the data for the class project on Coursera's

### Additional Notes ###
All work was performed using Version 0.98.507 – © 2009-2013 RStudio, Inc.


