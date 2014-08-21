---
layout: post
title: "Moving Our Blog"
author: philip
share: true
comments: true
tags:
- blog
- jekyll
- tumblr
date: 2014-08-22T00:57:57+02:00
---

We've moved our blog from Tumblr to Jekyll hosted on Github. Here's why and how.

## Why move

We've been steadily growing tired/frustrated with our Tumblr blog. The initial charm of Tumblr's simplicity has worn off and we were left there staring at the holes in its functionality. Two things made particularly upset:

- inability to have multiple authors on the same blog
- lack of full control over blog's rendering and structure

'Today is the day', we decided. And moved. 

## Why Jekyll

The amount of respect we have for Robert Louis Stevenson can only be overshadowed by our passion for well designed software. So [Jekyll](http://jekyllrb.com/) was a natural choice. 
 
## How to move

We first picked a jekyll based theme for the blog. There are few of them out there but ["So Simple Theme"](https://github.com/mmistakes/so-simple-theme) by [Michael Rose](http://mademistakes.com/about/) looked especially promising.

After forking it and following Michael's [detailed explanations](http://mmistakes.github.io/so-simple-theme/theme-setup/), it was up and running. A few minor UI tweaks and we were getting closer.

I've adjusted the list of authors for the blog, updated twitter handles and all social jazz, setup Disqus instance for the blog, had a cup of tea.

## Bring your stuff with you       

We had about 10 posts in our Tumblr which we wanted to bring a long. The makers of Jekyll clearly take that stuff seriously. You can import your scribbles from pretty much anything but stones and papyrus. More details [here](http://import.jekyllrb.com/). Running the following script did the trick   

{% highlight ruby %}
$ ruby -rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::Tumblr.run({
      "url"            => "http://blog.thebakery.io",
      "format"         => "html", # or "md"
      "grab_images"    => false,  # whether to download images as well.
      "add_highlights" => false,  # whether to wrap code blocks (indented 4 spaces) in a Liquid "highlight" tag
      "rewrite_urls"   => false   # whether to write pages that redirect from the old Tumblr paths to the new Jekyll paths
    })'
{% endhighlight %}

## Host

Our [site](https://github.com/thebakeryio/thebakeryio.github.com) is already hosted on Github so we put [our blog](https://github.com/thebakeryio/blog) there as well. With master branch deleted and using a single branch "gh-pages" we are able to redeploy our blog with a single git push. 

## Ta-ta

That's it. Shoot a comment down below (now that we have proper comments in place), [say hi](mailto:hi@thebakery.io) and [follow us on twitter](http://twitter.com/bakeryhq). 