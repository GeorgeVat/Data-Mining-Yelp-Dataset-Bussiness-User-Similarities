# Data-Mining-Yelp-Dataset-Bussiness-User-Similarities

Step 1: In this step you will use the data from Step 1 to create a sparse table 𝑅 that holds the ratings. Load the pruned_data.csv file in the form of triads (user id, business id, rating). Then randomly remove 5% of the ratings from table 𝑅. These are the ratings we want to predict so we will keep their position and values. The 𝑅 table with the ratings will no longer contain the values i removed.

Step 2: Implement the User-Based Collaborative Filtering (UCF) algorithm. The algorithm has a parameter 𝑘, which is the number of identical users it looks at. To calculate the value of a cell (𝑢, 𝑏), calculate the total 𝑁𝑘 (𝑢, 𝑏) with 𝑘 most similar users who have rated the business 𝑏. We use the following equation for our prediction:

𝑝(𝑢, 𝑏) = (∑𝑢′∈𝑁𝑘(𝑢,𝑏) 𝑠(𝑢, 𝑢′)𝑟(𝑢′, 𝑏))/ (∑𝑢′∈𝑁𝑘(𝑢,𝑏) 𝑠(𝑢, 𝑢′))

In equation 𝑠 (𝑢, ′ ′) is the similarity between users 𝑢 and u′. I will use cosine similarity for my implementation.

The implementation has the following steps:
• Calculate the table of similarities between users
• For each pair (𝑢, 𝑏) that i have removed:
    1. Find users who have rated 𝑏
    2. Take the similarity of these users with user u and keep 𝑘 more similar
    users
    3. Make two vectors, one with the similarities and one with the scores for the 𝑘 most
    like users
    4. Calculate the score with the above equation.

Step 3: Implement the Item-Based Collaborative Filtering (ICF) algorithm. The algorithm is essentially the same as in Step 2, i just work with the inverted array and exchange users and businesses. Below is its description for completeness:
The algorithm has a parameter 𝑘, which is the number of similar companies it will look at. To calculate the value of a cell (𝑢, 𝑏) calculate the total 𝑁𝑘 (𝑏, 𝑢) with 𝑘's most similar to 𝑏 companies that rated by 𝑢. Then use the following equation for your prediction:

𝑝(𝑢, 𝑏) = (∑𝑏′∈𝑁𝑘(𝑏,𝑢) 𝑠(𝑏, 𝑏′)𝑟(𝑢, 𝑏′)) /( ∑𝑏′∈𝑁𝑘(𝑏,𝑢) 𝑠(𝑏, 𝑏′))

In equation 𝑠 (𝑏, ′ ′) is the similarity between companies 𝑏 and b′. I will use cosine similarity for my implementation.
     
The implementation has the following steps:
• Calculate the table with similarities between companies 
• For each pair (𝑢, 𝑏) that i have removed:
    5. Find the companies that  has rated u
    6. Take the similarity of these businesses with business 𝑏 and keep the 𝑘 longer
    similar companies
    7. Make two vectors, one with the similarities and one with the scores for the 𝑘 most similar
    businesses
    8. Calculate the score with the above equation. The calculation can be done with
    vector operations.

Step 4: Apply the Singular Value Decomposition (SVD) to the table 𝑅, and hold the 𝑘 larger singular vectors to get a rank-𝑘 table 𝑅𝑘. Then we use the value 𝑝 (𝑢, 𝑏) = 𝑅𝑘 (𝑢, 𝑏) for our prediction. If the value becomes less than 0, or greater than 5, round to 0 or 5.

Step 5: Evaluate our algorithms. For the evaluation i will use the RMSE (Root Mean Square Error) metric. If 𝑟i are the ratings we want to predict, and 𝑝i are the predictions of the algorithm, the RMSE of the algorithm is defined as:

𝑅𝑀𝑆𝐸=√ (1/n ∑(𝑟i−𝑝i)^2)
𝑖=1

I create graphs with RMSE for different k values for all algorithms. For the UCF algorithm we use the values [1,5,10,20,50,100,200,500,1000]. For the ICF algorithm we use the values [1,5,10,20,40,50,60,70,80,100]. For the SVD algorithm we use the values [1,5,10,20,30,40,50,75,100]. Also, we find the 𝑘 with the lowest error

I will also compare with the following simple "baselines":
    1. User Average (UA): Use the average 𝑟 (𝑢) of the predictions ratings.
    ̅̅̅̅̅̅
    2. Business Average (BA): Use the average 𝑟 (𝑏) of the predictions ratings