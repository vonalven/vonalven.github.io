---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

---



 
From being a simple idea born inside the minds of [_two men_], Brian Chesky and Joe Gebbia, 
unable to afford their rent, to becoming one of the best vacation rental sites, 
AirBnb has come a long way. As a matter of fact, the “air” in AirBnb came as a result of 
Brian and Joe renting an [_air mattress_] on their living room floor. 


#### A Bit of Background


Since its foundation in 2008, the company experienced a [_continuous growth_] with a boom 
after 2012, ending up to a revenue of 2.6 billions US dollars in 2017, 12736 employees 
in 2019 and an astonishing 2 millions people lodging with AirBnb each night in October 
2019. Today, AirBnb offers listings in 191 countries and counts about 150 millions users.

<iframe src="assets/html_graphs/Airbnb_world_map.html"></iframe>
Here-above is a graph depicting the worldwide presence of AirBnb from data obtained through
[_Inside Airbnb_]. The bubbles sizes are proportional to the number of listings in each city.
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
 summarized in a so-called '[_compound_]' measure that defines the global sentiment of a comment.
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
workflow as it ranks [_25_] in most visited cities worlwide, and lies in the [_top 10_] 
most visited european destinations. The elevated touristic flux concurrent with 
the decent amount of AirBnb listings contained in this city's dataset motivated this choice.

Working with this single city, the construction ofa highly efficient and generalized framework to be applied to all the next sections, reducing the 
computational cost.

Choosing Amsterdam was motivated by the fact that it ranks fifth in
 Europe’s most visited cities (citer source), such that many visitors potentially make use
  of the plateform, without the dataset being too large and computationally intensive.
  
   
It is most likely for anyone who has ever gone on a touristic trip to develop
preferences in terms of housing to some extent, whether it be a price range, the distance 
to attractions and transportation or the type of accommodation. Indeed, it may be expected 
for someone visiting Amsterdam to want a rental place near the center, for a good price 
as well as possibly other services, such as an included breakfast. However the demography 
of travellers can be very diversified. Based on the age, interest, financial means,
 country of origin and so on, the appeal for a given listing may be very different. 

{% include img_compare.html 
  image_url="assets/dropdown_sankey.html"
%}


Though there might be a high level of variability in the data, we still manage to 
identify certain trends in terms of which features contribute most to which metric. In 
fact, Sankey diagrams allows for the importance of a given feature for the three success 
metrics: a listing's rating, the mean sentiment of its reviews and the amount of reviews 
it gets in a month, to be visualised. A dropdown menu allows for a wide range of cities to
 be selected and for their results to be compared. The thickness of the connection between
a given feature and a success metric is proportional to the weight of the feature's 
contribution to this metric. The importance of features was computed through a Random 
Forest analysis.

From these graphs we are able to draw a few conclusions:


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

INSERT CORRELATION Here

Now that you know what parameters to focus your attention on, it is in your best interest
 to know beforehand how you can optimize them to get better ratings, better comments and 
 more demand (more review/month). Select the city of your choice in the correlation plot 
 above to better visualize the relationship between the most important parameters for this
city and the succes metrics. To follow through on the previous example, where you were
hypothetically targeting Barcelona as a market to start hosting, you can now see that ...
amenities will lead to .... (change in a metric). 

Up to this point, the analysis was focused only on single cities, independently from the 
results other cities obtain. Therefore, to get further insight and to be able to 
generalize, we will provide a globalised analysis, identifying similarities between 
different locations may have.



Ancien texte peut-etre reutilisable:

-------

 Because of the considerable amount of parameters that are considered in this research, 
 the second plot focuses only on the 8 most important ones. As far as the owners of 
 Airbnbs in Amsterdam as conserned, in order to maximize their chance at success, they 
 hould focus their energy on:
-	increasing the number of amenities they offer to the renters as well as their response
 rate,
-	optimizer the pricing of their property
-	renting entire appartement that are closte to public transports station.
Also, the longest one has been hosting travelers, the more successful the listing.

(changer ci-dessous)
However, these results were obtained by looking at all the listings in Amsterdam. Let’s 
not forget you want to get your property to the top. Therefore, it is time to bring our 
analysis to an internationational level. That’s right, needs might differ with respect 
to where you decide to rent holiday housings. Indeed, some towns might be more prone to 
extensive exploration of touristic attractions whereas others might be more prone to 
enjoying tranquility by the pool or the beach for example. Let’s find out if these results
 can be generalized in order to give you the best tools to owning a successful listing.
 
 Let’s begin with the study of every aspect of success individually: for every country 
available on both the transport and airbnb dataset, let’s find out what aspect of a 
listing have the most impact on the booking frequency (review_per_month), the grade 
(review_score) and the positivity of the comments (compound) individually. 

