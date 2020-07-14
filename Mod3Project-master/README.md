# An Analysis on Terry Stops in Seattle, WA

<img src="/Mod_3_Images/mdpic.jpg"> 

## Purpose
The purpose of this analysis is to build a (classifier) model to predict whether an arrest was made after a "Terry Stop".

## Case Background
**Terry v. Ohio**, 392 U.S. 1 (1968), was a landmark decision of the Supreme Court of the United States in which the Court ruled that the Fourth Amendment's prohibition on unreasonable searches and seizures is not violated when a police officer stops a suspect on the street and frisks him or her without probable cause to arrest, if the police officer has a reasonable suspicion that the person has committed, is committing, or is about to commit a crime and has a reasonable belief that the person "may be armed and presently dangerous."



## Other Resources
#### Non Technical Presentation
https://www.youtube.com/watch?v=ccLsVuk2WhY

#### Blog
https://medium.com/@gabriel.erica3/an-analysis-of-reasonable-suspicion-e74482438aec


## Description of Data
* **Subject Age Group:** 10 year increments as reported by the officer
* **Subject ID:** Key, generated daily, identifying unique subjects
* **GO / SC Num:** "General Offense" or Street Check Number, relating the Terry Stop to the Parent Report
* **Terry Stop ID:** Key  Identifying Terry Stop Reports
Stop Resolution: Resolution of the Stop as reported by the officer
* **Stop Resolution:** Resolution of the stop as reported by the officer
* **Weapon Type:** Type of weapon, if any, identified during a search or frisk of the subject. Indicates "None"  if no weapons was found.
* **Officer ID:** Unique key identifying officers in the dataset
* **Officer YOB:** Year of brith as reported by the officer
* **Officer Gender:** Gender of the Officer
* **Officer Race:**  Race of the Officer
* **Subject Percieved Race:** Race of the subject as reported officer
* **Subject Percieved Gender:** Percieved gender as reported by the officer
* **Reported Date:** Date the Report was filed
* **Reported Time:** Time the stop was reported
* **Initial Call Type:** Initial classicifaction of the call as assigned by 911
* **Final Call Type:** Final classicifaction of the call as assigned by 911
* **Call Type:** How the call was recieved by the communication center
* **Officer Squad:** Functional sqaud assignment (not budget) of the officer as reported by the Data Analytics Platform (DAP)
* **Arrest Flag:** Indicator of whether or not a physical arrest was Made, of the subject, during the Terry Stop. Does not necessarily relfect a report of an arrest in Records Management System (RMS)
* **Frisk Flag:** Indicator of whether a frisk was conducted
* **Sector:** Sector of the address associated with the Computer Aided Dispatch (CAD) event. Not necessarily where the Terry Stop occurred
* **Precinct:** Precinct of the address assictaed with the CAD event. Not necessarily where the Terry Stop occurred
* **Beat:** Beat of the address associated with the underlying CAD event. Not nen=cessarily where the Terry Stop occurred* 



## Model

#### Model Performance
<img src="/Mod_3_Images/confmatrix.png">

<img src="/Mod_3_Images/ROC_Curve.png">


#### Description of Model
In order to predict whether an arrest was made after a "Terry Stop", cleaned and was divided via a 75%/25% test train split. Continuous variables were treated with a StandardScaler, and categorical variables were treated using OneHotEncoding. finally the imbalanced data from the X_train and y_train datasets were treated with SMOTE to correct the imbalance before they were inserted into the model. I created a child class that would switch between the following baseline models when used in conjunction with the Pipeline and GridSerachCV functions:
* KNeighborsClassifier()
* RandomForestClassifier()
* AdaBoostClassifier()
* GradientBoosting Classifier()

After 68 iterations, the Gradient Boosting Classifier was the best performing model producing a training accuarcy score of 0.998 and a testing accuracy score of 0.997. The most important features were "Officer Year of Birth", "Weapon", and "Stop Resolution_Arrest".


## Areas of Interest
<img src="/Mod_3_Images/Df.png">

