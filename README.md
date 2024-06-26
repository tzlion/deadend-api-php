deadend-api-php
===============

Simple PHP Wrapper for X/Twitter API v1.1 and v2 calls

Forked from [J7mbo/twitter-api-php](https://github.com/J7mbo/twitter-api-php) to allow the continued operation of some personal projects.

**This library is not supported and v2 functionality has only been tested for certain limited use cases.**
**I do not recommend you develop against the X/Twitter API in general due to the instability of the platform and its management.**

Original documentation follows
------------------------------

**The documentation from this point has been minimally updated and may be outdated in parts!**

**[Changelog](https://github.com/J7mbo/twitter-api-php/wiki/Changelog)** ||
**[Examples](https://github.com/J7mbo/twitter-api-php/wiki/Twitter-API-PHP-Wiki)** ||
**[Wiki](https://github.com/J7mbo/twitter-api-php/wiki)**

[Instructions in StackOverflow post here](http://stackoverflow.com/questions/12916539/simplest-php-example-retrieving-user-timeline-with-twitter-api-version-1-1/15314662#15314662) with examples. This post shows you how to get your tokens and more. 
If you found it useful, please upvote / leave a comment! :)

The aim of this class is simple. You need to:

- Include the class in your PHP code
- [Create a twitter app on the twitter developer site](https://dev.twitter.com/apps/)
- Enable read/write access for your twitter app
- Grab your access tokens from the twitter developer site
- [Choose a twitter API URL to make the request to](https://dev.twitter.com/docs/api/1.1/)
- Choose either GET / POST (depending on the request) 
- Choose the fields you want to send with the request (example: `array('screen_name' => 'usernameToBlock')`)

You really can't get much simpler than that. The above bullet points are an example of how to use the class for a POST request to block a user, and at the bottom is an example of a GET request.

Installation
------------

**Normally:** If you *don't* use composer, don't worry - just include TwitterAPIExchange.php in your application.

```php
require_once('TwitterAPIExchange.php');
```

**Via Composer:**

```bash
composer require tzlion/deadend-api-php
```

How To Use
----------

#### Set access tokens ####

```php
$settings = array(
    'oauth_access_token' => "YOUR_OAUTH_ACCESS_TOKEN",
    'oauth_access_token_secret' => "YOUR_OAUTH_ACCESS_TOKEN_SECRET",
    'consumer_key' => "YOUR_CONSUMER_KEY",
    'consumer_secret' => "YOUR_CONSUMER_SECRET"
);
```

#### Choose URL and Request Method ####

```php
$url = 'https://api.twitter.com/1.1/blocks/create.json';
$requestMethod = 'POST';
```

#### Choose POST fields (or PUT fields if you're using PUT) ####

```php
$postfields = array(
    'screen_name' => 'usernameToBlock', 
    'skip_status' => '1'
);
```

#### Perform the request! ####

For v1.1 endpoints
```php
$twitter = new TwitterAPIExchange($settings);
echo $twitter->buildOauth($url, $requestMethod)
    ->setPostfields($postfields)
    ->performRequest();
```

For V2 endpoints (JSON POST request)
```php
$twitter = new TwitterAPIExchange($settings);
echo $twitter->buildOauth($url, $requestMethod)
    ->setPostfields($postfields, true)
    ->performRequest();
```

GET Request Example
-------------------

Set the GET field BEFORE calling buildOauth(); and everything else is the same:

```php
$url = 'https://api.twitter.com/1.1/followers/ids.json';
$getfield = '?screen_name=J7mbo';
$requestMethod = 'GET';

$twitter = new TwitterAPIExchange($settings);
echo $twitter->setGetfield($getfield)
    ->buildOauth($url, $requestMethod)
    ->performRequest();
```

That is it! Really simple, works great with the 1.1 API. Thanks to @lackovic10 and @rivers on SO!
