# Data-Mining-Yelp-Dataset-Bussiness-User-Similarities

Step 1: In this step you will use the data from Step 1 to create a sparse table š that holds the ratings. Load the pruned_data.csv file in the form of triads (user id, business id, rating). Then randomly remove 5% of the ratings from table š. These are the ratings we want to predict so we will keep their position and values. The š table with the ratings will no longer contain the values i removed.

Step 2: Implement the User-Based Collaborative Filtering (UCF) algorithm. The algorithm has a parameter š, which is the number of identical users it looks at. To calculate the value of a cell (š¢, š), calculate the total šš (š¢, š) with š most similar users who have rated the business š. We use the following equation for our prediction:

š(š¢, š) = (āš¢ā²āšš(š¢,š) š (š¢, š¢ā²)š(š¢ā², š))/ (āš¢ā²āšš(š¢,š) š (š¢, š¢ā²))

In equation š  (š¢, ā² ā²) is the similarity between users š¢ and uā². I will use cosine similarity for my implementation.

The implementation has the following steps:
ā¢ Calculate the table of similarities between users
ā¢ For each pair (š¢, š) that i have removed:
    1. Find users who have rated š
    2. Take the similarity of these users with user u and keep š more similar
    users
    3. Make two vectors, one with the similarities and one with the scores for the š most
    like users
    4. Calculate the score with the above equation.

Step 3: Implement the Item-Based Collaborative Filtering (ICF) algorithm. The algorithm is essentially the same as in Step 2, i just work with the inverted array and exchange users and businesses. Below is its description for completeness:
The algorithm has a parameter š, which is the number of similar companies it will look at. To calculate the value of a cell (š¢, š) calculate the total šš (š, š¢) with š's most similar to š companies that rated by š¢. Then use the following equation for your prediction:

š(š¢, š) = (āšā²āšš(š,š¢) š (š, šā²)š(š¢, šā²)) /( āšā²āšš(š,š¢) š (š, šā²))

In equation š  (š, ā² ā²) is the similarity between companies š and bā². I will use cosine similarity for my implementation.
     
The implementation has the following steps:
ā¢ Calculate the table with similarities between companies 
ā¢ For each pair (š¢, š) that i have removed:
    5. Find the companies that  has rated u
    6. Take the similarity of these businesses with business š and keep the š longer
    similar companies
    7. Make two vectors, one with the similarities and one with the scores for the š most similar
    businesses
    8. Calculate the score with the above equation. The calculation can be done with
    vector operations.

Step 4: Apply the Singular Value Decomposition (SVD) to the table š, and hold the š larger singular vectors to get a rank-š table šš. Then we use the value š (š¢, š) = šš (š¢, š) for our prediction. If the value becomes less than 0, or greater than 5, round to 0 or 5.

Step 5: Evaluate our algorithms. For the evaluation i will use the RMSE (Root Mean Square Error) metric. If ši are the ratings we want to predict, and ši are the predictions of the algorithm, the RMSE of the algorithm is defined as:

ššššø=ā (1/n ā(šiāši)^2)
š=1

I create graphs with RMSE for different k values for all algorithms. For the UCF algorithm we use the values [1,5,10,20,50,100,200,500,1000]. For the ICF algorithm we use the values [1,5,10,20,40,50,60,70,80,100]. For the SVD algorithm we use the values [1,5,10,20,30,40,50,75,100]. Also, we find the š with the lowest error

I will also compare with the following simple "baselines":
    1. User Average (UA): Use the average š (š¢) of the predictions ratings.
    ĢĢĢĢĢĢ
    2. Business Average (BA): Use the average š (š) of the predictions ratings