# Potential Talent 

## Brief from client
As a talent sourcing and management company, we are interested in finding talented individuals for sourcing these candidates for technology companies. Finding talented candidates is not easy, for several reasons. The first reason is one needs to understand what the role is very well to fill in that spot, this requires understanding the client’s needs and what they are looking for in a potential candidate. The second reason is one needs to understand what makes a candidate shine for the role we are in search of. Third, where to find talented individuals is another challenge. The nature of our job requires a lot of human labour and is full of manual operations. Towards automating this process we want to build a better approach that could save us time and finally help us spot potential candidates that could fit the roles we are in search for. 
Moreover, going beyond that for a specific role we want to fill in we are interested in developing a machine learning-powered pipeline that could spot talented individuals, and rank them based on their fitness. We are right now semi-automatically sourcing a few candidates, therefore the sourcing part is not a concern at this time but we expect to first determine the best matching candidates based on how suitable these candidates are for a given role. We generally make these searches based on some keywords such as “full-stack software engineer”, “engineering manager” or “aspiring human resources” based on the role we are trying to fill in. These keywords might change, and you can expect that specific keywords will be provided to you.
Assuming that we were able to list and rank fitting candidates, we then employ a review procedure, as each candidate needs to be reviewed and then determined how good a fit they are through manual inspection. This procedure is done manually and at the end of this manual review, we might choose not the first fitting candidate in the list but maybe the 7th candidate in the list. If that happens, we are interested in being able to re-rank the previous list based on this information. This supervisory signal is going to be supplied by starring the 7th candidate on the list. Starring one candidate actually sets this candidate as an ideal candidate for the given role. Then, we expect the list to be re-ranked each time a candidate is starred.

We are interested in a robust algorithm, tell us how your solution works and show us how your ranking gets better with each starring action. How can we filter out candidates which in the first place should not be on this list? Can we determine a cut-off point that would work for other roles without losing high-potential candidates? Do you have any ideas that we should explore so that we can even automate this procedure to prevent human bias?

## Aim
1. Predict how fit a candidate is based on their available information (variable fit) and user input
2. Rank candidates based on a fitness score
3. Re-rank candidates based on user input, such as starring/selecting a candidate.

## Data
The dataset includes 104 entries with 5 features: 
1. id: unique identifier for the candidate (numeric)
2. job_title: job title for the candidate (text)
3. location: geographical location for the candidate (text)
4. connections: number of connections the candidate has, 500+ means over 500 (text)
5. Output (desired target): fit - how fit the candidate is for the role? (numeric, probability between 0-1)

However, after duplicates were removed the dataset quickly shrunk to 54 entries which isn't ideal. 

## Data Wrangling

As the entries for job titles and locations had to be cleaned up quite a bit as the entries had accents and abbreviations. Additionally, there were inconsistencies such as people entering a country for their location whilst others entering cities. There were even a few entries in foreign languages! The spellings were checked, and abbreviations were expanded upon. Each of the entries was changed to lowercase and all accents and symbols and punctuation were removed. Finally, spurious entries were double-checked and in some cases, they had to be dropped as they weren't necessarily job titles: such as 'always set them up for success'. Duplicates had to be double-checked, and then the job title column was combined with the location column so we had a corpus of a larger dataset. This was cleaned up by making sure to remove excess empty spaces, resulting in 52 unique entries. 

Then, the connections column was stripped of symbols and the datatype was changed to integers. There was one person who has only 1 connection, and about 8 people with single-digit connections. A closer look at ids 11, 98, 72, and 79  clearly highlighted the candidates are students which explains the lower number of connections. As a result, a decision had to be made about entries with lower connections. One method is to remove these entries; however, the brief doesn't outline whether they are interested in entry-level applicants or senior-level applications. If our client is interested in entry-level applicants, then those students who are seeking human resources positions would be interesting to keep. So instead of just removing the entries will single digit connections, only the entries of the lower number of connections which don't mention human resources were dropped from the dataset. Then, upon further inspection candidate with id number 6 has the keywords perfectly in the job description, but we can see there's only 1 connection which often means this could be a fake account, not an active account, or sometimes just not a candidate that can be reached. As there isn't any additional information regarding this candidate, this entry was also dropped. 


### Stop words
A custom stopword list was created 
