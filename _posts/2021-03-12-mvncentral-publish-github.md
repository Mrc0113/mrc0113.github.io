---
layout: post
title: Publishing Java Packages to Maven Central from Github for a new Domain
excerpt: "Over the past few weeks I went through the steps necessary to setup publishing of Java packages to Maven Central for a new domain. This was trickier than I thought so I figured I'd share what I did to hopefully help others :)"
categories: [post]
tags: []
comments: true
github_comments_issueid: 11
---

## Overview
Over the past few weeks I went through the steps necessary to setup publishing of Java packages to Maven Central for a new domain. This was trickier than I thought so I figured I'd share what I did to hopefully help others :)

I'm going to try to keep this short and to the point but feel free to let me know if you have any questions. 

I used the following resources when figuring out these steps so props to their creators!
* [OSSRH Guide](https://central.sonatype.org/pages/ossrh-guide.html) 
* [Publishing Java packages with Maven](https://docs.github.com/en/actions/guides/publishing-java-packages-with-maven)
* [How to Sign and Release to The Central Repository with GitHub Actions](https://gist.github.com/sualeh/ae78dc16123899d7942bc38baba5203c)

## Setting up OSSRH (The Repository)

### Get An Account

### Prove Domain Ownership

### Create Your User Token

## Configuring the Maven pom

## Create GPG Keys

### Create Your Keys

### Share Your Public Key

## Configure the Github Secrets

## Setting up the Github Action

## Running the Github Action

## Conclusion
Hope this was useful! Feel free to leave a comment if you have any questions :) 
