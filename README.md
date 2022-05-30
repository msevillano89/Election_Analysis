# Election Analysis
## Project Overview
The Colorado Board of Elections has required additional data to complete the election audit of a recent local congressional election:
1. The voter turnout for each county.
2. The percentage of votes from each county out of the total count.
3. The county with the highest turnout.

Previously, the election committee had required the following analysis:
- Calculate the total number of votes cast.
- Get a complete list of candidates who received votes.
- Calculate the total number of votes each candidate received.
- Calculate the percentage of votes each candidate won.
- Determine the winner of the election based on the popular vote.

## Resources
- Data Source: election_results.csv
- Software: Python 3.10, Visual Studio Code, 1.67.2

## Election-Audit Results
The analysis of the election shows that:
- There were a **total 369,711 votes** between the Jefferson, Denver, and Arapahoe counties. I determined the total of votes by creating a variable named 'total_votes' to serve as a counter, setting it to zero, and utilizing a loop to go through each CSV file row to get the total of votes in the election. See sample lines of PyPoll_Challenge Python code:

```
# Initialize a total vote counter.
total_votes = 0

# Candidate Options and candidate votes.
candidate_options = []
candidate_votes = {}

# 1: Create a county list and county votes dictionary.
county_list = []
county_votes = {}

# Track the winning candidate, vote count and percentage
winning_candidate = ""
winning_count = 0
winning_percentage = 0

# 2: Track the largest county and county voter turnout.
winning_county = ""
winning_count_county= 0
winning_percentage_county = 0

# Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes = total_votes + 1
```

- Breakdown of the number of votes and the percentage of total votes for each county in the precinct were:
    - Jefferson: 10.5% (38,855)
    - Denver: 82.8% (306,055)
    - Arapahoe: 6.7% (24,801)
 
Utilizing the same loop methodology to determine the total votes, I used a conditional statement to tabulate the total county vote and percentage.

Code example:

``` 
       # 3: Extract the county name from each row.
        county_name = row[1]

        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the county does not match any existing county in the county list.
        if county_name not in county_list:

            # 4b: Add the existing county to the list of counties.
            county_list.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0

        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1
```
After establishing how many votes for each county. I wrote a code to determine the percentage of votes each county received.

Code example:
```
# 6a: Write a for loop to get the county from the county dictionary.
    for county_name in county_votes:

        # 6b: Retrieve the county vote count.
        votes_county= county_votes[county_name]

        # 6c: Calculate the percentage of votes for the county.
        county_vote_percentage = float(votes_county) / float(total_votes) * 100
```
Finally, I worte a code to print the results in the election_results.txt file. 

Code example:
```
# 6d: Print the county results to the terminal.
        county_results = (
            f"{county_name}: {county_vote_percentage:.1f}% ({votes_county:,})\n")
        print(county_results)

         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)
```
- Based on the written code above, the county with the largest voter turnout was:
    - **Denver** received the largest number of votes, with **306,055 votes**.

- The candidate results were:
    - Charles Casper Stockham: 23.0% (85,213)
    - Diana DeGette: 73.8% (272,892)
    - Raymon Anthony Doane: 3.1% (11,606)

The methodology used to determine the candidate's vote breakdown is similar to the one used to determine the county vote breakdown.

- The winner of the election was:
    - **Diana DeGette** received **73.8%** of the vote and **272,892 votes**.

## Election-Audit Summary: 
The script developed focused on aiding the audit of the election results in three specific counties (Jefferson, Denver, and Arapahoe). However, the code is written flexibly, with no hard-coded portions. The commission could leverage it to help audit election results in other counties, provided the election results are delivered utilizing the same document format (i.e., csv file extension).

Moreover, the code provides an excellent basis for providing further insights into this type of election for other kinds of elections:

### Example #1: Referendums or Popular Consultations
A referendum or popular consultation is a direct vote determining the public or electorate's sentiment on a proposal. The voter will vote if they are in favor (Yes) or against (No). The script can be modified to capture the number of votes and breakdown percentages for either option and the winning opinion. 

### Example #2: Candidate vote breakdown by county
An interesting data point for each candidate would be their performance in each county that participated in the election. This information is of particular interest to the losing parties as they could use it to determine where they need to invest more efforts for future elections. 
