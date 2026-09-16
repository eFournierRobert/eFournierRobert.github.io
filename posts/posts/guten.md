---
template: post
title: "The joys of custom tooling"
excerpt: Migrating the website from Jekyll to Guten
date: 2026-09-15
tags:
  - posts
---

# The joys of custom tooling

Tooling is the kind of software that can be hit or miss. Everyone has a different idea
of what can be too much, too little, too complex, or too simple. This can go on and on.
The most-used tooling always has to account for the use cases of an enormous number of users,
and this can make it feel like you're adapting yourself, or the way you would make something,
to it. This situation makes a simple question arise: when is it too much for the user? Like I
said, everyone has their own answer to this.

Making my website is a situation where I put my foot down and had enough of the tooling I used. While
the friction kept mounting, I realized that the "cost" of making my own tooling, in terms of
time and complexity, was low. So, I made Guten, and we'll see in this article why I did this and
we'll do a small overview of how it affected my website, both good and bad.

## How this website was made

The idea of a website was something I had for a long time, but that I never really got around to. This
changed when someone recommended me [Jekyll](https://jekyllrb.com/). I liked how it was
a nice middle ground between the two "obvious" ways of making this kind of website.

On one end, making a static website in pure HTML/CSS is doable, but dealing with constantly repeating the markup for each page, manually updating the lists,
etc., would've been painful. It isn't the 90s anymore and I'm not using [Neocities](https://neocities.org/) (which is
really cool, by the way).

