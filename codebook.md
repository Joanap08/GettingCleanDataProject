codebook
Joana

18 November 2016

R Markdown
This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see http://rmarkdown.rstudio.com.

When you click the Knit button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

setwd(“C://Users//milic//Desktop//DataScientistCourse//GettingCleanData//getdata%2Fprojectfiles%2FUCI HAR Dataset//UCI HAR Dataset”) getwd()

install.packages(“knitr”) library(knitr) install.packages(“plyr”) install.packages(“stringr”) library(plyr) library(stringr)

1.Extracting each one of the files from the file.
trainx<-read.table(“X_train.txt”) trainy<-read.table(“Y_train.txt”, header = FALSE) testx<-read.table(“X_test.txt”, header = FALSE) testy<-read.table(“Y_test.txt”, header = FALSE) subtrain<-read.table(“subject_train.txt”, header= FALSE) subtest<-read.table(“subject_test.txt”, header= FALSE) feat<-read.table(“features.txt”) lab<-read.table(“activity_labels.txt”, header = FALSE)

Intermediate step: rbind x and y separately, because of the different dimensions
datax<-rbind(trainx,testx) datay<-rbind(trainy,testy) subject<-rbind(subtrain,subtest)

2. Extract only the measurement that have SD and MEAN written
Defining the pattern
pat<-(‘-mean|-std’) meansd<-grep(pat,feat[,2])

Intermediate step: Subsetting the columns only with mean and sd from the datax
datax<-datax[,meansd]

Intermediate step: Assign the names to the matrix datax
names(datax)<-feat[meansd,2]

Intermediate step: Assign the names to the matrix datay
datay[,1]<-lab[datay[,1],2]

Adding Activity to datay
names(datay) <- “Activity”

3. Use the descriptive activity names to name the activities in the dataset.
datayActivity<−as.character(datayActivity) dataylActivity[datayActivity == 1] <- “Walking” datayActivity[datayActivity == 2] <- “Walking Upstairs” datayActivity[datayActivity == 3] <- “Walking Downstairs” datayActivity[datayActivity == 4] <- “Sitting” datayActivity[datayActivity == 5] <- “Standing” datayActivity[datayActivity == 6] <- “Laying” datayActivity<−as.factor(datayActivity )

Intermediate step: Combine only now all in a data set to avoid confusions
names(subject)<-“Subject” dataall<-cbind(datax,datay,subject)

4. Creating a second independent tidy data set with the average of each
averages<-aggregate(.~Subject + Activity,dataall,mean)

5. Writing out the second tidy dataset.
write.table(averages,“averages.txt”, row.name=FALSE)
