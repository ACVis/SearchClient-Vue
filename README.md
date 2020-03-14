# SearchClient-Vue

Description  

Reason uses AWS’s search provider, Cloudsearch, to index and retrieve records from our site.
In this exercise, please build a JavaScript client (app, component, or single page) to query our
site search that meets the following requirements:

● The code and a functioning demonstration can be viewed. This could be in an online
sandbox, any publicly available hosted page, or even a self-contained file with clear
instructions.  
● The demonstration displays search results based on a user’s text input showing at least
headline, author bylines original published date, and an image, if available.  
● The demonstration includes some visual styling beyond the browser defaults. Use this as an opportunity to show your coding style and approach. Feel free to add features or enhance the design, but the priority should be on meeting the requirements and writing code
that can be understood by others. Feel free, but not obligated to use any framework, build tools, or code standards that you are comfortable with.

Our public endpoint can be found here:  
https://kvkbud4a7i.execute-api.us-west-2.amazonaws.com/production/

And can be simply queried like so:
https://kvkbud4a7i.execute-api.us-west-2.amazonaws.com/production/?q=test

Cloudsearch documentation can be found here:
https://docs.aws.amazon.com/cloudsearch/latest/developerguide/searching.html  

Note: we use the latest version (2013-01-01) of the Cloudsearch API, which is the version described in the above docs, in case you see mention of it. 