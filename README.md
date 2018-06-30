# MSDS692-Final-Project
by Vanessa Gonzalez, June 2018

## Helping Students Achieve Four-year Graduation Rates by Predicting Computer Science (CS) Program Pain Points in CS Course Sequence.

# Project Overview

Higher Education Institutions struggle in general with the problem of how to increase the graduation rates not just by institution but also by program. Graduation rates are actually reported 2 ways, as the percentage of full-time students who graduate in 4 years and as the percentage of students who graduate in 6 years. These measures are used to rank institutions and are important to maintain or increase enrollment and reputation. In this case we are going to look at the Computer Science program at a Colorado University where not all students that enroll with the Major of Computer Science stay and finish. Some students leave the institution but others change majors while progressing through the coursework. 
We would like to have a better understanding on why and when this happens. We believe that if we are able to predict what students are at risk when taking certain classes then they can be proactive and give additional support to these students to help them succeed and prevent attrition or delay in program completion. 
A variety of factors influence the student decision to leave or change major but we think that there may be a strong relationship between grades obtained in certain courses in a course sequence and four-year graduation rates.

We will try to answer the following questions:

* Which students are at risk at the start of a course to make sure we address their needs and provide support proactively?
* Which are the main points of attrition in the CS course sequence conducive to the loss of students from the CS program or University?

### Data Sets

The data used was extracted from the University Database using IBM Cognos as the tool to query the database. Data from 2008 to 2018 was used. Two data sets were created; One with grades for courses in the math and CS sequences all CS students are required to take for graduation, and another set with the dates when these courses were taken. Both data sets also contained variables describing if the students graduated from CS or if they left the program. A variable was included to describe if the students graduated in four years from CS or if they changed major from the major they changed to.

### Observations on the Quality and Cleaning of the Data
It was observed in both data sets that to show all the variables needed more than one table from the database was needed. Not all tables resided in the same Cognos packages so further mergers were necessary. Merges were performed utilizing Tableau with the student ID as the item for linking the separate data files. 
Further changes and cleaning were necessary:
* Academic period format had to be changed from year-period to year-month.
* Course names had to be changed to Number of Semester recommended plus course code.
* Double majors had to be cleaned to show just the CS record.
* Several CASE statements in Tableau were used to define depending registration in Spring 18 and Fall 18 if the students were current students or if the students had left the institution.
* CASE statements in Tableau were used to define the student group as CS students if CS had been their original major or their first major.
* Calculations were added in Tableau to define the length between original major date and graduation date. Additional modifications and preparation of the data sets happened in R. Details can be found in all the attached R files.

After modifications the finished data sets consisted of the fallowing variables:  
#### Data Set 1
'data.frame':	536 obs. of  24 variables:  

Year of OriginalMajorDate: int  2014 2008 2008 2011 2008 2008 2008 2008 2008 2008 ...  
GraduationStatus         : Factor w/ 3 levels "CurrentStudent",..: 2 2 3 3 2 2 2 2 3 2 ...  
YearsFromOMD             : num  4 9.84 9.84 6.84 9.84 9.84 9.84 9.84 9.84 9.84 ...  
CsGrad                   : Factor w/ 3 levels "NG","OtherMajor",..: 3 2 1 1 2 3 3 2 1 2 ...  
4YG                      : Factor w/ 2 levels "No","Yes": 2 1 1 1 2 2 2 2 1 2 ...  
5YG                      : Factor w/ 2 levels "No","Yes": 2 2 1 1 2 2 2 2 1 2 ...  
6YG                      : Factor w/ 2 levels "No","Yes": 2 2 1 1 2 2 2 2 1 2 ...  
1_CSCI101                : num  4 NA NA NA NA 4 4 NA NA NA ...  
1_MATH111                : num  3 3 3 3 3 3 4 3 2 3 ...  
2_CSCI261                : num  4 4 4 3.3 4 3 4 3 3 3 ...  
2_MATH112                : num  2 2 2 4 3 3 4 4 2 2 ...  
2_MATH201                : num  3 3 2 NA 3 2 4 NA NA 1 ...  
3_CSCI262                : num  3 NA 1 3 NA 3 4 4 1 NA ...  
3_MATH213                : num  4 3 2 2 3 4 4 4 1 2 ...  
4_CSCI341                : num  2 NA 2 2 NA 3 4 NA 3 3 ...  
4_CSCI358                : num  4 NA 3 2 NA 2 4 NA NA NA ...  
4_MATH225                : num  4 3 1 4 4 3 4 4 NA 1 ...  
5_CSCI306                : num  3 NA NA 3.7 NA 4 4 4 NA NA ...  
5_CSCI403                : num  4 NA NA 3 NA 4 4 NA NA NA ...  
5_MATH332                : num  3 NA 2 3 NA 3 4 NA NA NA ...  
6_CSCI406                : num  2 NA NA 0.3 NA 2 4 NA NA NA ...  
7_CSCI370                : num  3.3 NA NA NA NA 4 4 NA NA NA ...  
8_CSCI400                : num  3.3 NA NA 3.3 NA 3 4 NA NA NA ...  
9_CSCI442                : num  2.3 NA NA NA NA 3 4 NA NA NA ...  

