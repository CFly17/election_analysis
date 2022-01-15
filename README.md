# Election_Analysis

## Project Overview
Two Colorado Board of Elections employees, Tom and Seth, have established the task of completing an election audit of a recent local congressional election. 

1. Calculate the total number of votes submitted.
2. Get a complete list of candidates. 
3. Calculate the total number and percentage of votes for each candidate.
4. Determine the winner.

## Resources
-- Data Source: election_results.csv
-- Software: Visual Studio Code (version 1.63.2)

## Summary
The analysis of the election shows the following:
--There were 369,711 votes cast
--The candidates were:
    --Charles Casper Stockham
    --Diana DeGette
    --Raymon Anthony Doane
--The candidate results were:
    --85,213 votes for Charles Casper Stockham
    --272,892 votes for Diana DeGette
    --11,606 votes for Raymon Anthony Doane
--The winner of the election was:
    --Diana DeGette

## Challenge Overview
In addition to these results, we were able to calculate the following:
--The voter turnout for each county
--The percentage of votes from each county out of the total count
--The county with the highest turnout
The reason for this additional information was to provide additional  geo-political insights, to inform both the general public as well as those from the election commission and others involved in the campaign. This additional information may allow for future campaigns to increase their campaign presence in select counties. 

#### Voter turnout
We were able to calculate voter turnout across the counties with the following code:

![calculate_county_votes](https://user-images.githubusercontent.com/87148145/149632694-21815dac-b6d1-4e14-bb57-c938467260a0.PNG)

Note the use of a for loop in this code. 

After initializing the dictionary variable "county_votes = {}" above in the code, we can then implicitly pairing the 'county_name' variable as the key of the county_votes dictionary in line 160. This can be done because we have already defined 'county_name' as the second column in the dataset, i.e. as we loop through the rows, we point to index[1] of every row (that is, column 2) and define it as the county_name. By looping through each row and pairing the county name with the county_votes dictionary, which pairs county_name with its respective vote tally, this bit of code allows us to increment the total count:

*county_votes[county_name] += 1*

#### Percentage of Votes by County
Referencing the same image above, we can see how to calculate the percentage of votes per county: We define this variable for each count_name in line 161 of the above image. Then, in line 162, we perform the calculation, making sure to cast the total_county_votes for each county, as well as the overall total vote count for all three counties, as floats. 

#### County with Highest Turnout
The same code we used to calculate the winner of the election, as well as their respective vote count and percentage of the total vote count, is instructive in doing the same for each county:

![calculate_winner_data](https://user-images.githubusercontent.com/87148145/149633199-700b51cb-35ed-4a45-81d6-5e3403d94b92.PNG)

Note that this *if* statement is embedded in the following loop: 
*for candidate_name in candidate_votes:*...
This is important because the variable 'votes' (which for counties would be 'total_county_votes') is defined for each candidate (or county). 
By looping through each candidate's votes (and each counties total vote count), we set the winning variable to whichever is greatest. The utility of this for loop in setting the variable is that, initially the first county we loop over will be the winner; however, as we complete the loop, the winning must 'beat' the if statement of having a greater tally than the 'current' winner within the loop. Once that vote count is surpassed, a new winner is declared within the variable 'winning_count' variable (or in the case of our counties, the 'winning_county_votecount' variable). 

## Challenge Summary 
In summary, this code can serve as a template for future elections across any number of counties -- or even states, with some modifications. 

### Add to the dictionary
The following three lines of code illustrate how we can apply this code to any number of elections:

![calculate_list](https://user-images.githubusercontent.com/87148145/149633532-ec837e42-1a44-482b-afb4-2bc2c316835e.PNG)

By embedding this if statement within a for loop that loops through every column with a 'county_name' in it, we can add each new instance of a 'county_name' to our 'county_list' as soon as the criteria for the if statement (line 160 in the above image) are met. In the current analysis, the second row of the Excel sheet met this criteria, because our list is intially empty; and so we add 'Jefferson'. By the time we finish with the Jefferson votes and hit 'Denver' in row 38,857 of the .csv file, we then add 'Denver' to the list, because it hits the critera of the if statement. And so on. This same logic can be applied to candidates to determine and accumulate a list of unique candidate names. 