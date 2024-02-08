# R_Project
A nationwide survey of hospital costs conducted by the US Agency for Healthcare consists of hospital records of inpatient samples. The given data is restricted to the city of Wisconsin and relates to patients in the age group 0-17 years. The agency wants to analyze the data to research on healthcare costs and their utilization.

We use  Use-R studio. 

First we read the given csv hospital file and mount the table
 To record the patient statistics, the agency wants to find the age category of people who frequents the hospital and has the maximum expenditure.  
 The following question has two conclusions Now to find the category with the max frequency of hospital vists we us data visualization to get an overview of the all the categories, in this case we will use a histogram for frequency analysis. 
After that we will factor function the make the “AGE” column numerical which will be later used in summary function 
Conclusion 1: From the above results we conclude that infant category h as the max hospital visits (above 300). The summary of Age gives us the exact numerical output showing that Age 0 patients have the max visits followed by Ages 15-17. 
Aggregate function is used to add the expenditure from each age and then max function used to find highest costs. 
Conclusion 2: Thus, we can conclude that the infants also have the maximum hospital costs followed by Age groups 15 to 17, additionally we can say confidently that number of hospital visits are proportional to hospital costs. 
 
  In order of severity of the diagnosis and treatments and to find out the expensive treatments, the agency wants to find the diagnosis related group that has maximum hospitalization and expenditure.  
Now we will make sure that category column(“APRDRG”) is numerical and then generate a summary along with the which.max to generate the max index of the category data frame, this will be followed by aggregate function used in a similar way as above. 
Conclusion: Hence can conclude that category 640 has the maximum hospitalizations by a huge number (267 out of 500), along with this it also has the highest hospitalization cost. III. To make sure that there is no malpractice, the agency needs to analyze if the race of the patient is related to the hospitalization costs.  
 
Here we will first remove the “NA” values from our database, then factorize the Race variable to generate a summary, additionally to verify whether race made an impact on the hospital costs we will use ANOVA function with TOTCHG as dependent variable and RACE as grouping variable. 
Conclusion: F value is quite low, which means that variation between hospital costs among different races is much smaller than the variation of hospital costs within each race, and P value being quite high shows that there is no relationship between race and hospital costs, thereby accepting the Null hypothesis. Additionally, we have more data for Race 1 in comparison to other races (484 out of 500 patients) which make the observations skewed and thus all we can say is that there isn’t enough data to verify whether race of a patient affects hospital costs. 

 To properly utilize the costs, the agency has to analyse the severity of the hospital costs by age and gender for proper allocation of resources.  
 
Now to analyse the severity of costs we will use linear regression with TOTCHG(Cost) and independent variable along with AGE and Female as dependent variables 
Conclusion-Age has more impact than gender according to the P-values and significant levels, also there are equal number of Females and Males and on an average (based on the negative coefficient values) females incur lesser hospital costs than males. 

 
 Since the length of stay is the crucial factor for inpatients, the agency wants to find if the length of stay can be predicted from age, gender, and race.  
 
Using linear Regression, we can show whether length of stay is dependent on age, gender or race. Here we LOS is the dependent variable and age, gender and race are independent variables  
Conclusion-p-values for all independent variables are quite high thus signifying that there is no linear relationship between the given variables, finally concluding the fact that we can’t predict length of stay of a patient based on age, gender and race. 


To perform a complete analysis, the agency wants to find the variable that mainly affects the hospital costs.  
 Using linear Regression, we can show which variable affects the hospital costs the most, thus TOTCHG becomes dependent variable and rest all variables are taken as independent. Conclusion-Age and length of stay affect the total hospital costs. Additionally, there is positive relationship between length of stay to the cost, so with an increase of 1 day there is an addition of a value of 742 to the cost.

1. To record the patient statistics, the agency wants to find the age category of people who frequent the hospital and has the maximum expenditure
hosp_cost<-read.table(file.choose(),sep=",",header=TRUE)
head(hosp_cost)
summary(hosp_cost)
head(hosp_cost$AGE)
summary(hosp_cost$AGE)
table(hosp_cost$AGE)
hist(hosp_cost$AGE)
 


str(hosp_cost)
summary(as.factor(hosp_cost$AGE))
max(table(hosp_cost$AGE))
max(summary(as.factor(hosp_cost$AGE)))
which.max(table(hosp_cost$AGE))
age <- aggregate(TOTCHG ~ AGE, data = hosp_cost, sum)
max(age)

 

 2.In order of severity of the diagnosis and treatments and to find out the expensive treatments, the agency wants to find the diagnosis related group that has maximum hospitalization and expenditure.
t <- table(hosp_cost$APRDRG)
d <- as.data.frame(t)
names(d)[1] = 'Diagnosis Group'
d
which.max(table(hosp_cost$APRDRG))
which.max(t)
which.max(d)          
res <- aggregate(TOTCHG ~ APRDRG, data = hosp_cost, sum)
res
which.max(res$TOTCHG)
res[which.max(res$TOTCHG),]

 

 


 
 

 

3. To make sure that there is no malpractice, the agency needs to analyze if the race of the patient is related to the hospitalization costs
table(hosp_cost$RACE)
hosp_cost$RACE <- as.factor(hosp_cost$RACE)
fit <- lm(TOTCHG ~ RACE,data=hosp_cost)
fit
summary(fit)
fit1 <- aov(TOTCHG ~ RACE,data=hosp_cost)
summary(fit1)
hosp_cost <- na.omit(hosp_cost)
 
 



4. To properly utilize the costs, the agency has to analyze the severity of the hospital costs by age and gender for proper allocation of resources.
table(hosp_cost$FEMALE)
a <- aov(TOTCHG ~ AGE+FEMALE,data=hosp_cost)
summary(a)
b <- lm(TOTCHG ~ AGE+FEMALE,data=hosp_cost)
summary(b)
 

5. Since the length of stay is the crucial factor for inpatients, the agency wants to find if the length of stay can be predicted from age, gender, and race.
table(hosp_cost$LOS)
cat <- aov(LOS ~ AGE+FEMALE+RACE,data=hosp_cost)
summary(cat)
cat <- lm(LOS ~ AGE+FEMALE+RACE,data=hosp_cost)
summary(cat)
 
 

6. To perform a complete analysis, the agency wants to find the variable that mainly affects the hospital costs.
aov(TOTCHG ~.,data=hosp_cost)
mod <- lm(TOTCHG ~ .,data=hosp_cost)
summary(mod)

[HEALTHCARE.RESULT.docx](https://github.com/tejaswini301194/R_Project/files/14204350/HEALTHCARE.RESULT.docx)



[healthcare.csv](https://github.com/tejaswini301194/R_Project/files/14204356/healthcare.csv)

 
