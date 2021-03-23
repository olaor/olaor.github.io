---
tags: github.io howto 
author: oo
---

# Setting up a blog on github.io

## Self-hosted blogs are a hazzle

We have all been blogging at one time or another. And if you are like
me you will at one point come to the realization that blogging is for
kids and people with botox. You will also start to feel the need to
write stuff down so you won't forget it...

I used to host my own [Wordpress](https://wordpress.org) blog. That
was a major drag. At one point or another there would be a security
hole and you would need to patch it and fix broken plugins and it's
generally a lot of work for those maybe two blog posts a year.

## What to do?

### Hosted blogs

Well, you could go for a [wordpress.com](https://www.wordpress.com)
Free account. But it's a lot of clicking and choices and gui stuff and
you are going to end up with a paid plan quite fast. Paying $40 for
mapping in your own domain name is a steep price for a `ServerAlias`
line in a config somewhere. That's probably the same for other
mainstream hosted blog sites. So I opted out of that whole thing.

### Static blog generators

There's a whole lot of those out there. But then you would need to
install those on your machine, and if you use multiple machines you'd
need to reinstall the generator and their dependencies and it turns
out that's a lot of hazzle as well

### Enter github.io and MarkDown

[github.io](https://pages.github.com/) offers free hosting for
personal blogs. And it bases your blog on a
[GitHub](https://github.com) repo. Also Free.

But the real kicker is that it allows you to write your blog in
markdown, which - much like
[LaTeX](https://en.wikipedia.org/wiki/LaTeX) - allows you to focus on
content and structure rather than spend a lot of time manually
formatting each and every page you want to publish. The system around
your content does that, and even if you CAN customize stuff until your
fingers bleed you don't HAVE to.

And even if you can edit your blog in a web interface you can also do
it with whatever text editor you fancy from Word on Wintendo to ed on
AIX.

# Let's get started

When I tried to set it up I managed to get myself into a howto that
explained that I had to install the page generator
[Jekyll](https://jekyllrb.com/) locally. 

Don't.

There is no need. Github is nice enough to run all your markdown files
through Jekyll when you check them in so you don't need to. And since
Jekyll is made in ruby it's going to be a lot of hazzle (I seem to
like that word.) with gems and environments and stuff. That's kind
of what we wanted to avoid.

## Set up your gihub repo

Start by [signing up to github.com](https://github.com). When that's
done you need to follow the excellent howto for [setting up your
website
repo](https://docs.github.com/en/github/working-with-github-pages/creating-a-github-pages-site).

## Set up some basics for Jekyll

You're up and running with `https://yourusername.github.io` then?
Awesome. You are almost there. 

1. Set up a few defaults for your site
   Create the file `_config.yml` at the root of your repo and fill it
   with this:
 
   ```yml
theme: jekyll-theme-hacker
title: Your blog name goes here
timezone: Europe/Oslo # Or UTC or whatever
   ```
 
 
 2. Create the file `index.md` where you show a list of posts like my
    front page does. Note the bits with `{% raw %}{{ post.title }}{%
    endraw %}` and such,
    that's called [Liquid template
    language](https://shopify.github.io/liquid/) and helps you do more
    fancy stuff than just generate text paragraphs:
	
```markdown
{% raw %}
## This is my blog

It has posts.

{% for post in site.posts %}
### {{post.date | date: "%Y-%m-%d"}} [{{ post.title }}]({{ post.url }}) by {{post.author}} 
{% endfor %}

_Last update: {{ "now" | date: "%Y-%m-%d %H:%M:%S"}}_
{% endraw %}
```

Commit the code in GitHub's text web based text editor or in your
locally cloned repo and after some seconds or even minutes your new
blog is ready for use.

## Fill your blog with content

But that's just the front page. You'd want to make some posts.

1. Create the `_posts` directory.

	As Github uses Jekyll, you would want to put all your blog posts
    in the `_posts` folder. Create it in your repo root folder. 

2.  Create a post

	Create a file named something like
    `2021-01-01-my-first-post.md`. It's really important to name the
    file with a date at the beginning or GitHub/Jekyll won't
    understand it's a post.

	Fill it with some nonsense:

```markdown
{% raw %}
---
tags: "first post" 
categories: Test "First posts"
author: "Beavis Butthead"
---

# First post!

Lorem ipsut!
{% endraw %}
```
 
Then commit and push that file, and hey presto (well, after waiting ut
to a minute for it to render...), you have a blog!
 
 
