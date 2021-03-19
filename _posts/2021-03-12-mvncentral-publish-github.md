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
The [Solace](solace.com) Developer Relations team recently launched our [SolaceCommunity github organization](github.com/SolaceCommunity] as a home for open source projects that are authored, maintained and supported by the amazing [Solace Community](solace.community). If you're interested in joining our community you can read more about it [here](https://solace.com/blog/announcing-new-solacecommunity-github-organization/), but that won't be the focus of the rest of this blog. The focus of this blog is how I enabled publishing of Java packges to Maven Central for this new github community. Since Java is one of our most used languages, and most Java projects now leverage Maven or Gradle, I wanted to enable developers contributing their Java projects to be able to easily publish to Maven Centralto make it easier for everyone in the community to easily use them. Over the past few weeks I went through the steps necessary to setup publishing of Java packages to Maven Central for the https://solace.community domain. This was trickier than I thought so I figured I'd share what I did to hopefully help others :)

I'm going to try to keep this short and to the point but feel free to let me know if you have any questions. 

I used the following resources when figuring out these steps so props to their creators!
* [OSSRH Guide](https://central.sonatype.org/pages/ossrh-guide.html) 
* [Publishing Java packages with Maven](https://docs.github.com/en/actions/guides/publishing-java-packages-with-maven)
* [How to Sign and Release to The Central Repository with GitHub Actions](https://gist.github.com/sualeh/ae78dc16123899d7942bc38baba5203c)

## Setting up OSSRH (The Repository)
There are a handful of approved repository hosting options specified by Maven Central. You can find the entire list [here](https://maven.apache.org/repository/guide-central-repository-upload.html#approved-repository-hosting), but the easiest approach seems to leverage [Open Source Software Repository Hosting (OSSRH)](http://central.sonatype.org/pages/ossrh-guide.html) so that's the approach I decided to take. 

*Note that if you're just trying to publish a few personal projects on github and are fine publishing under `io.github` you can skip this section*

### Get An Account
The first step down this road is to register a OSSRH account. This account will be used to prove ownership of your domain (for publishing packages), but also to manage your repositories in the future. Sign up for an account here](https://issues.sonatype.org/secure/Signup!default.jspa)

### Prove Domain Ownership
Now that you have an account the next step in the process is to prove ownership of the domain that matches the group that you'd like to publish to. Usually this is your domain name in reverse, so something like `com.company` if your domain is `company.com`. Since our developer community is at `solace.community` this meant we would publish to the `community.solace` group.   

To prove that we own this domain I had to execute a few simple steps: 
1. Open a [New Project Ticket](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134) with OSSRH. 
1. Follow the instructions request in the ticket to addd a DNS TXT record to our domain. 
1. Wait a few hours (it says it could take up to 2 business days) for the DNS TXT record to be verified. 
1. Check the ticket for confirmation that domain ownership has been confirmed.
1. Make a note to comment on this ticket after your first release to enable syncing to maven central!

### Create Your User Token
Now that we have permission to publish to our domain we need to create a user token for publishing. This token will be used as part of the publishing process. 

To get this token do the following: 
1. Login to the [OSSRH Nexus Repository Manager](https://s01.oss.sonatype.org/#welcome) w/ your OSSRH account
1. Go to your profile using the menu under your username at the top right.
1. You should see a list menu that is on the `Summary` page; change it to `User Token`. You can create your token on this page. 
1. Copy & Paste this token info so you can use it later! **(Keep it private!)**

✅ OSSRH is now ready to go and we have the info we need 

## Configuring the Maven pom
The next step is to setup our maven pom for publishing. Note that I used copy and paste programming to figure this out so I'm by no means an expert here :) 
If you are reading this and think I should include more detail here or my explanations are confusing please drop a comment and let me know.

Here is what I did: 
1. Ensured that my `groupId` starts with the reverse domain that we have approval to publish to! For example this is what we used, note that the `groupId` starts with `community.solace`
    ```
	<groupId>community.solace.spring.integration</groupId>
	<artifactId>solace-spring-integration-leader</artifactId>
	<version>1.1.0</version>
    ```
1. Include a description name, description and url pointing to your repository. 

1. Include a license, developers and organization(I believe this is optional) information. 
1. Add a profile for OSSRH which includes the `snapshotRepository` info, the `nexus-staging-maven-plugin`, and the `maven-gpg-plugin`
1. Include the `maven-release-plugin`, the `maven-javadoc-plugin`, the `maven-source-plugin` and the `flatten-maven-plugin` plugin. 

## Create GPG Keys

### Create Your Keys

### Share Your Public Key

## Configure the Github Secrets

## Setting up the Github Action

## Running the Github Action

## Conclusion
Hope this was useful! Feel free to leave a comment if you have any questions :) 
