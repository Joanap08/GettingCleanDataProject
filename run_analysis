## So we need to create a merge between train and test.
setwd("C://Users//milic//Desktop//DataScientistCourse//GettingCleanData//getdata%2Fprojectfiles%2FUCI HAR Dataset//UCI HAR Dataset")
getwd()

install.packages("plyr")
install.packages("stringr")
library(plyr)
library(stringr)
#1.extract the datasets 

trainx<-read.table("X_train.txt")
trainy<-read.table("Y_train.txt", header = FALSE)
testx<-read.table("X_test.txt", header = FALSE)
testy<-read.table("Y_test.txt", header = FALSE)
subtrain<-read.table("subject_train.txt", header= FALSE)
subtest<-read.table("subject_test.txt", header= FALSE)
feat<-read.table("features.txt")
lab<-read.table("activity_labels.txt", header = FALSE)

## rbind x and y separately because of the different dimensions and then cbind
datax<-rbind(trainx,testx)
datay<-rbind(trainy,testy)
subject<-rbind(subtrain,subtest)

##2. extract only the measurement that have SD and MEAN written
## this will define the pattern
pat<-('-mean|-std')
meansd<-grep(pat,feat[,2])

## subset the columns only with mean and sd from the total dataset
datax<-datax[,meansd]

## assign the names to the matrix dataall
names(datax)<-feat[meansd,2]


## 3. Use the descriptive activity names to name the activities in the dataset.

## We know that y only has a column related to activity, which is the column 2
## so we are assigning the labels to this same data, by reading all the column
datay[,1]<-lab[datay[,1],2]

# we are adding the name of activity to collumn that we 
names(datay) <- "Activity"

##4. Put the labels with the descriptive variables
#Combinel all in a data set only now to avoid confusions
names(subject)<-"Subject"
dataall<-cbind(datax,datay,subject)

names(dataall)<-gsub("^t", "time", names(dataall))
names(dataall)<-gsub("^f", "frequency", names(dataall))
names(dataall)<-gsub("Acc", "Accelerometer", names(dataall))
names(dataall)<-gsub("Gyro", "Gyroscope", names(dataall))
names(dataall)<-gsub("Mag", "Magnitude", names(dataall))
names(dataall)<-gsub("BodyBody", "Body", names(dataall))



## Creating a second independent tidy data set with the average of each
##variable for each activity and each subject.
averages<-aggregate(.~Subject + activity,dataall,mean)

#writing out the second tidy dataset.
write.table(averages,"averages.txt", row.name=FALSE)

## Found the information that this would create codebook
install.packages("knitr")
library(knitr)
knit2html("codebook.Rmd")


