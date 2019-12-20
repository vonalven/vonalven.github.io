---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

---



 
From being a simple idea born inside the minds of [_two men_][two men], Brian Chesky and Joe Gebbia, 
unable to afford their rent, to becoming one of the best vacation rental sites, 
AirBnb has come a long way. As a matter of fact, the “air” in AirBnb came as a result of 
Brian and Joe renting an [_air mattress_][air mattress] on their living room floor. 


#### A Bit of Background


Since its foundation in 2008, the company experienced a [_continuous growth_][continuous growth] with a boom 
after 2012, ending up to a revenue of 2.6 billions US dollars in 2017, 12736 employees 
in 2019 and an astonishing 2 millions people lodging with AirBnb each night in October 2019.
 Today, AirBnb offers listings in 191 countries and counts about 150 millions users.

<iframe src="assets/html_graphs/Airbnb_world_map.html"></iframe>

Here-above is a graph depicting the worldwide presence of AirBnb from data obtained through
[_Inside Airbnb_][Inside Airbnb]. The bubbles sizes are proportional to the number of listings in each city.
In total, approximatively 1.5 MIO listings are present in the dataset!


With such astonishing numbers, one can’t help but wonder how to get a piece of the pie. 
More specifically, how can short term renting be turned into a sucessful business, to the
point of being a source of income? If you are interested in the idea of subletting your
properties and are considering AirBnb as the plateform to do so, then this data story 
is for you! Indeed, with the help of a thorough analysis of AirBnb data, this article 
will try to solve the mystery of profitable rentings by determining what makes a 
listing sucessful.

  
Thus, we seek to find answers to the following underlying questions of our problem:
-	What do people look for when booking an AirBnb ?
-   What variables have the largest impact on a listing's success ?
-   Are they the same in every city ?



{% include question.html in_text=true
 text="Defining Success"
 image_url="assets/img/Success.jpg"
%}


Before getting down to business by pointing how to get make your listing reach the top, 
let’s get everybody on the same page by detailing what it means for a rented property to 
be successful. Quite naturally, the goal when renting a vacation housing would be to get 
the highest rating accompanied with good reviews and have custumers all year round. There
 are other indicators such as having customers come back to your place but for the purpose 
 of this study only the three factors previously mentioned will be taken into account. 
Since customers rate a listing over several criteria such as cleanliness or communication,
an overall rating that includes all of these aspects will account for client
satisfaction. This is the role of the *review_scores_rating* feature.
Due to AirBnb’s international presence, reviews are found in many languages, with English.
being the most common one. From the latter, sentiment analysis is carried out to evaluate
both the overall positivity and overall negativity of the reviews. These two measures are
 summarized in a so-called '[_compound_][compound]' measure that defines the global sentiment of a comment.
A compound value greater than 0.05 indicates positivity whereas values lower than -0.05 
are related to negativity. For values in-between, reviews are considered as neutral.
The booking frequency, our third indicator of success, is estimated with the average number 
of reviews given to a listing every month. This is under the assumption that, in average, there is
a similar proportion of customers leaving a review of their stay. This is only an estimation 
since not all guests leave reviews. In addition, the duration of the stays could vary considerably. 
It can nevertheless be stated that this metric provides information on the demand for a listing.

Now that we can all agree on a common definition of success, we can move along to getting 
an understanding what parameters have the most impact on a listing’s so-called success.
To do so, we developed a complete pipeline integrating some Machine Learning algorithms 
to perform a preliminary exploratory analysis.


{% include question.html in_text=true
  text="Zooming into a city at a time"
  image_url="assets/img/amsterdam_.jpg"
%}


As a first approach, the analysis concentrated on understanding the parameters that 
influence the most the success of an AirBnb listing in Amsterdam. Focusing on 
Amsterdam only allowed us to strategically build an efficient framework that would later 
be applied to other cities, as we hypothesise that some parmeters may have location-
dependant importances. This city was selected as a reference to develop the analysis 
workflow as it ranks [_25_][25] in the most visited cities worldwide, and lies in the [_top 10_][top 10] 
most visited european destinations. The elevated touristic flux, concurrent with 
the decent amount of AirBnb listings contained in this city's dataset motivated this choice.

Working with this single city, a highly efficient and generalized framework to was constructed,
reducing the computational cost in comparison to building it with the worldwide dataset.

Based on the age, interest, financial means, country of origin and so on, 
the appeal for a given listing may be very different. Though there might be a high level of variability in the data, 
we still expect to manage to identify certain trends in terms of which features contribute most to which success metric.
It is most likely for anyone who has ever gone on a touristic trip to develop
preferences in terms of housing to some extent, whether for the price range, the distance 
to touristics attractions and transportations or the type of accommodation. While most of this information
is present in the [_Inside Airbnb_][Inside Airbnb] dataset, it lacks any clear reference to the proximity to public transportation!
For this reason, we integrate supplementary data with the open-source [_citilines_][citilines] database. 
As not all the corresponding cities are available in this database, we reduce our initial 
dataset to contain only cities for which the public transportations data is available.

Before diving any further into the analysis, we will shortly describe the implemented Machine Learning approaches
that were used. We selected Random Forest (RF) models because of their high capacity in generating high-performance and 
computationally efficient models. Normalisation as well as hyperparameter tuning and multiple performance 
assessment methods were considered. Machine Learning was also applied for the natural language 
analysis of comments guests left to listings they stayed in.

