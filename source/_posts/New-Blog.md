---
title: New Blog
date: 2019-01-20 23:21:37
tags: meta, website
category: web
---

I finally decided to switch to a new format for my personal website. There were a few reasons I decided to do so.

The previous iterations of my website were somewhat crude. The first was very simple HTML/CSS, and before I understood good practices in terms of web development. I had no JS aside from [`particles.js`](https://github.com/VincentGarreau/particles.js/) inspired from LA Hacks 2015's signup website which I thought looked very cool. This version was not mobile friendly at all, and had only an "About" page with a HTML button that links to my Resume. The second iteration was slightly better, but to be honest I don't really remember much about it. I think I still wasn't using a web framework, but at the very least, had tabs for more conent (links to Twitter, Github, my resume, etc). My third iteration was much better. I used [React](https://reactjs.org/) to get more practice with it (I had more of an Angular background) and the whole thing was a lot better structured than my previous attempts. At this point, I had a good amount of experience in web development, so the website was mobile-friendly and took proper advantage of routes to prevent page reloads. However, after a while I realized that React still probably wasn't the best way to build a personal website. For one thing, adding pages was fairly tedious and unnecessarily so. I rarely updated my site because it took too long to change the appearance/layout.

I took a look at some other people's websites for inspiration and noticed a few trends. First, their website didn't have a link to an external blog site like Medium, but had in in their website itself. The pages were minimal, clean, and conveyed information very effectively. I believe some used services like Squarespace and Wix to manage their site, while others used Github Pages. I previously was using Github Pages with a custom domain and was fairly impressed by how seamless it was, but I wanted to see if there were other options out there. I came across an [article that described using Google Cloud Storage to host websites](https://cloud.google.com/community/tutorials/automated-publishing-cloud-build) and was fairly intrigued. Although not free, the costs were fairly low and I wanted to see if this was a better experience than Github Pages, so my blog will reside here for now.

For my static site generator, I decided on [Hexo.io](https://hexo.io/) after debating between a few options. I knew I wanted to write my content in pure Markdown, and it claims to have "Blazing Fast" file generation and ease of use. I also enjoy that it is Javascript-based, since I have a good amount of experience developing in JS. So far, I've been fairly pleased with the content, and I have since followed the instructions in the blog linked earlier to setup pushes to Cloud Storage via Google Cloud Build from Github triggers. This makes adding new content as simple as running `hexo generate` and then pushing to Github. The author of the linked tutorial also had a blog post on how to automate the process by building the website on a container first, which I will probably switch over to doing at a later time. For now, I'm doing a quick hack by adding the static page generation command to a Git pre-commit hook.

I'll try this format out for a while and see if I like it, or if I should switch back to Github Pages/Medium. Although I miss how easy it was to format articles on Medium, the lack of support for codeblock formatting really turned me off. With this, I can do nice stuff like this:

``` bash
echo "Until next time" > /dev/null
```