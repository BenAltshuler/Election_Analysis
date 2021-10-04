* Python Election Audit by Ben Altshuler

** The purpose of this Python script is to gather and summarize election results from a csv, then display the summary in the terminal and in a text file.

** Election-Audit Results
- Total Votes

    Our script shows that 369,711 votes were cast in this election and present in the csv. 

- County Breakdown  
    - Jefferson 10.5 percent with 38,855 votes  
    - Denver 82.8 percent with 306055 votes
    - Arapahoe 6.7 percent with 24801 votes

- Largest number of votes: Denver

- Candidate Breakdown
    - Charles Casper Stockham: 23.0% (85,213 votes)
    - Diana DeGette: 73.8% (272,892 votes)
    - Raymon Anthony Doane: 3.1% (11,606 votes)

- Winner
    - Diana DeGette wins the election with 73.8% of the votes (272,892)

* Election-Audit Summary

The election commission should be excited about this script and its ability to be quickly adapted to any similar voting audit. The script is able to parse the spreadsheets and note all unique candidates and counties. Part of this logic is below. 

if candidate_name not in candidate_options:

            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county:


            # 4b: Add the existing county to the list of counties.
            county.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0
            
The logic is simple enough to modify for other purposes such as referendums: an if statement could capture yes's and no's in an added column, while nested in a similar for loop that iterates through the rows. It could even be placed inside our current for loop "for row in reader: ...". Since a referendum is binary, we would only need to count yes's or no's and can calculate the other number at the end (no need for two counters). We'd then write an output statement for our result. 

Another modification is to look at other issues on the ballot. This script is only auditing one result from a ballot that probably had multiple races. As I touched on in my previous point, we already look at every cast ballot as a row in our main reading for loop. If, for instance, there was another race with different candidates and a different winner, we could augment our first for loop to account for any number of other columns. We could, for example, create a new list for "Senator_Options[]" and append it with candidates, while counting votes in a new "Senator_Votes{}" dict. Finally, we would write a new for loop similar to the one below which would analyze the results from additional columns. 

for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")
