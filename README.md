#### Background
Nowadays, most people plan their trips though the travel sites such as booking.com, Expedia, Priceline, and so many more. These sites are easy to negative and can generate best price to meet travelers needs. Since there are so many travels sites, it all comes down to travelers' prefrence. These include but not limit to price, discounts, reviews, refund policy, mobile app availablity, and travel packages/guides. 
Among these travel sites, none of them provide award travel booking. As a wedding travel agent at destinationweddings.com, my job is to undertand customers needs and provide best customized services within desired budgets. 
    
#### Problem Statement
Reddit is a network platform where people share their interests, hobbies, and passions and it allows data scrapping.  In order to design marketing strategies to meet customer demands, which subreddit can provide useful data?
    
#### Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|subreddit|object|awardtravel_4000|data scraping from r/awardtravel|
|subreddit|object|TravelHacks_4000|data scraping from r/TravelHacks|
|selftext|object|df_combined|self-posts, the body of the post| 
|title|object|df_combined|the title of the post|
|distinguished|object|awardtravel_4000|post distinguished by the moderators of r/awardtravel| 
|distinguished|object|TravelHacks_4000|post distinguished by the moderators of r/TravelHacks|
|author|object|df_combined|author of the post|
|removed_by_category|object|awardtravel_4000|how the post was removed on r/awardtravel| 
|removed_by_category|object|TravelHacks_4000|how the post was removed on r/TravelHacks| 
|num_comments|int64 |df_combined|number of comments for each post|
|utc_datetime_str|object|df_combined|when the post was posted|
|text|object|df_combined|a combination of selftext and title|
|text_cleaned|object|df_final|text was tokenize and cleaned|


#### Model Development Plan

1. create a function using Pushshift's API to collet aroudn 4000 posts each from r/awardtravel and r/TravelHacks
2. explore and test different model combination
3. model testing and evaulation


#### Summary
1. text cleaning result
    before: 'booked JAL F for two via Cathay!!! But now advice on picking seats… Finally!! Got the booking confirmed for two ,\n\n240K miles and 650$ in fees for two first class JAL 4/15\n\nThere are 3 available seats with two next to eachother at least via expertflyer information however I was not able to choose which 2 I wanted,\nI have the JAL reference number but when I type that in, they tell me that I need to contact JAL calll center, but apparently that’s not 24/7 and that’s closed right now? Am. I missing something. \n\nWhat should I do?',
    after: 'booked jal f cathay advice picking seat finally got booking confirmed k mile fee class jal available seat eachother expertflyer information able choose wanted jal reference number type tell need contact jal calll center apparently closed right missing'

2. EDA:
    On average, r/AwardTravel has much longer length of selftext than r/TravelHacks. The average post length of title is about equal for both site. r/AwardTravel seems to have more active members leaving comments to the posts.
![image](https://github.com/aichieh/project-3/blob/main/pic/num_post.png)

In general, most posts are neutral; however, r/AwardTravel has a slightly higher sentiment score than r/TravelHacks.
![image](https://git.generalassemb.ly/aichieh/project-3/blob/12f801fdc8a59939575e5718f74698fa13778726/pic/Sentiment.png)

Most popular unigrams via Cvec:
![image](https://git.generalassemb.ly/aichieh/project-3/blob/3f9c7bd6f2d67426de24998bb72c0d192c5b8475/pic/cvec.png)

Most popular unigrams via TFidf:
![image](https://git.generalassemb.ly/aichieh/project-3/blob/0796fa3bb5a46cd2c6d2bcd5a841ec5417be4e00/pic/tvec.png)

Most popular trigrams via CountVectorizer in between two subreddits:
![image](https://git.generalassemb.ly/aichieh/project-3/blob/1193a46ac365ea8df12378966043f21a84fdbc4a/pic/Top%20trigrams.png)

#### Conclusions

r/TravelHacks and r/AwardTravel is somewhat similar because awardtravel is type of travel hacks. From the frequent bigrams and trigrams, r/awardtravel is more about points, flight tickets, and airline company, while r/travelhacks is more about rental car, trip planning, and destinations. According to the Sentiment Analysis, r/AwardTravel has a slightly higher sentiment score than r/TravelHacks. The MultinomialNB model with countvector and gridsearch is the best model to make prediction with accuracy of 91%. 

####  Recommendations
r/awardtravel may be appealing for the customers who want to redeem points for their trips, while r/TravelHacks may be great for customers whose trips involved car rentals. 
One of the major limitions for my model is that all numbers were removed during text cleaning; therefore, it will be hard to provide any features related to numbers such as cost, distance, and number of points for award redeemtion. 
The next steps to improve the model will be:
1. Modify the text cleaning steps to ensure no important numbers are removed
2. Make a list of words related to the airport code so that they are not being removed during the text cleaning process
3. Stake the models to see if the accuracy of model is improved
        
#### Reference
1. https://research.aimultiple.com/scraping-travel-data/
2. https://www.allerin.com/blog/nlp-is-taking-the-travel-and-tourism-industry-to-new-places-heres-how
3. https://www.blog.datahut.co/post/web-scraping-for-travel-industry
4. https://api.pushshift.io/redoc#operation/search_reddit_subreddits_reddit_search_subreddit_get
5. https://www.youtube.com/watch?v=AcrjEWsMi_E
6. https://stackabuse.com/removing-stop-words-from-strings-in-python/
7. https://www.geeksforgeeks.org/nlp-expand-contractions-in-text-processing/
8. https://www.geeksforgeeks.org/python-removing-newline-character-from-string/
9. https://stackoverflow.com/questions/43356467/removing-special-characters-and-symbols-from-a-string-in-python
10. https://stackoverflow.com/questions/11331982/how-to-remove-any-url-within-a-string-in-python
11. https://stackoverflow.com/questions/54396405/how-can-i-preprocess-nlp-text-lowercase-remove-special-characters-remove-numb
12. https://pypi.org/project/redditcleaner/
13. https://stackoverflow.com/questions/67613774/how-to-add-a-mean-and-median-line-to-a-seaborn-displot
14. https://stackoverflow.com/questions/67504409/how-to-handle-out-of-vocab-words-with-bag-of-words
15. https://stackoverflow.com/questions/64039664/combine-metrics-results-into-a-dataframe-python
16. https://seaborn.pydata.org/generated/seaborn.kdeplot.html#seaborn.kdeplot
17. https://www.python-graph-gallery.com/scatter-plot/

