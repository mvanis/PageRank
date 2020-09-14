# PageRank
This code computes PageRank by implementing equation 5.1 found in https://galton.uchicago.edu/~lekheng/meetings/mathofranking/ref/langville.pdf

Try running it on small_now (to see how it works quickly), or adding more commands and running it on lawfareblog. 

For example;


pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona' --search_query='-corona'
returns:


rank=0 pagerank=8.8870e-01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
rank=1 pagerank=8.8867e-01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
rank=2 pagerank=1.8256e-01 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
rank=3 pagerank=1.0729e-01 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
rank=4 pagerank=9.4298e-02 url=www.lawfareblog.com/lawfare-podcast-mom-and-dad-talk-clinirank=5 pagerank=7.9633e-02 url=www.lawfareblog.com/fault-lines-foreign-policy-quarantined                                                                     uarantined
rank=6 pagerank=7.5307e-02 url=www.lawfareblog.com/limits-world-health-organization                                                                           tion      
rank=7 pagerank=6.8115e-02 url=www.lawfareblog.com/chinatalk-dispatches-shanghai-beijing-i-beijing-and-hong-kong
rank=8 pagerank=6.4847e-02 url=www.lawfareblog.com/us-moves-dismiss-case-against-company-t-company-linked-ira-troll-farm
rank=9 pagerank=6.4847e-02 url=www.lawfareblog.com/livestream-house-armed-services-holds-ces-holds-hearing-national-security-challenges-north-and-south-america
