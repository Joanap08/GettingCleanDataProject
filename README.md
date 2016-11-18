# GettingCleanDataProject

For this project we are focusing into tidy a data set for data collected from acelerometters.

We have have performed our analysis accordingly with the following steps:

Run_Analysis.R

# 1.Merge the datasets train and test
# We have used mostly rbind and cbind to extract and merge the train and the test variables.

# 2.Extract only the measurement that have SD and MEAN written
# In this step we have use the grep to extract all the columns that did not mention either standard deviation or mean.

# 3. Use the descriptive activity names to name the activities in the dataset.
In this particular step we assign and create the column activities in the data set.

# 4. Put the labels with the descriptive variables
Simply clarify some of the variables for more clear names.
# 5.Creating a second independent tidy data set with the average of each subject and activity
we simply use aggregate operation to be able to calculate the mean for each activity and subject.


