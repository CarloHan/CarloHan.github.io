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
id:
description: I spent a week to migrated my blog from AWS to GIthub pages. Thanks to the powerful blog framework HEXO, the process of migrated and deployed is very simple. Then I can focus on the theme's custom and optimize. In this article, I will not describe the specific of each step, but the key points. Hope it could help you.
---

<style>
  .box {width:60%; text-align:center; font-size:10px; margin:0 auto;}
  .box img {border-radius: 10px;}
</style>

<div class="box">
  <img src=" " alt=" " />
</div>

Although I have registered on GitHub more than 6 years, I did't really start using it until last year, then felt its convenience immediately. During the touch I got that GitHub provide a static site hosting service named GitHub Pages. With this service, you can host your site on 'github.io' domain or your custom domain fastly.
The default site generator on GitHub is JekyII. Of course there are a lot of open source generator which support GitHub Pages you can choose, such as my choice: Hexo.

## About GitHub Pages and Hexo

>**[GitHub Pages](https://docs.github.com/en/github/working-with-github-pages/about-github-pages)** is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub, optionally runs the files through a build process, and publishes a website.
>
>**[Hexo](https://hexo.io/)** is a fast, simple & powerful blog framework. It includes a lot of powerful features such as fast blazing, Markdown support, one-command deployment and plugin support.

## Custom domain

After deployed your site, the default domain will be 'www.[your name].github.io', of course you can custom it if you have a personal domain: save your domain in the repository setting, then go to your DNS server add an A record and a CNAME record, done. For the specific step click [here](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages).

## 