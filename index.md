---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

---



 
From being a simple idea born inside the minds of two men, Brian Chesky and Joe Gebbia, 
unable to afford their rent, to becoming one of the best vacation rental sites, 
AirBnb has come a long way. As a matter of fact, the “air” in AirBnb came as a result of 
Brian and Joe renting an air mattress on their living room floor. 


#### A Bit of Background


Since its foundation in 2008, the company experienced a continuous growth with a boom 
after 2012, ending up to a revenue of 2.6 billions US dollars in 2017, 12736 employees 
in 2019 and an astonishing 2 millions people lodging with AirBnb each night in October 
2019. Today, AirBnb offers listings in 191 countries and counts about 150 millions users 
[1].

<iframe src="assets/html_graphs/Airbnb_world_map.html"></iframe>
Here-above is a graph depicting the worldwide presence of AirBnb from data obtained through
 Inside AirBnb.


With such astonishing numbers, one can’t help but wonder how to get a piece of the pie. 
More specifically, how can short term renting be turned into a sucessful business, to the
 point of being a source of income? If you are interested in the idea of subletting your
  properties and are considering AirBnb as the plateform to do so, then this data story 
  is for you! Indeed, with the help of a thorough analysis of AirBnb data, this article 
  will try to solve the mystery of profitable rentings by determining what makes a 
  listing sucessful.

  
Thus, answers are seeked for the following underlying questions of our problem:
•	What do people look for when booking an airbnb: what variables have the largest 
impact on a listing ?
•	What can be learned from the "big players" and "international players" of the Airbnb 
platform ? Are the same parameters important for all cities ?


#### Defining Success

Before getting down to business by pointing how to get make your listing reach the top, 
let’s get everybody on the same page by detailing what it means for a rented property to 
be successful. Quite naturally, the goal when renting a vacation housing would be to get 
the highest rating accompanied with good reviews and have custumers all year round. There
 are other indicators such as having customers come back to your place but for the purpose 
 of this study only the three factors listed previously will be taken into account. 
Since customers rate a listing over several criteria such as cleanliness or communication
, an overall rating that takes all of these aspects into account will account for client
satisfaction.
Additionally, due to Airbnb’s international presence, reviews are found in many languages.
 However, the majority of the customers write in English. These are the reviews, 
 which positivity is analysed. Rather than with positivity itself, reviews’ compound 
 values are analyzed. 
A compound value > 0.05 would demonstate positive reviews whereas values < -0.05 amounts 
for negative reviews. For values inbetween, reviews are thought as neutral.
 Finally, the booking frequency is estimated with the average number of reviews wrote for 
 a listing every months. Note that this is only an estimation since not all guests leave 
 reviews and they might have different length of stay. However it does provide information
  on the demand for a listing.

Now that we can all agree on a common definition of success it is time to understand what 
parameters have the most impact on a listing’s success.


insert
GRAPH DISTRIBUTION DES METRICS

By looking at the distribution of the success metric, some simple observations can be 
made. First, the average score is left skewed : very few listings have overall scores 
under 80/100. Then, reviews per months are right-skewed, that is, most listings receive 
very few reviews every months. Finally, the Gaussian distribution of compound values shows
 that most comments have compound values close to 0.5. Virtually no comment is negative, 
 most comments are positive or neutral. These distributions were obtained when inspecting
  the values of a single city : Amsterdam. This city was taken as a case study to build 
  analysis, which was extended to ...30... cities.  The resulting analysis is described in
  further detail in the following section.

{% include question.html in_text=true
  text="Zooming into a city at a time"
  image_url="assets/img/amsterdam_.jpg"
%}


To get more insight, the analysis focused, as a first step, on understanding the 
parameters that influence the most the success of an AirBnb in Amsterdam. Focusing on 
Amsterdam allowed us to strategically build an efficient framework that would later be 
applied to other cities, as we hypothesize that some parmeters may have location-dependant 
importances. Choosing Amsterdam was motivated by the fact that it ranks fifth in
 Europe’s most visited cities (citer source), such that many visitors potentially make use
  of the plateform, without the dataset being too large and computationally intensive. 
It is most likely for anyone who has ever gone on a touristic trip to developed
preferences in terms of housing to some extent, whether it be a price range, the distance 
to attractions and transportation or the type of accomodation. Indeed, it may be expected 
for someone visiting Amsterdam to want a rental place near the center, for a good price 
as well as possibly other services, such as an included breakfast. However the demography 
of travellers can be very diversified. Based on the age, interest, financial means,
 country of origin and so on, the appeal for a given listing may  be very different. 

{% include img_compare.html 
  image_url="assets/dropdown_sankey.html"
%}


Though there might be a high level of variability in the data, we still manage to 
identify certain trends in terms of which features contribute most to which metric. In 
fact, the Sankey diagram allows for these trends to be visualized. 
By placing your mouse on every connection between a parameter and the success metric 
it influences you can get the weight of this particular connexion. These weights reveal 
how much a parameter has influence over the different aspect of a listing’s success.
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
 
 
{% include question.html in_text=true
  text="From single cities to a worldwide view"
  image_url="assets/img/international.jpg"
%}

Even though interesting results were drawned in the previous section, it is time to go 
even further by investigationg highly touristic cities across the world. 

Let’s begin with the study of every aspect of success individually: for every country 
available on both the transport and airbnb dataset, let’s find out what aspect of a 
listing have the most impact on the booking frequency (review_per_month), the grade 
(review_score) and the positivity of the comments (compound) individually. 

{% include img_compare.html 
  image_url="assets/dropdown_metrics.html"
%}


GRAPH POLAR + HEATMAP AVEC ONGLET POUR COMPOUND, REVIEWS AND BOOKING FREQUENCY

A first interesting information at this point is how cities can be clustered on their 
parameters relevance in the success of a vacation rental. Indeed, 8 city-clusters appears.

PLOT POWERPOINT QUI REGROUPE LES CLUSTER

<iframe src="assets/dropdown_bubble.html"></iframe>



Directly following the first observation is that, as expected, what influences success 
varies depending on your location. For example, the time elapsed since one has been a 
host on Airbnb is the second most relevant parameter to getting good grades in cities 
in the fifth cluster whereas it only is the forth one for cities in the tenth cluster. 

Now that it is known for a fact that the location matters for how to handle your reting
 property, it is time to understand which parameters it would be in your best interest 
 to improve as best as possible. For that, a multi-target study might come in handy. 
 Indeed, it is time to look at success by considering all its aspects and to come up 
 with the best strategy for you to access the hosts’ elite. 

GRAPH POLAR + HEATMAP DE LA MULTITARGET ANALYSIS

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

<iframe src="assets/html_graphs/compound_importances_ranking_similarity_interactive.html"></iframe>

#### Conclusion and discussion

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






<iframe src="assets/export/by_rents_all_in_one.html"></iframe>


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
