feedly-get
==========


# Feedly-get

## Simple, read-only access to the Feedly Cloud API

Feedly-get is a module that provides convenience methods for read-only access to the Feedly Cloud API.  All methods return JSON objects and currently support the non-PRO queries to most of the entities in Feedly Cloud API including Feeds, Entries, Streams, Mixes, Search, Profile, Subscriptions, Categories, and Tags. 

I'm building an app that uses the Feedly Cloud API and the requirements of my app drove the features I added to this module. I will add more features as my application evolves.  


##

### NOTE: Because Feedly's authentication framework is completely outsourced to the OAuth ###implementation's of other apps - currently Twitter, Google, and WordPress. You'll need to use ###a web browser to manually log into Feedly, then copy the auth code (from the redirect URI) and ###include it in the instantiation of your feedly-get object.

For example, 

1. Get an authorization code from the feedly cloud

''' javascript
http://sandbox.feedly.com/v3/auth/auth?response_type=code&client_id=sandbox&scope=https%3A%2F%2Fcloud.feedly.com%2Fsubscriptions&redirect_uri=http%3A%2F%2Flocalhost''' 


2. Interact with the browser and login using your Twitter, WordPress, or Google account. 

-insert screenshot


3. Grab the code from the redirect URI

''' javascript
http://localhost/?code=AQAAN3B7InUiOiIxMTQxNjQ2ODcyMDUzMTE5NzM1NzgiLCJpIjoiNGQ3MjQ3ODctMDNmOC00MGRiLTg0YWEtN2RkNWU4MjFiMjRlIiwicCI6NiwiYSI6IkZlZWRseSBzYW5kYm94IGNsaWVudCIsInQiOjEzODc5OTA3NjYwODN9&state='''


4. Use this code when instantiating your feedly-get object.

''' javascript
var feedly = new FeedlyAPI(code, "http://sandbox.feedly.com", "sandbox", "${clientSecret}", "${redirectURI}")'''


5. Then you can request an Auth Token from the Feedly Cloud and start using the Feedly-get methods which require authentication. 

''' javascript 
var entryID = "vSbjObuspiUUUlHx496XW/WaRBw2NaRdTW1NAiwoLAs=_1431c635828:bf50:7cda226";
var id_list = null;

feedly.getStreamEntryIds(entryID, function(returnedInfo){id_list = returnedInfo}); '''