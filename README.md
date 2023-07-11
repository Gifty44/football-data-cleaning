# football-data-cleaning

Working on the Fifa dataset containing players details to find irregularities to be cleaned in order to prepare the dataset for analysis. Excel was used in carrying out the cleaning process . The following are the irregularities found in the data;

* Inconsistent format for the columns names 
* Wrong datatype
* Inconsistency in the players names
* Inconsistent measurement units in column
*  Wrong capitalization
* Special characters
* Irrelevant column
                The following cleaning processes were carried out to ensure the data was clean to work with;
Step 1
Some columns were having inconsistent naming format just like, Short Passing and some were abbreviated like BOV. Some columns abbreviated were spelt in full names and the naming format was changed to have one type, which is using an underscore to join both words, like, Short_Passing .

Step 2
Some columns that were not in their right datatype were changed using the drop down  menu close to the column names

Step 3
The Name column was only having the initials and the last names of the players, the LongName column was having the first and last names of the players and also initials and the PlayerUrl column was having the full names of the players
The full names of the players was extracted from the Player_Url column, the - in the names were substitued and it was capitalize using this fomulars:  =RIGHT(E2,LEN(E2)-FIND("/",E2,FIND("player",E2)+7)), =PROPER(SUBSTITUTE(LEFT(F2,FIND("/",F2)-1),"-"," ")) and was renamed Player_names

Step 4 
The Weight column was having two measurement units which are lbs and kg. The weight in lbs was converted to kg  and removed the unit of measurement using this formula :  ==IF(RIGHT([@Weight], 3) = "lbs", ROUNDUP(VALUE(LEFT([@Weight], LEN([@Weight])-3)) * 0.45359237, 0), IF(RIGHT([@Weight], 2) = "Kg", LEFT([@Weight], LEN([@Weight])-2), [@Weight]))
 the column was renamed to Weight(kg) showing that the weight is in kg

The Height column was having three measurement units, which were in foot, inches and cm.  In converting the foot to inches and the the inches to cm and removed the unit of measurement using this formular : = =IF(ISNUMBER([@Height]), [@Height], IF(ISNUMBER(SEARCH("'",[@Height])), ROUNDUP(LEFT([@Height], SEARCH("'",[@Height])-1)*30.48 + MID([@Height], SEARCH("'",[@Height])+1, SEARCH("""",[@Height])-SEARCH("'",[@Height])-1)*2.54, 0), SUBSTITUTE([@Height], "cm", "")))


Step 5
The Value, Wage and Release_Clause columns were having special characters which was removed by using find and replace values, the special characters were replaced by empty space.

These same columns have figures in millions and thousands in short form like 165K, 171M except the Wage column which was only in thousand. To get only the numeric value, the K and M have to be in their full value and after that they will be removed as well as the special character using this formula:
  

 for value: = =IF(RIGHT([@Value],1)="M", VALUE(SUBSTITUTE(SUBSTITUTE([@Value],"â‚¬",""),"M",""))*1000000, IF(RIGHT([@Value],1)="K", VALUE(SUBSTITUTE(SUBSTITUTE([@Value],"â‚¬",""),"K",""))*1000, 0))
 
         
         Wage: = =VALUE(SUBSTITUTE(SUBSTITUTE([@Wage], "â‚¬",""),"K", ""))*1000

 Release_Clause: = =IF(RIGHT([@[Release Clause]], 1) = "M", VALUE(SUBSTITUTE(SUBSTITUTE([@[Release Clause]], "â‚¬", ""), "M", ""))*1000000, IF(RIGHT([@[Release Clause]], 1) = "K", VALUE(SUBSTITUTE(SUBSTITUTE([@[Release Clause]], "â‚¬", ""), "K", ""))*1000, 0))


Step 7
The club column was having special characters which each represent an alphabet and other columns c had special characters too which all special characters were removed using find and replace from the menu bar

Step 8
         Columns which will not be relevant for analysis were dropped using the choose column from the menu  