With these tools, we can start to answer to our research question. The importance of all the features in the Random Forest 
predictions was determined for each success metric: the listing's rating, the mean sentiment of its reviews 
and the monthly rate of reviews. Sankey diagrams allow to visually summarize the results. We provide a dropdown menu allowing to compare 
different cities. The thickness of the connection between a given feature and a success metric is proportional to the contribution of this feature
to the prediction in the RF model. 


{% include img_compare.html 
  image_url="assets/dropdown_sankey.html"
%}


From these graphs some conclusions can be drawn:
- The distance of a listing to transportation (dist_to_station) seems to be a determining
factor in most cities.
- Rate of host response appears to be a more important factor in determining the amount of
 reviews per month for Berlin than for Manchester.
- ...

So say you are interested in launching an accommodation business on the plateform in the 
city of your choice, for example Barcelona. You will be able to deduce from the Sankey
diagrams that you should pay particular attention to the number of amenities you offer,
the price you ask, as well as to whether transportation is in close reach. Moreover, you 
will notice that the quality of your offer is not the only factor to influence the success
it will have. In fact, guests also look into the the host behind the listing. As a host 
you should keep in mind that your experience (host_since, host_total_listings_count) will
greatly impact the success of your listing. (Build a trustworthy clientele ?)

Up to this point, the analysis was focused only on single cities, independently from the 
results other cities obtain. Therefore, to get further insight and to be able to 
generalize, we will provide a globalised analysis, identifying similarities between 
different locations may have.

 
{% include question.html in_text=true
  text="From single cities to a worldwide view"
  image_url="assets/img/international.jpg"
%}

We previously established that for different cities, different factors are determinant of
a listing's success. It would thus be interesting to see whether the AirBnb platforms of 
different sets of cities can be clustered according to their similarity in the most important 
succes-determining features. In doing so, we may be able to infer what are the common characteristics
of these groups of cities. It would also be interesting to determine which features are 
conserved throughout the different clusters.

To compute the similarity between cities, only the list of the top 5 most important features are considered. 
An attentive and extensive research was performed to identify the best algorithm and Rank-biased overlap (RBO)
was finally selected, having interesting properties such as non-conjointness groups handling (different elements 
in the compared lists) and the highest weighting of higher ranks. The clustering effect can be
visualized in the heatmap below. The colorscale indicates the degree of similarity between feature ranking
for different cities. Clusters can easilybe identified as diagonal light boxes. 
This analysis was performed for all of the success metrics as target through the RF model. 

To provide an overall summarized view of the 3 different success metrics, we generalized the RF model
to a multi-target prediction. In this case the features that contribute the most to the simultaneous
combination of all the metrics are identified.

{% include img_compare.html 
  image_url="assets/dropdown_metrics.html"
%}

Depending on the selected target, different clusters are formed, defined by a corresponding set of relevant features.
We see....

Now let's get a better look at the clusters. A detailed representation of the conserved most important features across 
clusters is provided with the following scatter bubble-plots.

<iframe src="assets/dropdown_bubble.html"></iframe>

Analyse bubble plot...

<iframe src="assets/dropdown_cluster.html"></iframe>

HERE: Insert png table of what cities in cluster

Try to draw a few conclusions....

-----

Reste du texte à Sirine:

Among all the parameters inspected througout this article, they can finally be topped 
down to 8 key features with the most effect on the success of a listing. These features 
are: 
-	The distance between the housing and the neirest public transportation station
-	The minimum amount of night allowed for a stay
-	The host being a superhost
-	The overall price
-	The price per person 
-	The host response rate
-	How long has the host been renting properties on airbnb
-	The total amount of properties the host has for rent online
-	The number of amenities proposed by the host

You might be panicking at this point, thinking you won’t be able to improve all these 
features. Well, there is no need to be alarmed: if you plan on renting your property in 
a town presented in this study, you’ll just have to identify the town-cluster to wich it 
belongs and then you can find an even smaller list of parameters to improve in order to 
increase your chances of success! 
For example, if you happen to own a real estate that you would like to rent in a town of 
the ninth cluster, then you only have to set your focus on the number of amenities you 
offer, the minimum nights you allow, the proximity with public transportation stations, 
your response rate and being patient because the experience of the host (time elapsed 
since the first rental) also has effect on the success of your listing. 

-----


{% include question.html in_text=true
 text="Conclusion and discussion"
 image_url="assets/img/Discussion.jpg"
%}


At the end of this analysis, we truly hope you will get the best results (and income) 
with your listing. Eventhough the competition is tough, remember that few elements can 
improve a big deal your chance at success. Also keep in mind that the parameters that 
most influence your future success will also depend on where your housing will be located.
 However, tourists’ expectations do meet in particular places regardless of the 
 destination. As expected, most travelers aim for affordable places (price, 
 price_per_person, minimum_nights) close to public transportations 
 (distance_nearest_station) rented by a host they feel they can trust based on their 
 experience (host_since, superhost, high response rate) and that has a lot to offer 
 (number_of_amenities).






All the images are open sources and retrieved from [_pixabay_][pixabay].


[two men]: https://growthhackers.com/growth-studies/airbnb
[air mattress]: https://muchneeded.com/airbnb-statistics/
[continuous growth]: https://muchneeded.com/airbnb-statistics/
[Inside Airbnb]: http://insideairbnb.com
[coumpound]: https://towardsdatascience.com/sentiment-analysis-beyond-words-6ca17a6c1b54
[25]: https://dutchreview.com/cities/amsterdam/amsterdam-is-the-25th-most-visited-city-in-the-world/
[top 10]: https://www.traveltrivia.com/most-visited-cities-in-europe/
[citilines]: https://www.citylines.co
[pixabay]: https://pixabay.com/fr/