On the other end, I could have used something like [Angular](https://angular.dev/). It would've
worked, but it is just too much for the kind of website this is supposed to be. It doesn't
make sense to make this with a big JavaScript framework. Asking that much CPU and memory
just to show text and some images is ridiculous.

Jekyll falls right in the middle. It generates static pages in basically pure HTML, but lets you
make templates or list things without having you write everything yourself. Writing the articles in Markdown,
making some templates, and letting the generator do the heavy lifting feels like the modern way of making a static website.

## The problems of Jekyll

While using Jekyll, some things came up and started really bothering me over time. The first
one is more personal, while the second is somewhat of a deal breaker.

### Non-standard syntax

Jekyll uses a small templating language called [Liquid](https://jekyllrb.com/docs/liquid/). This
allows you to achieve the middle ground we talked about earlier. You can define some Liquid code
inside an HTML or Markdown template, and then the generator will transform it into what you asked.

Let's say I wanted to make a template that lists all the *posts* on my website. With Liquid, it
would look something like this:

```html
<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
```

The `{% ... %}` is Liquid syntax. This works fine, but the moment you have a formatter for HTML
that formats on save, this quickly becomes chaotic. It isn't standard HTML, so the formatter
doesn't understand what it is looking at and can butcher the markup. This makes the files difficult to read.

Of course, I could deactivate the formatter, format everything by hand, and call it a day, but this is the type
of small friction that mounts over time. I would also like to keep my Markdown and HTML as "pure"
as possible. Having Liquid sprinkled all over it made them extremely coupled to Jekyll.

This was clearly
shown when I tried to turn my articles into PDF files to see what it would look like in the famous
LaTeX style. I quickly realized that the small amount of Liquid I used for images in my Markdown
files isn't standard. This meant that, in the final file, I had the weird markup instead of the
images I wanted.

### Library conflicts

This is something more personal, and I don't know how it affects other Linux distributions or OSes,
to be honest, but Ruby itself became a problem. Just before I start, I'm not a Ruby developer and I don't
intend on becoming one, so maybe I did something wrong.

Jekyll is made in Ruby and this bleeds into the way you manage your website. You have to use Bundler, gems, etc. Ruby's
ecosystem has its own way of managing libraries and dependencies, and this became a source of friction
on my system.

Now, I don't want this to become a post on dependency management, but I found Ruby's model way too difficult to deal with.
Having to juggle
versions of libraries and avoid conflicting versions can become complicated very quickly. Python brought
virtual environments, but I think it feels like a workaround to the problem instead of an elegant solution.
I think a modern way to manage libraries is how Go or Rust handles them. Even JavaScript, with all
its downsides, has an easy way to handle dependencies for projects.

Anyway, this brought a bit of chaos to my computer. I installed the Arch Linux Jekyll package,
but that worked 50% of the way or something. Bundler was still requiring me to install things,
but if I installed those libraries through the Arch packages, they weren't the right versions
since Arch is a rolling distribution. Jekyll kept falling behind.

I could install the libraries
"manually" with Bundler, bypassing my package manager, but this meant that every time my system updated
and had to update those libraries, they were conflicting. A conflict meant I couldn't update and that
I had to manually clean up my system.

This is something that became enough of a nuisance that I didn't even want to update my website anymore, since it
meant playing this game all over again. The trouble even extended from my system to GitHub Actions,
also running into version conflicts at one point. I couldn't even fix that problem and had to get bailed out by someone else.

At that point, I realized that I had to change something. I couldn't continue fighting with Ruby just
to update my website or my computer. It was too much for something that should've been simple. After sitting down and
figuring out what I really needed from Jekyll, I took the time to write my own static website
generator and made it specifically tailored to my needs.

## Making Guten

All of this led me to make Guten, as in Gutenberg, over the last week. It is a small Go program that generates static
websites from Markdown and HTML templates without the added complexity of Jekyll. I also fully migrated
this website to it along with the GitHub Action for deployment.

### Advantages

The first advantage of using it was Go. Being a compiled language with no shared libraries apart from
standard C libraries means that I can install one binary and use it where I want.
I don't need to adapt my project to its build system or dependency management, since there's none.

This dramatically simplified the website since I could remove all the files that were related to Ruby
Gems and Bundler instead of the website. This made the repository more focused on what it is. Also, this meant
that, apart from the binary, I don't need to install anything else for it to work.

Another advantage was the removal of Liquid. I don't need something this complicated in my templates,
so being able to remove all the Liquid felt like cleaning up rather than downgrading. In Guten, listing
*posts*, like we did above, became this:

```html
{{ posts }}
```

This is much simpler and doesn't interfere much with the HTML. The removal of Liquid also meant that my
Markdown became standard Markdown. This made it possible for me to do other things with the files if I wish to,
since the syntax isn't directly attached to Guten.

You can see how all of this made my repository much smaller than with Jekyll, without losing much
functionality. Guten implements just enough of what Jekyll does that my website can work fine on it.

### Some drawbacks

Making a tool with the objective of trimming the fat and solving some issues can lead to some drawbacks.
Of course, I found some net positives for myself, but trimming fat is, at the end of the day, trimming
features.

One thing I could see becoming unpleasant is the lack of HTML includes. Currently, my website doesn't have
a navigation bar, which is a typical application of this, but it has some HTML that repeats between pages.
The fact Guten can't take those and copy them where you want for you will probably become a pain over time
if I start having a lot of repeating HTML. The ideal would be a solution that I could write once and let
Guten make the copies.

Another thing I lost is previews. If we take our example of listing *posts*, Liquid allows me to make
a custom HTML template for it. This is useful to customize the website. Right now, Guten has a
hard-coded HTML template for listing things, which is restrictive. The benefit is that I hardcoded the
way of making it on my website, but, if I want to change it later, I'll have to implement templating
for previews.

## Conclusion

To conclude, Jekyll is a great tool for making static websites, but it was too much for my use case.
This and other issues with Ruby brought me to make Guten, which is far easier to use in my situation.
Of course, there are drawbacks and there's no way that Guten will ever match Jekyll, but a lot of
the functionality I need can be implemented over time, when I need it.

Right now, Guten works more than fine for what I need it to do, and this is the joy of custom tooling.
We spend a lot of time using tools and, sometimes, we bend over backward and spend so much effort
trying to make what we want to do fit the tooling rather than the opposite. If I ever need more from
Guten, I'll implement it, but right now, it is a tool that fits like a glove to my website and I
can't ask for anything better.
