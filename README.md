# Kibana_Essentials
**This is a repository which is used in book Kibana Essentials.**

**Please use file named "tweet_ESv1.json"  if you are using elasticdump v1.0.x or more**

**Please use file named "tweet.json"  if you are using elasticdump less than v1.0.x**

Note:- Make sure you are not using elasticdump v2.x.x. If you are using it you will not be able to load tweets from file into the Elasticsearch indices. To install a particular version of elasticdump, use following command:-

**npm install elasticdump@1.1.4 -g**

----


Fetch Tweets using Elasticsearch Twitter River
==================================

Pre-requisites for installing Twitter River:-
-------------

You need to have Twitter oAuth tokens  (Consumer key, Consumer secret, Access Token and Access Token Secret). To obtain oAuth tokens kindly refer to Chapter 6, Real Time Twitter Data Analysis, in the section, Creating Twitter Developer Account.

Installing Elasticsearch Twitter River Plugin:-
------------

**Windows:-**
* Open Command Prompt.
*	Navigate till the elasticsearch installation directory.
*	Enter  the following command in command prompt : bin\plugin install elasticsearch/elasticsearch-river-twitter/2.5.0
*	Restart Elasticsearch after successful installation of twitter river plugin.

**Ubuntu:-**
*	Open Terminal.
*	Navigate till the elasticsearch installation directory.
*	Enter  the following command in command prompt : bin/plugin install elasticsearch/elasticsearch-river-twitter/2.5.0 
*	Restart Elasticsearch after successful installation of twitter river plugin.

You need to install a version matching your Elasticsearch version:

|       Elasticsearch    |Twitter River Plugin|                                                            Docs                                                                   |
|------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
|    master              | Build from source | See below                                                                                                                          |
|    es-1.x              | Build from source  | [2.7.0-SNAPSHOT](https://github.com/elasticsearch/elasticsearch-river-twitter/tree/es-1.x/#version-270-snapshot-for-elasticsearch-1x)|
|    es-1.6              |     2.6.0         | [2.6.0](https://github.com/elastic/elasticsearch-river-twitter/tree/v2.6.0/#version-260-for-elasticsearch-16)                  |
|    es-1.5              |     2.5.0         | [2.5.0](https://github.com/elastic/elasticsearch-river-twitter/tree/v2.5.0/#version-250-for-elasticsearch-15)                  |
|    es-1.4              |     2.4.2         | [2.4.2](https://github.com/elasticsearch/elasticsearch-river-twitter/tree/v2.4.2/#version-242-for-elasticsearch-14)                  |
|    es-1.3              |     2.3.0         | [2.3.0](https://github.com/elasticsearch/elasticsearch-river-twitter/tree/v2.3.0/#version-230-for-elasticsearch-13)                  |
|    es-1.2              |     2.2.0         | [2.2.0](https://github.com/elasticsearch/elasticsearch-river-twitter/tree/v2.2.0/#twitter-river-plugin-for-elasticsearch)          |
|    es-1.0              |     2.0.0         | [2.0.0](https://github.com/elasticsearch/elasticsearch-river-twitter/tree/v2.0.0/#twitter-river-plugin-for-elasticsearch)          |
|    es-0.90             |     1.5.0         | [1.5.0](https://github.com/elasticsearch/elasticsearch-river-twitter/tree/v1.5.0/#twitter-river-plugin-for-elasticsearch)          |

Create Twitter River 
------------

*	Open a text editor such as Notepad++ in Windows or vi/vim using Terminal in Ubuntu.
*	Create following configuration file:-

```
curl -XPUT localhost:9200/_river/twitter/_meta -d '
{	
    "type" : "twitter",
    "twitter" : {
		"geo_as_array" : true,
		"oauth" : {
            "consumer_key" : "XXXXXXXXXXXXXXXXXXXX",
            "consumer_secret" : "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
            "access_token" : "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
            "access_token_secret" : "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
        }
    }, 
    "index" : {
        "index" : "tweet",
        "type" : "tweet"
    }
}'

```
*	Save this twitter river configuration file using .sh extension. Example: twitterriver.sh

Run Twitter River 
------------

*	Go to Terminal in Ubuntu or open Git Bash in Windows.
*	Navigate to the folder containing twitter river configuration file.
*	sh filename
```
Ex: sh twitterriver.sh
```
*	On successful execution of twitter  river you will get following message:
```
{“_index”:”_river”,”_type”:”tweet”,”_id”:”_meta”,”_version”:1,”created”:true}
```
*	To delete the river enter following command in Terminal for Ubuntu or Git Bash for Windows:
```
curl –XDELETE localhost:9200/_river
```
It will stop  fetching tweets from twitter and will store fetched tweets in tweet index.

For more information on Elasticsearch Twitter river refer to Elasticsearch Twitter River GitHub Page:-
https://github.com/elastic/elasticsearch-river-twitter
