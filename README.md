# Relax Data Science Take-Home Challenge
## Overview
This project analyzes user engagement data to identify factors that predict user adoption.
An adopted user is defined as:
A user who logged into the product on 3 separate days within any 7-day period.
 
## Data
Two datasets were provided:
•	takehome_users.csv: user attributes (signup method, marketing flags, org, etc.) 
•	takehome_user_engagement.csv: daily login activity 
 
## Approach
1. Define Adoption
•	For each user, checked for ≥3 unique login days within any rolling 7-day window 
•	Created binary target variable: adopted_user (1 = adopted, 0 = not adopted) 
