# Regular Expressions to Match Social Media Profiles
This repository lists regular expressions to match and extract URLs of social media profiles. For simplicity URLs have to be filtered beforehand, i.e. the regular expression has to be executed on a single URL. To do this, you could use a regular expression matching valid URLs or use a specific library, for example JSOUP for Java. Furthermore, only exact profile urls are matched (for example no profile urls inside a url referencing a post).

Please note:
If you want to extract social media links, there are possibly easier ways:

* I've created a [Python library called socials](https://github.com/lorey/socials) that uses these expressions to *automate url detection* and extraction.
You input the urls, it extracts the social media profiles.
* There's also a [Socials API](https://github.com/lorey/socials-api) you can use for free or deploy yourself.
You simply input any URL and it will fetch and return all social media links on this website. Try it [here](http://socials.karllorey.com/try).

If you're missing a particular platform, please feel free to add it.
Also feel free to add a test that does not work.
An explanation of how this repo works can be found in [CONTRIBUTING.md](CONTRIBUTING.md).
You might also open an issue, of course, I'm happy to help!

## Table of Contents
- [twitter](#twitter)
- [github](#github)
- [linkedin](#linkedin)
- [facebook](#facebook)
- [instagram](#instagram)
- [google plus](#google-plus)
- [skype](#skype)
- [telegram](#telegram)
- [email](#email)
- [phone](#phone)
- [stackoverflow](#stackoverflow)
- [stackexchange](#stackexchange)
- [stackexchange network](#stackexchange-network)
- [youtube](#youtube)
- [reddit](#reddit)
- [snapchat](#snapchat)
- [vimeo](#vimeo)
- [Monster Regex](#monster-regex)



## twitter

### user
```regex
(?:https?:)?\/\/(?:[A-z]+\.)?twitter\.com\/@?(?P<username>[A-z0-9_]+)\/?
```
Allowed for usernames are alphanumeric characters and underscores.


## github

### user
```regex
(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<login>[A-z0-9_-]+)\/?
```
Exclude subdomains other than `www.` as these redirect to github pages sometimes.

### repo
```regex
(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<login>[A-z0-9_-]+)\/(?P<repo>[A-z0-9_-]+)\/?
```
Exclude subdomains as these redirect to github pages sometimes.


## linkedin

### regular
```regex
(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/in\/(?P<permalink>[\w\-\_À-ÿ%]+)\/?
```
These are the currently used, most-common urls ending in /in/<permalink>

### pub
```regex
(?:https?:)?\/\/(?:www)?linkedin\.com\/pub\/(?P<permalink_pub>[A-z0-9_-]+)(?:\/[A-z0-9]+){3}\/?
```
These are old public urls not used anymore, more info at [quora](https://www.quora.com/What-is-the-difference-between-www-linkedin-com-pub-and-www-linkedin-com-in)


## facebook

### profile
```regex
(?:https?:)?\/\/(?:www\.)?(?:facebook|fb)\.com\/(?P<profile>(?![A-z]+\.php)(?!marketplace|gaming|watch|me|messages|help|search|groups)[A-z0-9_\-\.]+)\/?
```
A profile can be a page, a user profile, or something else. Since Facebook redirects these URLs to all kinds of objects (user, pages, events, and so on), you have to verify that it's actually a user. See https://developers.facebook.com/docs/graph-api/reference/profile

### profile by id
```regex
(?:https?:)?\/\/(?:www\.)facebook.com/(?:profile.php\?id=)?(?P<id>[0-9]+)
```



## instagram

### profile
```regex
(?:https?:)?\/\/(?:www\.)?(?:instagram\.com|instagr\.am)\/(?P<username>[A-Za-z0-9_](?:(?:[A-Za-z0-9_]|(?:\.(?!\.))){0,28}(?:[A-Za-z0-9_]))?)
```
The rules:

* Matches with one . in them disco.dude but not two .. disco..dude
* Ending period not matched discodude.
* Match underscores _disco__dude
* Max characters of 30 1234567890123456789012345678901234567890


## google plus

### username
```regex
(?:https?:)?\/\/plus\.google\.com\/\+(?P<username>[A-z0-9+]+)
```
Matches username.

### user id
```regex
(?:https?:)?\/\/plus\.google\.com\/(?P<id>[0-9]{21})
```
Matches profile numbers with exactly 21 digits.


## skype

### profile
```regex
(?:(?:callto|skype):)(?P<username>[a-z][a-z0-9\.,\-_]{5,31})(?:\?(?:add|call|chat|sendfile|userinfo))?
```
Matches Skype's URLs to add contact, call, chat. More info at [Skype SDK's docs](https://docs.microsoft.com/en-us/skype-sdk/skypeuris/skypeuris).


## telegram

### profile
```regex
(?:https?:)?\/\/(?:t(?:elegram)?\.me|telegram\.org)\/(?P<username>[a-z0-9\_]{5,32})\/?
```
Matches for t.me, telegram.me and telegram.org.


## email

### mailto
```regex
mailto:(?P<email>[A-z0-9_.+-]+@[A-z0-9_.-]+\.[A-z]+)
```
This is for scraping only and in no way usable as a validation.


## phone

### phone number
```regex
(?:tel|phone|mobile):(?P<number>\+?[0-9. -]+)
```
Should be cleaned afterwards to strip dots, spaces, etc.


## stackoverflow

### user
```regex
(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/users\/(?P<id>[0-9]+)\/(?P<username>[A-z0-9-_.]+)\/?
```
Username can be changed at any time, user_id is persistent.

### question
```regex
(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/questions\/(?P<id>[0-9]+)\/(?P<title>[A-z0-9-_.]+)\/?
```



## stackexchange

### user
```regex
(?:https?:)?\/\/(?:www\.)?stackexchange\.com\/users\/(?P<id>[0-9]+)\/(?P<username>[A-z0-9-_.]+)\/?
```
This is the meta-platform above stackoverflow, etc. Username can be changed at any time, user_id is persistent.


## stackexchange network

### user
```regex
(?:https?:)?\/\/(?:(?P<community>[a-z]+(?!www))\.)?stackexchange\.com\/users\/(?P<id>[0-9]+)\/(?P<username>[A-z0-9-_.]+)\/?
```
While there are some "named" communities in the stackexchange network like stackoverflow, many only exist as subdomains, i.e. gaming.stackexchange.com. Again, username can be changed at any time, user_id is persistent.


## youtube

### user
```regex
(?:https?:)?\/\/(?:[A-z]+\.)?youtube.com\/user\/(?P<username>[A-z0-9]+)\/?
```


### channel
```regex
(?:https?:)?\/\/(?:[A-z]+\.)?youtube.com\/channel\/(?P<id>[A-z0-9-\_]+)\/?
```


### video
```regex
(?:https?:)?\/\/(?:(?:www\.)?youtube\.com\/(?:watch\?v=|embed\/)|youtu\.be\/)(?P<id>[A-z0-9\-\_]+)
```
Matches youtube video links like https://www.youtube.com/watch?v=dQw4w9WgXcQ and shortlinks like https://youtu.be/dQw4w9WgXcQ


## reddit

### user
```regex
(?:https?:)?\/\/(?:[a-z]+\.)?reddit\.com\/(?:u(?:ser)?)\/(?P<username>[A-z0-9\-\_]*)\/?
```



## snapchat

### profile
```regex
(?:https?:)?\/\/(?:www\.)?snapchat\.com\/add\/(?P<username>[A-z0-9\.\_\-]+)\/?
```



## vimeo

### video
```regex
(?:https?:)?\/\/(?:(?:www)?vimeo\.com|player.vimeo.com\/video)\/(?P<id>[0-9]+)
```


### user
```regex
(?:https?:)?\/\/vimeo\.com\/user(?P<id>[0-9]+)
```


## Monster Regex
If you want to match all social media profiles with one regex, use this monster:

```regex
(?P<twitter__user>(?:https?:)?\/\/(?:[A-z]+\.)?twitter\.com\/@?(?P<twitter__user__username>[A-z0-9_]+)\/?)|(?P<github__user>(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<github__user__login>[A-z0-9_-]+)\/?)|(?P<github__repo>(?:https?:)?\/\/(?:www\.)?github\.com\/(?P<github__repo__login>[A-z0-9_-]+)\/(?P<github__repo__repo>[A-z0-9_-]+)\/?)|(?P<linkedin__regular>(?:https?:)?\/\/(?:[\w]+\.)?linkedin\.com\/in\/(?P<linkedin__regular__permalink>[\w\-\_À-ÿ%]+)\/?)|(?P<linkedin__pub>(?:https?:)?\/\/(?:www)?linkedin\.com\/pub\/(?P<linkedin__pub__permalink_pub>[A-z0-9_-]+)(?:\/[A-z0-9]+){3}\/?)|(?P<facebook__profile>(?:https?:)?\/\/(?:www\.)?(?:facebook|fb)\.com\/(?P<facebook__profile__profile>(?![A-z]+\.php)(?!marketplace|gaming|watch|me|messages|help|search|groups)[A-z0-9_\-\.]+)\/?)|(?P<facebook__profile_by_id>(?:https?:)?\/\/(?:www\.)facebook.com/(?:profile.php\?id=)?(?P<facebook__profile_by_id__id>[0-9]+))|(?P<instagram__profile>(?:https?:)?\/\/(?:www\.)?(?:instagram\.com|instagr\.am)\/(?P<instagram__profile__username>[A-Za-z0-9_](?:(?:[A-Za-z0-9_]|(?:\.(?!\.))){0,28}(?:[A-Za-z0-9_]))?))|(?P<google_plus__username>(?:https?:)?\/\/plus\.google\.com\/\+(?P<google_plus__username__username>[A-z0-9+]+))|(?P<google_plus__user_id>(?:https?:)?\/\/plus\.google\.com\/(?P<google_plus__user_id__id>[0-9]{21}))|(?P<skype__profile>(?:(?:callto|skype):)(?P<skype__profile__username>[a-z][a-z0-9\.,\-_]{5,31})(?:\?(?:add|call|chat|sendfile|userinfo))?)|(?P<telegram__profile>(?:https?:)?\/\/(?:t(?:elegram)?\.me|telegram\.org)\/(?P<telegram__profile__username>[a-z0-9\_]{5,32})\/?)|(?P<email__mailto>mailto:(?P<email__mailto__email>[A-z0-9_.+-]+@[A-z0-9_.-]+\.[A-z]+))|(?P<phone__phone_number>(?:tel|phone|mobile):(?P<phone__phone_number__number>\+?[0-9. -]+))|(?P<stackoverflow__user>(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/users\/(?P<stackoverflow__user__id>[0-9]+)\/(?P<stackoverflow__user__username>[A-z0-9-_.]+)\/?)|(?P<stackoverflow__question>(?:https?:)?\/\/(?:www\.)?stackoverflow\.com\/questions\/(?P<stackoverflow__question__id>[0-9]+)\/(?P<stackoverflow__question__title>[A-z0-9-_.]+)\/?)|(?P<stackexchange__user>(?:https?:)?\/\/(?:www\.)?stackexchange\.com\/users\/(?P<stackexchange__user__id>[0-9]+)\/(?P<stackexchange__user__username>[A-z0-9-_.]+)\/?)|(?P<stackexchange_network__user>(?:https?:)?\/\/(?:(?P<stackexchange_network__user__community>[a-z]+(?!www))\.)?stackexchange\.com\/users\/(?P<stackexchange_network__user__id>[0-9]+)\/(?P<stackexchange_network__user__username>[A-z0-9-_.]+)\/?)|(?P<youtube__user>(?:https?:)?\/\/(?:[A-z]+\.)?youtube.com\/user\/(?P<youtube__user__username>[A-z0-9]+)\/?)|(?P<youtube__channel>(?:https?:)?\/\/(?:[A-z]+\.)?youtube.com\/channel\/(?P<youtube__channel__id>[A-z0-9-\_]+)\/?)|(?P<youtube__video>(?:https?:)?\/\/(?:(?:www\.)?youtube\.com\/(?:watch\?v=|embed\/)|youtu\.be\/)(?P<youtube__video__id>[A-z0-9\-\_]+))|(?P<reddit__user>(?:https?:)?\/\/(?:[a-z]+\.)?reddit\.com\/(?:u(?:ser)?)\/(?P<reddit__user__username>[A-z0-9\-\_]*)\/?)|(?P<snapchat__profile>(?:https?:)?\/\/(?:www\.)?snapchat\.com\/add\/(?P<snapchat__profile__username>[A-z0-9\.\_\-]+)\/?)|(?P<vimeo__video>(?:https?:)?\/\/(?:(?:www)?vimeo\.com|player.vimeo.com\/video)\/(?P<vimeo__video__id>[0-9]+))|(?P<vimeo__user>(?:https?:)?\/\/vimeo\.com\/user(?P<vimeo__user__id>[0-9]+))

```
