# The blog

## Setup 
**Jekyll 2.x required**

```
gem install bundler
bundle install
```

## New post

```
octopress new post "Post Title"
```

To enable sharing and comments for the new post edit the header in the .md file and add this

```
share: true
comments: true
```

Also don't forget to set the author value. Author info is in _data/authors.yml

```
author: dino|mark|philip
```

## Running locally

When running locally through ```jekyll serve``` you'll need to update url setting in _config.yaml

```
url: http://localhost:4000
```

---
based on [So simple Theme](https://github.com/mmistakes/so-simple-theme) by [Michael Rose](https://github.com/mmistakes) 
