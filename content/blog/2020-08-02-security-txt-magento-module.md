---
id: 1256
title: 'Security.txt Magento module'
date: '2020-08-02T03:12:38+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - Magento2
    - Security
---

With the recent release of Magento 2.4.0 open source and commerce, you can find a brand new module under vendor/magento/ directory named **module-securitytxt**. You may find it a small module, but you will amaze to know the importance of that module in terms of the security. Two years ago, I was reading the blog post from Troy Hunt and other reputed people in the security industry about this new file called Security.txt which allows security researchers to report security vulnerabilities to the right people in the organization. I am amazed by this, because of my personal experience in not getting hold of right people in the organization whenever I find any security vulnerability on any website. I found security issues on numerous websites before reading about security.txt, and tried many ways to reach out to the people in the organization in an effort to get a hold of someone who is responsible to fix this. I sent messages to the people working in that organizations via LinkedIn, Twitter DM, tech email addresses I could find from whois, customer service, etc.. But, zero replies!! Of course, who would want to reply to such scary messages about their website right?!

## Security.txt to the rescue

As soon as I learned about security.txt, I read many articles and checked its official website https://securitytxt.org/ to understand how it works. I really liked the concept, and thought to make it available to everyone in the very platform I love, Magento. I built Magento 2 module to allow administrators to input and store all the security contact details and signature in the database, which can be then easily viewed at the standard locations https://website.com/.well-known/security.txt and https://website.com/.well-known/security.txt.sig

Security.txt files have been adopted by many big players in the industry like Google, GitHub, LinkedIn and Facebook.

## Listen to the community

Right after building the module and pushing it to my Github [securitytxt repo](https://github.com/kalpmehta/securitytxt), I was gathering feedbacks about this new security standard from the Magento community. I asked many well known people in the community, at various events and Dev Exchange, to understand its pros/cons from other people’s perspective. Unsurprisingly, many were in favor of this. There were some people against having a dedicated module for this, because Magento already has many modules that not every merchants need but they still have to keep it because… it comes out of the box. Totally valid point. However, this is a security module and Magento 2 was already infested with security bugs in the early days and not to mention security bugs that gets introduced via third-party extensions. With the modular approach of the securitytxt, it is very convenient for any merchant to enable and input security contact details and save right from the admin, which hardly takes 2 minutes! I do not know why anyone would want to disable any security module tbh. Before the module, there were hardly any merchants who had uploaded security.txt file on their server, even though the argument was it is the easiest approach so why to introduce a module for that. Ultimately, reward outweighed the risk and it was decided to ship this module in the core bundle.

I presented security.txt’s importance in various meetups last year and gathered feedbacks from the event attendees as well.

## Security.txt in Magento 2.4.0

> Finally after 2 years my [\#magento](https://twitter.com/hashtag/magento?src=hash&ref_src=twsrc%5Etfw) community contributed module ([\#Security](https://twitter.com/hashtag/Security?src=hash&ref_src=twsrc%5Etfw).txt) is available OOTB with today's release of 2.4.0 version!! 🎉
> 
> Highly recommended to use it on all your upcoming 2.4 Magento stores.
> 
> Special thanks [@EdOverflow](https://twitter.com/EdOverflow?ref_src=twsrc%5Etfw) [@troyhunt](https://twitter.com/troyhunt?ref_src=twsrc%5Etfw) [@okorshenko](https://twitter.com/okorshenko?ref_src=twsrc%5Etfw) [@piotrekkaminski](https://twitter.com/piotrekkaminski?ref_src=twsrc%5Etfw) [pic.twitter.com/B4tc6picE5](https://t.co/B4tc6picE5)
> 
> — kalpesh.eth (@kalpmehta) [July 29, 2020](https://twitter.com/kalpmehta/status/1288335942940372992?ref_src=twsrc%5Etfw)

<script async="" charset="utf-8" src="https://platform.twitter.com/widgets.js"></script>

If you are working as a Magento developer in retail, please make sure you submit security contact details to the security.txt configuration in the admin panel. If you are at an SI/Agency, and responsible to manage your clients’ websites, please submit your company’s security team contact information so all the emails/phone calls come to you. After all, it is a nightmare to know about security vulnerabilities once the website is already compromised.

## Thanks

It was a broader community and cross-functional team effort at Magento to make this possible. I thank all the people who were very helpful in the entire process – providing positive and constructive feedbacks, improving module by suggesting and making changes to ensure best code quality, introducing unit tests, participants of the meetings with product owners and community engineering team to go through the features, devdocs and release notes article writers, QA and product release team. May be I missed some, I thank them as well. Special thanks to Troy Hunt, Ed Foudil, Oleksii Korsenko, Piotr Kaminski, Smita Verma and Eugene Shakhsuvarov.