#### Data Set 2

Classes ‘tbl_df’, ‘tbl’ and 'data.frame':	195 obs. of  25 variables:  

UID                      : chr  "12972" "12973" "41647" "98022" ...  
Year of OriginalMajorDate: chr  "2008" "2008" "2011" "2008" ...  
YearsFromOMD             : chr  "9.88" "9.88" "6.88" "9.88" ...  
4YG                      : Factor  "No" "No" "No" "Yes" ...  
5YG                      : Factor  "Yes" "No" "No" "Yes" ...  
6YG                      : Factor  "Yes" "No" "No" "Yes" ...  
GraduationStatus         : chr  "Graduated" "InactiveReg" "InactiveReg" "Graduated" ...  
CsGrad                   : chr  "OtherMajor" "NG" "NG" "OtherMajor" ...  
Nine.CSCI442             : num  NA NA NA NA NA ...  
Eight.CSCI400            : num  NA NA 2017 NA NA ...  
Seven.CSCI370            : num  NA NA NA NA NA ...  
Six.CSCI406              : num  NA NA 2018 NA NA ...  
Five.CSCI403             : num  NA NA 2017 NA NA ...  
Five.MATH332             : num  NA 2011 2015 NA NA ...  
Five.CSCI306             : num  NA NA 2017 NA 2011 ...  
Four.CSCI358             : num  NA 2012 2017 NA NA ...  
Four.CSCI341             : num  NA 2011 2015 NA NA ...  
Four.MATH225             : num  2010 2011 2015 2010 2009 ...  
Three.CSCI262            : num  NA 2010 2015 NA 2010 ...  
Three.MATH213            : num  2010 2010 2013 2009 2009 ...  
Two.CSCI261              : num  2010 2010 2014 2010 2009 ...  
Two.MATH201              : num  2011 2012 NA 2010 NA ...  
Two.MATH112              : num  2009 2010 2013 2009 2009 ...  
One.MATH111              : num  2009 2009 2013 2009 2009 ...  
One.CSCI101              : num  NA NA NA NA NA ...  

### Process for Project and Major Tools Used

This project was completed utilizing:
* IBM Cognos -  to query the University data base and produce seven different csv files from different tables.
* Tableau – to clean, format, and combine csv files into two main files. Data was pivoted and summarized to produce the desire order of variables and information.
* R – Used to modify, and analyze the two main data sets. R files are located at:
* A youtube presentation is located at: 

# EDA (Exploratory Data Analysis)
### Data Set 1
The data sets were uploaded, summaries, data frames, tables, and plots created using the code in the files attached.

![image1](/images/SummarydfDataset.png)

![image](/images/CSStudentStatusPie.png). 

A bar plot was created where the "graduated" students were divided into CS and Other Major students.

![image2](/images/BarChart.png)

### Data Set 2
Variable CS Grad:  
* Yes - CS Students
* OtherMajor - Left CS
* NG - Not Graduated. 

Data from 2008-2018 and excludes current students and students that graduated from CS.

Summaries were created.  

![image3](/images/SummaryLastClass.png)

To start the analysis for four year graduation success the need of creating a subset of the data arised. It was necessary to look at just the students that had completed the CS program succesfully in four years. It was also helpful to find the correlation between the courses taken by the students. The code below was used to achieve this.

![image4](/images/CorrelationPlot.png). 

# Analysis
## Building the Models in R
Several Libraries were used to perform this task:
* library("mlbench"). 
* library("dplyr"). 
* library("caret"). 
* library("randomForest")  
* library("lattice"). 
* library("ggplot2"). 
* library("rpart"). 
* library("e1071"). 
* library("caret"). 

Three main models were used to determine variable importance, to train, and test the model.