Directly following the first observation is that, as expected, what influences success 
varies depending on your location. For example, the time elapsed since one has been a 
host on Airbnb is the second most relevant parameter to getting good grades in cities 
in the fifth cluster whereas it only is the forth one for cities in the tenth cluster. 

Now that it is known for a fact that the location matters for how to handle your reting
 property, it is time to understand which parameters it would be in your best interest 
 to improve as best as possible. For that, a multi-target study might come in handy. 
 Indeed, it is time to look at success by considering all its aspects and to come up 
 with the best strategy for you to access the hosts’ elite. 

 
--------
 
{% include question.html in_text=true
  text="From single cities to a worldwide view"
  image_url="assets/img/international.jpg"
%}

We previously established that for different cities, different factors are determinant of
a listing's success. It would thus be interesting to see whether the AirBnb platforms of 
different sets of cities can be grouped according to their similarity in succes-
determining features. In doing so, we may be able to infer what are the characteristics
of these groups of cities and how they may relate to why a set of parameters may be of
importance for this group.  

{% include img_compare.html 
  image_url="assets/dropdown_metrics.html"
%}

-----

insert here heat map explanation

-----

From the heatmaps above, clusters of cities showing various degrees of similarity can be 
identified. Similarities were evaluated over several targets: each of our success metrics 
and a multi-target approach that finds out the features that contribute most to a 
combination of all the metrics. Depending on the selected target, different clusters are 
formed, defined by a corresponding set of relevant features.

We see....

Now let's get a better look at the clusters...

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



#### reste du truc des autres



[_quartiers_][quartiers_lausanne].



Our first [dataset][asit] consists of the geographical, [cadastral] and address
data behind [map.lausanne.ch](https://map.lausanne.ch). It features the owner of
each of the almost 8000 plot

[^1]:  
    This number does not account for PPE (_prorpiété par étage_). If a house's
    flats are owned by individuals the dataset does not distinguish the
    different owners. It just indicates PPE.




{: .owner-legend }
 - {: .public } public institutions: _the city, the swiss railways etc._

- {: .pension } pension or similar funds: _investment foundations, the city's
  pension fund, etc._

 - {: .corp } corporations: _listed public companies like Swiss Life S.A., Régie
  Chamot & Cie S.A. etc._

 - {: .coop } cooperatives: _registered cooperative companies like Migros, la
  Mobilière etc._

 - {: .foundation } foundations and associations: _for example the olympic foundation for
    cultural heritage._

 - {: .ppe } PPE: _single flats in a building owned by different private people
 -- in french_ proriété par étage.

 - {: .private } individual privates: _private citizens owning an entire building._


If we look at the data as a map a very noisy mosaic shows up.







{% include question.html in_text=true
 text="What makes rents in Lausanne expensive?"
 image_url="assets/img/belair.jpg"
%}




![Linear regression on the rent prices](assets/export/distance.svg)


{% include question.html in_text=true
 text="What have we learned from it?"
 image_url="assets/img/Lausanne_img_0585.jpg"
%}



[^2]: All images are from [wikimedia commons](https://commons.wikimedia.org/wiki/Category:Lausanne).

[_Ouchy_]: https://map.geo.admin.ch/?lang=en&topic=ech&bgLayer=ch.swisstopo.pixelkarte-farbe&layers=ch.swisstopo.zeitreihen,ch.bfs.gebaeude_wohnungs_register,ch.bav.haltestellen-oev,ch.swisstopo.swisstlm3d-wanderwege&layers_visibility=false,false,false,false&layers_timestamp=18641231,,,&E=2537733&N=1150883&zoom=7.498594761554026&crosshair=marker

[_Flon_]: https://map.geo.admin.ch/?lang=en&topic=ech&bgLayer=ch.swisstopo.pixelkarte-farbe&layers=ch.swisstopo.zeitreihen,ch.bfs.gebaeude_wohnungs_register,ch.bav.haltestellen-oev,ch.swisstopo.swisstlm3d-wanderwege&layers_visibility=false,false,false,false&layers_timestamp=18641231,,,&E=2537831&N=1152550&zoom=7.896666666666668&crosshair=marker

[Shannon entropy]: https://en.wikipedia.org/wiki/Entropy_(information_theory)
[linear regression]: https://en.wikipedia.org/wiki/Linear_regression
[k-nearest-neighbours]: https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm
[asit]: https://www.asitvd.ch/chercher/catalogue.html?view=sheet&guid=486&catalog=main&type=complete&preview=search_list
[cadastral]: https://en.wikipedia.org/wiki/Cadastre
[homegate_example]: https://www.homegate.ch/rent/real-estate/city-lausanne/matching-list?tab=list&o=sortToplisting-desc
[quartiers_lausanne]: https://www.lausanne.ch/en/officiel/statistique/quartiers/presentation-des-quartiers.html
[_zones foraines_]: https://www.lausanne.ch/en/officiel/statistique/quartiers/presentation-des-quartiers/90-zones-foraines.html
