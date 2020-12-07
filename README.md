# PageRank

## This operates as a search engine

This code computes PageRank by implementing equation 5.1 found in https://galton.uchicago.edu/~lekheng/meetings/mathofranking/ref/langville.pdf

Give it a try! 

UPDATE: now we can return urls that are closely related to the --search_query. Adjusting some hyperparameters can change the results to focus on urls matching the --search_query exactly. 

First I updated the url_satisfies_query funcion to return true for the search query and the 5 words most similar to the search query 
(according to gensim.downloader.load('glove-twitter-25')) 
```
python pagerank.py --data=./lawfareblog.csv.gz --search_query='weapons'

INFO:root:rank=0 pagerank=0.04005281254649162 url=www.lawfareblog.com/why-did-you-wait-moral-emptiness-and-drone-strikes
INFO:root:rank=1 pagerank=0.024694116786122322 url=www.lawfareblog.com/dc-district-court-dismisses-journalists-drone-lawsuit
INFO:root:rank=2 pagerank=0.022750990465283394 url=www.lawfareblog.com/revived-cia-drone-strike-program-comments-new-policy
INFO:root:rank=3 pagerank=0.021692432463169098 url=www.lawfareblog.com/us-court-appeals-dc-circuit-dismisses-suit-over-us-drone-strike
INFO:root:rank=4 pagerank=0.017879409715533257 url=www.lawfareblog.com/iran-shoots-down-us-drone-domestic-and-international-legal-implications        
INFO:root:rank=5 pagerank=0.017875775694847107 url=www.lawfareblog.com/german-courts-weigh-legal-responsibility-us-drone-strikes
INFO:root:rank=6 pagerank=0.011944924481213093 url=www.lawfareblog.com/slaughterbots-and-other-anticipated-autonomous-weapons-problems
INFO:root:rank=7 pagerank=0.00916246697306633 url=www.lawfareblog.com/faa-wants-hear-you-about-privacy-and-domestic-drones
INFO:root:rank=8 pagerank=0.008907114155590534 url=www.lawfareblog.com/very-low-tech-drone-smackdown
INFO:root:rank=9 pagerank=0.008891156874597073 url=www.lawfareblog.com/ryan-calo-faas-setback-domestic-drones
```
Since the pagerank for urls containing drones is much higher than urls containing weapons, there are alot of results for drones. 

This is how similarity is defined: 

```
>>> import gensim.downloader
>>> vectors = gensim.downloader.load('glove-twitter-25')

>>> vectors.most_similar('weapons')
[('drones', 0.8980589509010315), ('drone', 0.8965808749198914), ('assault', 0.8937928676605225), ('targets', 0.8834593296051025), ('firearms', 0.8833326101303101), ('weapon', 0.8730441927909851), ('hiv', 0.8625047206878662), 
('laws', 0.8613511919975281), ('drug', 0.8555658459663391), ('concealed', 0.8548306822776794)]
```



Next I updated the search function to increase the pagerank based on how similar the webpage url is to the --search_query. Adjusting --sumts_weight changes the results. 

Take a look;

```
 python pagerank.py --data=./lawfareblog.csv.gz --search_query='biden' --sumts_weight=.005

INFO:root:rank=0 pagerank=0.5526832938194275 url=www.lawfareblog.com/james-comey-hillary-clinton-and-email-investigation-guide-perplexed
INFO:root:rank=1 pagerank=0.5518247485160828 url=www.lawfareblog.com/fbi-director-comeys-statement-hillary-clintons-use-private-email-server
INFO:root:rank=2 pagerank=0.5517845153808594 url=www.lawfareblog.com/lawsuit-filed-against-hillary-clinton
INFO:root:rank=3 pagerank=0.5517845153808594 url=www.lawfareblog.com/hillary-clinton-encryption-problem-be-solved
INFO:root:rank=4 pagerank=0.5517845153808594 url=www.lawfareblog.com/hillary-clinton-addresses-iran-deal-brookings
INFO:root:rank=5 pagerank=0.5517253279685974 url=www.lawfareblog.com/peter-keisler-trumps-promise-jail-hillary-clinton
INFO:root:rank=6 pagerank=0.5516722798347473 url=www.lawfareblog.com/peter-smiths-search-hillary-clintons-emails-subplot-thickens
INFO:root:rank=7 pagerank=0.19047796726226807 url=www.lawfareblog.com/hillarys-email
INFO:root:rank=8 pagerank=0.19047796726226807 url=www.lawfareblog.com/rational-security-hillary-and-hellfire-edition
INFO:root:rank=9 pagerank=0.17052996158599854 url=www.lawfareblog.com/charlie-savage-romney-team-memo-interrogation
INFO:root:rank=10 pagerank=0.17042067646980286 url=www.lawfareblog.com/would-president-romney-bring-back-enhanced-interrogation
```

