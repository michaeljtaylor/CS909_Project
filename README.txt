Michael Taylor's - Code submission for CS909

REQUIRMENTS: R, Reuters 21578 pre-installed, RStudio, text editor

CONTENTS: 1 file including several functions written to be applied to the Reuters 21578 text corpus.
Instructions for use in RStudio will be covered only.
The code in the file will take the user from the full corpus to two outputs, a training data set and a test data set.
The data sets will be split on the LewisSplit meta tag and cleaned and ready for modelling, classification, and clustering.
How you then proceed with modelling, classification, and clustering is up to the user. Bear in mind that the outputs given are what are required for most software and R packages that are readily available.

NOTES: Some instruction information is also included as comments in the code.

INSTRUCTIONS:

FIRST - Open the .R file in a chosen text editor, load RStudio, create a new project, and load in the Reuters 21578 data set. Instructions can be found at Warwick University webpage: http://www2.warwick.ac.uk/fac/sci/dcs/teaching/material/cs909/reuters/
Assume that you have loaded the Reuters 21578 corpus in as variable rt.

SECOND - OPTION A - In R Studio, click on New R Script (Ctrl + Shift + N).
Copy and paste all of the code from the .R file into the R Script window in RStudio.
Select the whole script in window and either press Ctrl + Enter or click on the option Run the current selection.

SECOND - OPTION B - Copy and paste all of the code from the .R file into the Condole window in RStudio.
Press Enter. 

THIRD - Type in the following commands in the console. After typing each command, press Enter, wait for it to finish, then move to the next command.

rt <- mt_preprocess(rt)

tdm <- mt_full_tdm(rt)

tdm_labels <- mt_fulltdm_label(rt, tdm)

tdm_labels <- mt_empty_problem(tdm_labels)

output.datasets <- mt_prepforclass_clust(tdm_labels[1], tdm_labels[2])

COMPLETION:
Once this has been done, the variable output.datasets will contain a list of two data items.
The first is a train set and the second a test set. These can then be coerced into whichever data type you would like.

As most functions require different types of data it is up to you to decide which you would like.

Here is an example for kNN which will provide a confusion matrix after applying the prediction model derived from the training data to the test data.

mat.train <- as.matrix(output.datasets[1])
mat.test <- as.matrix(output.datasets[2])
var.col <- ncol(mat.train)
train.labels <- mat.train[c(var.col)]
test.labels <- mat.test[c(var.col)]
mat.train <- mat.train[c(-var.col)]
mat.test <- mat.test[c(-var.col)]

knn.prediction <- knn(mat.train, mat.test, train.labels)

confusion.matrix <- table("Predictions" = knn.prediction, "Actual" = test.labels) 

confustion.matrix



