---
layout: post
title: "How I added the comments section"
---

Yesterday I created this blog and right after I pushed the initial commit to GitHub Pages, I realized that this blog lacks an important social component, that is the comments section.

## Minimal Mistakes

A quick search brought me to this incredible [post](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#comments) by Michael Rose dedicated to [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/), a flexible two-column Jekyll theme.

You will see that there is a large selection of blog comment hosting services, including [Disquis](https://disqus.com) and [Facebook](https://developers.facebook.com/docs/plugins/comments). In my case, I found it convenient relying on [utterances](https://utteranc.es), which uses GitHub Issues, the tracking tool integrated in my GitHub Pages repository, without need of relying in additional third party tools.

## Configuring utterances

First and foremost, we need to add utterances application to our GitHub Pages repository. To do that, go to utterances official site.

![21991](/assets/images/2021-12-30-adding-a-comments-section/21991.png)

Scroll down, until `configuration` section and click the `utterances app` link.

![12880](/assets/images/2021-12-30-adding-a-comments-section/12880.png)

Click `Install` button.

![23622](/assets/images/2021-12-30-adding-a-comments-section/23622.png)

Tell GitHub to install utterances only to GitHub Pages repository (which has to be public).

![12481](/assets/images/2021-12-30-adding-a-comments-section/12481.png)

Now that application has been added, you can simply add the following code at the bottom of each post.

``` html
<script
  async
  src="https://utteranc.es/client.js"
  repo="A5kar/A5kar.github.io"
  issue-term="title"
  theme="github-light"
  crossorigin="anonymous">
</script>
```

For instance, below is what you would get inside your code, while writing this post.

![20402](/assets/images/2021-12-30-adding-a-comments-section/20402.png)

## Way forward

So far, the solution seems simple and immediate. I wonder however what would be the way to add the above script at the end of each post, to avoid this repetitive task (which easily can lead to mistakes and bugs). If you know a way, jump in and be the first to comment below!

*NOTE: just to clarify, the solution I would like to see should not require using [third party themes](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll), or modifying the default (minima) theme. Locally, I can easily modify the local copy of the theme and add the above few lines to `_layouts/post.html`, but I believe this solution will not work in the remote GitHub Pages server, where a separate instance of Jekyll will generate the website files. Did not try it though, since it would require me to [upload](/2021/12/29/opening-a-blog.html#submit_initial_commit) the entire `vendor` folder (99 MB) to repository.*

<script
  async
  src="https://utteranc.es/client.js"
  repo="A5kar/A5kar.github.io"
  issue-term="title"
  theme="github-light"
  crossorigin="anonymous">
</script>
