# Getting-and-cleaning-data-peer-graded-assignment

This is the file where I explain my analysis.

You download the "tdata_wide.txt" file and save it inside a directory.
Go to tht directory and open a R console and then you can save tdata_wide.txt
file using the following command:

mydata <- read.table("tdata_wide.txt", header = TRUE)

it will look tidy. Please remember that if you open "tdata_wide.txt" file
using notepad or notepad++, it may look lousy. First convert it into
a dataframe and then please judge it. Please make sure you have used 
header = TRUE argument.

Now about my analysis part:
---------------------------------------------------------------------------------
Step-1, merging train and test data:
---------------------------------------------------------------------------------
The variables used for this step are as follows:

features: contains information of features.txt
xtrain: contains information of x_train.txt
ytrain: contains information of y_train.txt
subtrain: contains information of suject_train.txt
xtest: contains information of x_test.txt
ytest: contains information of y_test.txt
subtest: contains information of suject_test.txt
train: combination of ytrain, subtrain, xtrain
test: combination of ytest, subtest, xtest
combine: combination of train and test


X_train and X_test data both have 561 columns and features data has 561 rows.
The names which are mentioned in features data, are the column names of
X_train and X_test.

y_train and y_test they have the activity list and subject_train and
subject_test, they have subject list. The details of activity and subject types
are mentioned in the codebook.

First I fixed the column names of train files and test files separately after
reading these files.
I cbinded y_train, subject_train and x_train to have a complete train set
and similarly cbinded y_test, subject_test and x_test to have a complete test set.
Then I merged trained and test files using rbind function.



---------------------------------------------------------------------------------
Step-2, Extracting mean and std data:
---------------------------------------------------------------------------------

The variables used for this step are as follows:

ms: stands for mean and std


I have checked separately that there is no "activity" or "subject" inside ANY 
OTHER COLUMN NAMES without these two particular columns. Then I used grepl to 
separate the columns which has mean and std in the column names. The column names
which has meanFreq are also included in it as it was not mentioned anywhere 
whether to include these columns or not. I have included these.
(as Ref:
https://thoughtfulbloke.wordpress.com/2015/09/09/getting-and-cleaning-the-assignment/ )

Here I want to mention that this step can be done in a different way also.
While merging if I don't merge y_train, y_test, subject_train and subject_test
with x_train and x_test, then after just merging x_train and x_test, I could 
extract only mean and std columns. And after that I could merge the activity and 
subject columns with these merged x_train and x_test data. But in this case also,
at the end I will have same result, so it does not matter which way I am doing it.



---------------------------------------------------------------------------------
Step-3, Uses descriptive activity names to name the activities in the data set:
---------------------------------------------------------------------------------

Activity names were included in the data.
1: walking
2: walking_upstairs
3: walking_downstairs
4: sitting
5: standing
6: laying

---------------------------------------------------------------------------------
Step-4, Appropriately labels the data set with descriptive variable names:
---------------------------------------------------------------------------------
 
 Here I have just removed "()" signs replaced "-" sign with "." sign from the
 column names. I did not find any reason to further elaborate the names of
 the columns here, as anyway in codebook I gave a detailed description of the
 names of the columns.

---------------------------------------------------------------------------------
Step-5, From the data set in step 4, creates a second, independent tidy data set
with the average of each variable for each activity and each subject:
---------------------------------------------------------------------------------

I used reshape2 package for this purpose. 

The variables used for this step are as follows:

tdata_long means tidy data in long format.
tdata_wide means tidy data in wide format

In tdata_long, melt function keeps "activity" and "subject" columns of  "ms" 
data frame as it is and creates a third column named "variable" where all other 
column names of "ms" data frame goes and their values are written in a 4th column 
named "value" in tdata_long. In tdata_wide, dcast function then calculates the 
average(MEAN) of each of the "variable" quantities for each "activity" and  each
"subject".

-----------------------------------------------------------------------------------
Final step: writing the data of tdata_wide data frame in a text file
-----------------------------------------------------------------------------------

tdata_wide.txt is the file prepared from tdata_wide data frame.

I hope things are clear and I could make you understand about my analysis.
