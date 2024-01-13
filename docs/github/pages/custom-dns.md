---
title: Custom DNS
layout: home
nav_order: 1
grand_parent: GitHub
parent: GitHub Pages
permalink: docs/github/pages/custom-dns
last_modified_date: 2024-01-13
---

# Custom DNS

GitHub Pages allows you to use a custom domain for your websites, which means you can point a domain you own to your GitHub Pages site. This is often referred to as setting up custom DNS for GitHub Pages. By configuring the DNS settings for your domain, you can make it resolve to your GitHub Pages site, effectively associating your custom domain with your GitHub Pages website.

## Table of Contents


## Create CNAME file

To create a CNAME file for your custom domain, follow these steps:

1. Create a new file in the root of your GitHub Pages repository.
2. Name the file "CNAME" (without any file extension).
3. Open the "CNAME" file and add your custom domain (e.g., example.com) as the content of the file.

You can consult an example at [CNAME](https://github.com/user-cube/devops-cheatsheet/blob/main/CNAME)

## Crate DNS CNAME record

Navigate to your DNS provider and create a CNAME record that points your subdomain to the default domain for your site. For example, if you want to use the subdomain `www.example.com` for your user site, create a CNAME record that points `www.example.com` to `<user>.github.io`. 

If you want to use the subdomain `another.example.com` for your organization site, create a CNAME record that points `another.example.com` to `<organization>.github.io`. The CNAME record should always point to `<user>.github.io` or `<organization>.github.io`, excluding the repository name. For more information about how to create the correct record, see your DNS provider's documentation. For more information about the default domain for your site, see "[About GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites)".

### Configure DNS with Cloudflare

If you are using Cloudflare as your DNS provider, follow these steps to configure your custom domain:

1. Log in to your Cloudflare account.
2. Navigate to your domain's DNS settings.
3. Add a CNAME record with the name "www" and point it to `<user>.github.io`.
4. Ensure the CNAME record is proxied through Cloudflare to benefit from their security and performance features.

![dns-cname](https://user-cube.github.io/devops-cheatsheet/assets/images/github/dns-cname.jpeg)

## Configure GitHub Pages

To set up a `www` or custom subdomain, such as `www.example.com` or `blog.example.com`, you must add your domain in the repository settings. After that, configure a CNAME record with your DNS provider.

On GitHub, navigate to your site's repository.

Under your repository name, click ![settings](https://user-cube.github.io/devops-cheatsheet/assets/images/github/settings.svg) Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.

Screenshot of a repository header showing the tabs. The "Settings" tab is highlighted by a dark orange outline.

In the "Code and automation" section of the sidebar, click ![pages](https://user-cube.github.io/devops-cheatsheet/assets/images/github/pages.svg) Pages.

![pages-settings](https://user-cube.github.io/devops-cheatsheet/assets/images/github/github-pages-settings.png)