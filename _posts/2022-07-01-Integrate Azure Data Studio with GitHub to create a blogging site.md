---
layout: post
title:  Welcome to my Azure DP-300 Certification Blog!
date: 2020-07-02 20:00:00 -0300
categories: DP-300
---

# Quickstart: Use Azure Data Studio, Git, and Jekyll to create a blogging site on Github pages with ease.

<!-- 2. Introductory paragraph 
Required. Lead with a light intro that describes what the article covers. Answer the 
fundamental “why would I want to know this?” question. Keep it short.
-->

Traditionally, casual bloggers would need to look for services like Wordpress or Wix among many other providers to create a simple blog repository. Manitaning code files and other supporting files along with the blog needed separate storage. This quick start goes over how to use free tools such as Azure Data Studio, Git, Jekyll, and Github pages to create blogs with ease. 

## Resources

This section lists all the references that made this quick-start article possible. 
* R1: To enable Git with Azure Data Studio: https://docs.microsoft.com/en-us/sql/azure-data-studio/source-control?view=sql-server-ver16#git-support-in-azure-data-studio

* R2:  Azure Data Studio GIT Integration: https://www.youtube.com/watch?v=EmSrQCDsMv4

* R3: Jekyll Installation on Windows: https://kencenerelli.wordpress.com/2017/03/08/installing-jekyll-on-windows/

* R4: Jekyll installation on Windows (This one goes over msys related error) - https://gist.github.com/arthurattwell/281a5e1888ffd89b08b4861a2e3c1b35 

## Prerequisites

- Azure Data Studio - Download link [here](https://docs.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio?view=sql-server-ver16). -->
- This quick-start goes over the setup on a Windows Machine 
- Git for Windows. Azure Data Studio ships with a Git source control manager (SCM), but you still need to install Git (version 2.0.0 or later) before these features   
  are available. Note: Reference https://docs.microsoft.com/en-us/sql/azure-data-studio/source-control?view=sql-server-ver16 for the latest version of Git   
  installation-->
- Jekyll for Windows - Please refer to the resource R3 on the resources section for Jekyll installation walkthrough. Please note that you may get msys related errors 
  with Jekyll installation. If you run into that issue, the following additional commands to be executed to correct the issue: (Reference R3 from resources section)
  *  Install MSYS2. This provides extra tools required for Jekyll's native extensions. To do this, run choco install msys2. (More details here.) Again, close the 
     Command Prompt and open it again as an administrator.
  * Run the RIDK installer. Still more tools for native extensions. enter ridk install and at the prompts choose the default option to run options 1, 2 and 3 at once. 
  * Re-run the command gem install jekyll


## Watch this video walkthrough to create your first blog with Azure Data Studio

Video Walkthrough : Credit goes to https://www.youtube.com/watch?v=EmSrQCDsMv4

## Introduction

Github repositories can be enabled with Github pages. Github pages is a static hosting service that is integrated with Github repository. Github pages can be enabled on your repository in order to integrate your repo content and render it to your blogging site. Any changes to the repo are automatically built  by Jekyll and published to the blog. Jekyll is an open source software that builds the repository and publish to the Github pages blogging site. You can either edit the blog content directly online on Github or offline on a tool like Azure Data Studio. Blog posts can be created with markdown language. You can also include code snippets, embed  videos and images on your blog  articles. If using  Azure Data Studio, once  the post is complete, with a simple Git add, commit , and push you can upload the blog post to your Github repository. If Github repository is integrated with Github pages, Jekyll  automatically builds your repository and renders it on your blogging site.    

## Setup

1. Sign in to the [<Github> portal](https://github.com/).
2. Create a new repository on the Github portal. 
4. Create a Readme.MD file in order to create a main branch.
3. Enable Github pages on your Github repository. Note: The repository has to be public for enabling pages with the free offering.
4. Launch Azure Data Studio and clone this repository.
5. Open the terminal on Azure Data Studio and type the following:
  ```
  jekyll new . --Force
  ```
  This creates a new blog site with a folder called _posts that is the container for the blog post markdown files. 
  
## Author your blog posts

1. Create your blog posts under the _posts folder
2. Blog post file name follows the naming convention of date-title.md; Date should be formatted like this YYYY-MM-DD  
3. On the Azure Data Studio Command Prompt, issue the Git Commit command then a Git Sync command. With this, your blog posts are uploaded to your repository and 
   publised to the Github pages site


Happy blogging!