```
python pagerank.py --data=./lawfareblog.csv.gz --search_query='biden' --sumts_weight=.5

INFO:root:rank=0 pagerank=0.5526832938194275 url=www.lawfareblog.com/james-comey-hillary-clinton-and-email-investigation-guide-perplexed
INFO:root:rank=1 pagerank=0.5518247485160828 url=www.lawfareblog.com/fbi-director-comeys-statement-hillary-clintons-use-private-email-server
INFO:root:rank=2 pagerank=0.5517845153808594 url=www.lawfareblog.com/lawsuit-filed-against-hillary-clinton
INFO:root:rank=3 pagerank=0.5517845153808594 url=www.lawfareblog.com/hillary-clinton-encryption-problem-be-solved
INFO:root:rank=4 pagerank=0.5517845153808594 url=www.lawfareblog.com/hillary-clinton-addresses-iran-deal-brookings
INFO:root:rank=5 pagerank=0.5517253279685974 url=www.lawfareblog.com/peter-keisler-trumps-promise-jail-hillary-clinton
INFO:root:rank=6 pagerank=0.5516722798347473 url=www.lawfareblog.com/peter-smiths-search-hillary-clintons-emails-subplot-thickens
INFO:root:rank=7 pagerank=0.500001072883606 url=www.lawfareblog.com/trump-encourages-china-investigate-biden-family-clouding-trade-talks
INFO:root:rank=8 pagerank=0.5 url=www.lawfareblog.com/live-brookings-host-vice-president-joe-biden
INFO:root:rank=9 pagerank=0.5 url=www.lawfareblog.com/new-obama-biden-campaign-bumper-sticker
INFO:root:rank=10 pagerank=0.19047796726226807 url=www.lawfareblog.com/hillarys-email
```





Here are all the tasks I have had this program run prior to 12/6/2020: 
They do not have the hyperparameter options, but are helpful to look at. 

To implement this version comment out line 188, change line 209 to "url_satisfies_query_notsim(url,query):" -- you'll get the results below. 


```
$ pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona' --search_query='-corona'
```
returns:

```
rank=0 pagerank=8.8870e-01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
rank=1 pagerank=8.8867e-01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
rank=2 pagerank=1.8256e-01 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
rank=3 pagerank=1.0729e-01 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
rank=4 pagerank=9.4298e-02 url=www.lawfareblog.com/lawfare-podcast-mom-and-dad-talk-clinirank=5 pagerank=7.9633e-02 url=www.lawfareblog.com/fault-lines-foreign-policy-quarantined                                                                     uarantined
rank=6 pagerank=7.5307e-02 url=www.lawfareblog.com/limits-world-health-organization                                                                           tion      
rank=7 pagerank=6.8115e-02 url=www.lawfareblog.com/chinatalk-dispatches-shanghai-beijing-i-beijing-and-hong-kong
rank=8 pagerank=6.4847e-02 url=www.lawfareblog.com/us-moves-dismiss-case-against-company-t-company-linked-ira-troll-farm
rank=9 pagerank=6.4847e-02 url=www.lawfareblog.com/livestream-house-armed-services-holds-ces-holds-hearing-national-security-challenges-north-and-south-america
```

```

```

```
pagerank.py --data=./small_now.csv.gz --verbose

computing indices
computing values
found epsilon
rank=0 pagerank=2.1634e+00 url=4
rank=1 pagerank=1.6664e+00 url=6
rank=2 pagerank=1.2402e+00 url=5
rank=3 pagerank=4.5712e-01 url=2
rank=4 pagerank=3.5620e-01 url=3
rank=5 pagerank=3.2078e-01 url=1
```

```
pagerank.py --data=./lawfareblog.csv.gz --search_query='corona'

rank=0 pagerank=4.5861e-03 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
rank=1 pagerank=4.0460e-03 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
rank=2 pagerank=2.6116e-03 url=www.lawfareblog.com/britains-coronavirus-response
rank=3 pagerank=2.5390e-03 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
rank=4 pagerank=2.3557e-03 url=www.lawfareblog.com/israeli-emergency-regulations-location-tracking-coronavirus-carriers
rank=5 pagerank=2.2895e-03 url=www.lawfareblog.com/why-congress-conducting-business-usual-face-coronavirus
rank=6 pagerank=2.2727e-03 url=www.lawfareblog.com/livestream-house-oversight-committee-holds-hearing-government-coronavirus-response
rank=7 pagerank=2.2520e-03 url=www.lawfareblog.com/congressional-homeland-security-committees-seek-ways-support-state-federal-responses-coronavirus
rank=8 pagerank=2.1878e-03 url=www.lawfareblog.com/paper-hearing-experts-debate-digital-contact-tracing-and-coronavirus-privacy-concerns
rank=9 pagerank=2.0339e-03 url=www.lawfareblog.com/cyberlaw-podcast-how-israel-fighting-coronavirus
```
```
pagerank.py --data=./lawfareblog.csv.gz --search_query='trump'

rank=0 pagerank=6.6243e-02 url=www.lawfareblog.com/donald-trump-and-politically-weaponized-executive-branch
rank=1 pagerank=6.0194e-02 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
rank=2 pagerank=3.4969e-02 url=www.lawfareblog.com/trump-administrations-worrying-new-policy-israeli-settlements
rank=3 pagerank=3.2193e-02 url=www.lawfareblog.com/document-trump-revokes-obama-executive-order-counterterrorism-strike-casualty-reporting
rank=4 pagerank=3.0971e-02 url=www.lawfareblog.com/dc-circuit-overrules-district-courts-due-process-ruling-qasim-v-trump
rank=5 pagerank=2.8460e-02 url=www.lawfareblog.com/how-trumps-approach-middle-east-ignores-past-future-and-human-condition
rank=6 pagerank=2.5252e-02 url=www.lawfareblog.com/why-trump-cant-buy-greenland
rank=7 pagerank=2.2457e-02 url=www.lawfareblog.com/oral-argument-summary-qassim-v-trump
rank=8 pagerank=2.1462e-02 url=www.lawfareblog.com/dc-circuit-court-denies-trump-rehearing-mazars-case
rank=9 pagerank=2.1103e-02 url=www.lawfareblog.com/second-circuit-rules-mazars-must-hand-over-trump-tax-returns-new-york-prosecutors
```

