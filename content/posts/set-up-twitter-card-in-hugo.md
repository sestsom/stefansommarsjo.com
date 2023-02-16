+++
author = "Stefan Sommarsjö"
title = "Set Up Twitter Card in Hugo"
date = "2023-02-15"
description = "How to add Hugo twitter card"
thumbnail = "/img/random/pythoncross.jpg"
twitter_creator: "@sestsom"

tags = [
    "Hugo",
	"Twitter",
]
categories = [
    "Developing",
    "Coding",
]
series = ["Coding"]
aliases = ["set-up-twitter-card-in-hugo"]
draft = false
+++
Choose a Twitter Card type: Twitter offers several types of Cards, such as summary, summary_large_image, app, player, and more. You can choose the card type that suits your content the best. In this example, we will use the summary_large_image card, which allows for a large image and a title, description, and website URL.

Add meta tags to the site head: Open the head.html file in your Hugo theme, and add the following meta tags to the head section:
<!--more-->


```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="{{ .Title }}">
<meta name="twitter:description" content="{{ .Description }}">
<meta name="twitter:image" content="{{ .Site.BaseURL }}{{ .Params.images }}">
<meta name="twitter:site" content="{{ .Site.Params.twitter }}">
```

These meta tags tell Twitter what type of Card you want to use, and what information to display. Note that we are using Hugo variables (such as .Title and .Description) to populate the content dynamically.

Set up front matter for each post: In each post's front matter, you can add additional metadata for Twitter Cards. Here's an example:
```html
---
title: My awesome post
description: This is a summary of my post that will be displayed on Twitter
images: /images/my-post-image.png
twitter_creator: "@myusername"
---
```

In this example, we've added the post's title and description, as well as the URL for the post's image. We've also included the Twitter username of the post's creator.

Test the Cards: Once you've set up Twitter Cards for your Hugo site, you should test them to make sure they are displaying properly. You can use Twitter's Card Validator tool to do this. Simply enter the URL of one of your posts, and the tool will display the Card that Twitter will use when someone shares that post.