### Question 1: How do demographics influence the outcomes of community policing?

#### EDA

<img src="/Mod_3_Images/OfficerRace.png">




<img src= "/Mod_3_Images/subjectrace.png">




<img src= "/Mod_3_Images/OfficerYOB_toRace.png">



#### Findings

* Seattle is 70% White and 51% male. Black/African Americans make up 6.1% of Seattle's Population, but make up 1/3 of the Terry Stop subjects. While those who identify as women make up 20% of the Terry Stop subjects.
* 76% of the officers in this datset are white and 88% of the officers identify as male.  The average age of the officers on duty were born in the year 1982, while the oldest reporting officers was born in 1946 and the youngest officers were born in 1997.

#### Recommendations & Insights
For community policing to be effective, the police force should at a minimum be representative of the total population for that city and/or Precinct. Programs should be started to recruit more minorities and women to be police officers and representatives of the law. Minority representation within the law will help well intentioned laws from unfairly targeting People of Color. With so few women being stopped, it raises the questions;
1. Are women generally seen as less threatening by society? 
2. Because of this, do officers often let their guards down around women? 
3. Could this be a blind spot for the police force and for residents?


### Question 2: On what basis are “hunches made”? What factors influence these instincts, and how do those instincts impact residents?

#### EDA
<img src="/Mod_3_Images/Officer_Race_Gender.png">





<img src="//Mod_3_Images/Subject_Percieved_Gender.png">






<img src="/Mod_3_Images/Subjectby_calltype.png">


#### Findings
The most common reported 911 calls and the top reason for Onview (police field stops- stops not initiated by calls) were categorized as “Suspicious Person”. The majority of all stops made came from the N3 (the North Precinct) and E2 (the East Precinct) Beats. These are predominately white areas in Seattle.

#### Recommendations & Insights
The data here raises many questions, namely; 
1. "How is “Suspicious” defined by Seattle police departments?”
2.  “Is the criteria measurable and trainable?”
3.  “Does it look the same across genders and races?"
4.  How do we as a society define what is threatening or suspicious activity for a man vs a woman. How do these views contribute to the amount of people who “get away”? 
5. Do these criteria vary by age group or is it something else?
6. How does an officer's demeaner affected when he or she hears the phrase "supicious suspect"?
7. How are the lines drawn between "a hunch", instinct, and bias?

911 Dispatchers and officers should be enrolled in annual implicit bias training. This is pertinent for dispatchers because as the messengers and classifiers of the calls, they should be trained in asking the proper questions to identify whether actual threats are imminent or if bias is the culprit. These fielding questions will save officers time and prevent potential violence against pedestrians who are not carrying or committing a crime. In addition officer health plans should be expanded to include therapy. Officers need a medium to deal with stress, rage, and anxiety so that those emotions do not manifest themselves into their work dealing with the citizens that they are tasked with protecting. Lastly, police officers should be partnered with licensed counselors to deal with abuse victims, individuals with mental health issues who may be exhibiting "suspicious behavior", and to check officer biases in real time. 
 

### Question 3: What common age groups are stopped? Are they weapon's carriers? 

#### EDA
<img src="/Mod_3_Images/SubjectAge_toWeapon_Best.png">

#### Findings
Subjects ages 26 - 35 years old were the most stopped age group, totaling 1/3 of the dataset. This age group had the most weapons found on their person. Teenagers were also subject to Terry Stops. A little over 1500 children ranging from 1 - 17, and less than 1/4 of them were found to be carrying weapons. The gun laws in the state of Washington are stricter on purchasing and possessing long guns and semiautomatic weapons, which requires a person to be at least 21 years of age, however it is still largely open to interpretation. 


#### Recommendations & Insights
The age to purchase and possess weapons of any kind should be set at 21 years old. Weapons purchasing and possession should also be restricted to households who have children under the age of 18 in the home. 

### Conclusion
The cost of these new measures will offset the costs of class action lawsuits for harassment & profiling, civil rights violations, and wrongful death suits.