```
pagerank.py --data=./lawfareblog.csv.gz

rank=0 pagerank=8.4156e+00 url=www.lawfareblog.com/our-comments-policy
rank=1 pagerank=8.4156e+00 url=www.lawfareblog.com/lawfare-job-board
rank=2 pagerank=8.4156e+00 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
rank=3 pagerank=8.4156e+00 url=www.lawfareblog.com/subscribe-lawfare
rank=4 pagerank=8.4156e+00 url=www.lawfareblog.com/support-lawfare
rank=5 pagerank=8.4156e+00 url=www.lawfareblog.com/upcoming-events
rank=6 pagerank=8.4156e+00 url=www.lawfareblog.com/snowden-revelations
rank=7 pagerank=8.4156e+00 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site
rank=8 pagerank=8.4156e+00 url=www.lawfareblog.com/topics
rank=9 pagerank=8.4156e+00 url=www.lawfareblog.com/documents-related-mueller-investigation
```

```
pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2

rank=0 pagerank=4.6091e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
rank=1 pagerank=2.9867e+00 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
rank=2 pagerank=2.9669e+00 url=www.lawfareblog.com/opening-statement-david-holmes
rank=3 pagerank=2.0173e+00 url=www.lawfareblog.com/senate-examines-threats-homeland
rank=4 pagerank=1.8769e+00 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
rank=5 pagerank=1.8762e+00 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
rank=6 pagerank=1.8693e+00 url=www.lawfareblog.com/whats-house-resolution-impeachment
rank=7 pagerank=1.7655e+00 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
rank=8 pagerank=1.6807e+00 url=www.lawfareblog.com/summary-david-holmess-deposition-testimony
rank=9 pagerank=9.8346e-01 url=www.lawfareblog.com/events
```
```
pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999


rank=0 pagerank=5.2385e+01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
rank=1 pagerank=5.2385e+01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
rank=2 pagerank=7.9438e+00 url=www.lawfareblog.com/cost-using-zero-days        
rank=3 pagerank=2.3700e+00 url=www.lawfareblog.com/lawfare-podcast-former-congressman-brian-baird-and-daniel-schuman-how-congress-can-continue-function       
rank=4 pagerank=1.5529e+00 url=www.lawfareblog.com/events
rank=5 pagerank=1.1867e+00 url=www.lawfareblog.com/water-wars-increased-us-focus-indo-pacific
rank=6 pagerank=1.1867e+00 url=www.lawfareblog.com/water-wars-drill-maybe-drill
rank=7 pagerank=1.1867e+00 url=www.lawfareblog.com/water-wars-disjointed-operations-south-china-sea
rank=8 pagerank=1.1867e+00 url=www.lawfareblog.com/water-wars-us-china-divide-shangri-la
rank=9 pagerank=1.1867e+00 url=www.lawfareblog.com/water-wars-sinking-feeling-philippine-china-relations
```
```
pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona'

rank=0 pagerank=8.8870e-01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
rank=1 pagerank=8.8867e-01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
rank=2 pagerank=1.8256e-01 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
rank=3 pagerank=1.4907e-01 url=www.lawfareblog.com/brexit-not-immune-coronavirus
rank=4 pagerank=1.4907e-01 url=www.lawfareblog.com/rational-security-my-corona-edition
rank=5 pagerank=1.0729e-01 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
rank=6 pagerank=1.0199e-01 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism      
rank=7 pagerank=1.0199e-01 url=www.lawfareblog.com/britains-coronavirus-response
rank=8 pagerank=9.4298e-02 url=www.lawfareblog.com/lawfare-podcast-mom-and-dad-talk-clinical-trials-pandemic  
rank=9 pagerank=8.7207e-02 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
```