* Regression Partition with method "class". 
* Random Forest model. 
* Logistic Regresion.  
80% of the data was used as the training set and 20% of the data was used as the testing set.

Models were created using all courses variables and then subsequently variables with less importance were removed. New models were created for this new data set. Several methods were tried to increase accuracy. Trees were prunned, size of training set was increased and different number of variables were removed. The ideal conditions for accuracy are the ones shown below.

### Regression Classification Trees and Random Forest Using All Variables
* Partitions Creation
* Regression Partition with method "class".
* Random Forest Method
* Logistic Regression Method for Variable Importance

### Models using less variables
* Regression Partition with method "class" for set with less variables
* Random Forest model with less variables
* Logistic Regression with less variables

### Prediction of Students at Risk on Fifth Semester

* Random Forest model using less variables for semester 5
* Regresion Partition with method "class" for less variables for 5th semester courses.
* Random Forest method with less variables on 5th semester.
* Logistic Regression method for variable importance

# Analysis Results
Results were produced for Regresion Partition with all variables, after pruning, and Random Forest for three data sets:  
## All courses variables
#### Regression Partition with method "class".
![image5](/images/RegressionAllV.png)
#### Pruned Tree
![image6](/images/PruneAll.png)
#### Random Forest
![image7](/images/RFAll.png)
![image8](/images/RFAllPlot.png)
## Less Course Variables
#### Regression Partition with method "class".
![image9](/images/RpartLess.png)
#### Pruned Tree
![image10](/images/PruneLess.png)
Importance of varialbes.  
![image11](/images/ImpVarLess.png)
Plot of importance of variables.  
![image12](/images/ImpVarPlot.png)
#### Random Forest
![image13](/images/RFLess.png)
## 5th Semester Variables
#### Random Forest
![image14](/images/FifthSemRF.png). 
![image18](/images/VarPlot.png). 

## Last course taken by students that left the program
The analysis for last CS highest course taken by students was done in three different data sets:
#### All Students that left the CS program
![image15](/images/AllStudentsLeft.png)
#### Students that left the institution
![image16](/images/LeftInst.png)
#### Students that went to other majors in the same institution
![image17](/images/OtherMajor.png)


# Conclusions

536 Students were registered with a CS first major in the 2008-2014 time frame. By Spring 2018, 73.88% of those students graduated, 20.15% left the institution and 5.97% left the CS program and graduated from a different major.

It is important to predict which students are at risk of not graduating in 4 years, of leaving the program, or of leaving the institution and provide the additional support needed to increase the four-year graduation rate. The produced model can be applied when students are starting their 6th semester of the Computer Science program and predict if the student will graduate in four years or not graduate in four years with a 75.74% accuracy.

Considering that the no information rate was 71.8% it is an acceptable result with a Kappa of 0.37. I would like to see a higher accuracy but even if just one extra student is detected, helped, and graduates on time it would be a success.

There is a strong correlation between different CS courses in the sequence but was interesting to find a strong correlation of the MATH201 (Statistics Course) with so may of the CS courses.

With the second data set it was found that most students that leave the program do so after taking the CSCI261 course fallowed by CSCI442, CSCI358, and CSCI262. This information provides insight to the Computer Science Department on doing additional research to figure out why this is. By modifying the class or provide students with additional help on this course student retention may increase.

It was interesting to find the main course variables that affect the 4-year graduation rate and how they correlate with each other. Some CECS courses were important as expected but the MATH201 statistics class was found to be important by every method and we really do not know why this is. Additional research should be done to figure out the reason.

There is a lot more to be done. More questions to to be answered and other angles to be explored. It would be interesting to add more variables to our data set including gender, nationality, instate or out of state tuition, and race.
It would also be interesting to apply the same model and process to other programs course sequences and reach out to students at risk to provide them with additional support.





# References 
Github: [1] (https://github.com/guanegonzalez/MSDS692-Final-Project).   

Github R PDF Files: [2] (https://github.com/guanegonzalez/MSDS692-Final_Project-Vanessa_Gonzalez/tree/master/R_PDF_Files).   

Github R RMD Files: [3] (https://github.com/guanegonzalez/MSDS692-Final_Project-Vanessa_Gonzalez/tree/master/rmd_files).   

Github Presentation in PDf: [4] (https://github.com/guanegonzalez/MSDS692-Final_Project-Vanessa_Gonzalez/tree/master/Presentations). 

Youtube Presentation: [5] (https://youtu.be/eOgN_IJm3YI)








