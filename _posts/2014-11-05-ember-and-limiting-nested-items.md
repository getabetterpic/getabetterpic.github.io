---
layout: post
title: Ember and limiting nested items
date: '2014-11-05T20:12:00.002-05:00'
author: Daniel Smith
tags: 
modified_time: '2014-11-05T20:12:24.844-05:00'
blogger_id: tag:blogger.com,1999:blog-358950712929443967.post-5796220492642714514
blogger_orig_url: http://www.getabetterpic.com/2014/11/ember-and-limiting-nested-items.html
---

One issue I have been facing lately is I have a model, let's call it Post
that then has a lot of child objects, like Comments. So Post hasMany Comments. 
But by default when you set these up in a model, setting async to true, if you're
using Ember Data it will call every single id listed in the comments array.
I've been trying to get around that so I can implement paging if I need to.    

For instance, say you have a url like `/posts/1/comments`. Without a way to limit
comments, by default it would load all of them at once. While trying to solve
this I wound up in the source code and stumbled across the piece I needed. 
It was [here](http://emberjs.com/api/data/classes/DS.ActiveModelAdapter.html#method_findHasMany). 
The key was the `findHasMany` method was looking for JSON from the server like this:



```json
{
  "post": {
    "id": 1,
    "title": "Rails is omakase",
    "links": { "comments": "/posts/1/comments" }
  }
}
```



So instead of the normal comments array, it is replaced by a links object that
specifies the url to hit for that resource. This in turn is just an index action
that I can limit to however many records I need for the first pull. This doesn't get me to paging yet, but it's a start.