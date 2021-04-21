---
title: Migrated my blog from AWS to GitHub
tags:
  - Website migration
  - Blog
  - CSS
  - Github
categories:
  - - life
  - - HTML+CSS
  - - GitHub
description: >-
  I spent a week to migrated my blog from AWS to GIthub pages. Thanks to the
  powerful blog framework HEXO, the process of migrated and deployed is very
  simple. Then I can focus on the theme's custom and optimize. In this article,
  I will not describe the specific of each step, but the key points. Hope it
  could help you.
id: ‘8’
abbrlink: 13264
date: 2021-04-09 14:18:51
---

<style>
  .box {width:60%; text-align:center; font-size:10px; margin:0 auto;}
  .box img {border-radius: 10px;}
</style>

Although I have registered on GitHub more than 6 years, I didn't really start using it until last year, then felt its convenience immediately. During the touch I got that GitHub provide a static site hosting service named GitHub Pages. With this service, you can host your site with 'github.io' domain or your custom domain.
The default site generator on GitHub is JekyII. Of course there are a lot of open source generator which support GitHub Pages you can choose, such as my choice: Hexo.

---

## About GitHub Pages and Hexo

>**[GitHub Pages](https://docs.github.com/en/github/working-with-github-pages/about-github-pages)** is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub, optionally runs the files through a build process, and publishes a website.
>
>**[Hexo](https://hexo.io/)** is a fast, simple & powerful blog framework. It includes a lot of powerful features such as fast blazing, Markdown support, one-command deployment and plugin support.

## Custom domain

After deployed your site, the default domain will be 'www.[your name].github.io', of course you can custom it if you have a personal domain.

- Save your domain in the repository setting
- Go to your DNS server add an A record and a CNAME record, done
- For the specific step click [here](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages).

## Select a theme from internet and custom it by yourself

There are a lot of excellent open source themes on the internet and you can select it as you prefer. In fact, a theme only provide a basic style for your blog, there is no one that happens to meet all your preferences. In order to custom your blog, my suggestion is study a few HTML and CSS grammars. It doesn't means the specific grammar or elements, but the structures, to understand how does the "wheel" work.

My favorite theme is **[NEXT](https://github.com/theme-next/hexo-theme-next)**:

<div class="box">
  <img src="https://user-images.githubusercontent.com/16272760/63487983-da41b080-c4df-11e9-951c-64883a8a5e9b.png" alt="NEXT" />
</div>

>NEXT is a high quality elegant Hexo theme.

## Multi-computer syn management

When it comes to version control, the first thing in your mind is GitHub definitely, you are right, the best solution to manage Hexo blog is GitHub also. What you need to do is create a new branch in your page repository, then upload the source files.

The working principle is that your website page is deployed at master branch, but the source files you need to upgrade is pulled to the branch that you were created.

---

Above just introduced a few key steps to deploy a website on GitHub pages. There are great number tutorials on the web. Also, if you have any question please leave it in the comments and we can study together.
