---
id: 1203
title: '#MagentoImagine2019 Dev Exchange Recap – Make Magento more secure'
date: '2019-06-09T06:09:10+00:00'
author: kalpesh
layout: post
tags:
    - Magento
    - 'Magento Imagine'
    - Security
tags:
    - 'devexchange 2019'
    - 'magento imagine 2019'
    - 'magento security'
---

<div class="wp-caption aligncenter" id="attachment_1212" style="width: 610px">![Magento Imagine 2019 Dev Exchange](http://ka.lpe.sh/wp-content/uploads/2019/06/magento_imagine_2019_dev_exchange-1024x616.jpg)Magento Imagine 2019 Dev Exchange

</div>This year Magento Imagine conference was amazing, around 3,500 people from around the world attended the event which was held at Wynn, Las Vegas. I met many people whom I already knew, and many more whom I never met before in real life but interacted on social media and forums.

I hosted a table at Dev Exchange around [Magento security](https://community.magento.com/t5/Magento-Imagine-DevExchange-2019/Make-Magento-more-secure/idi-p/127723), which was co-hosted by [Pablo Benitez](https://twitter.com/centerax) from eBizmarts. [Piotr Kaminski](https://twitter.com/piotrekkaminski) and [Steven Zurek](https://twitter.com/StevenZurek) participated from Magento/Adobe’s side. [Talesh Seeparsan](https://twitter.com/_Talesh) took all the notes and contributed to the discussion during the talk. Other people that joined the table from Magento and community were [Igor Miniailo](https://twitter.com/iminyaylo), [Igor Gorin](https://twitter.com/theigorgorin), [Georgiy Slobodenyuk](https://twitter.com/youanden), [Lee Saferite](https://twitter.com/LeeSaferite), [Manish Mittal](https://twitter.com/mittalmanishm), [Jeanne](https://twitter.com/JeanneMage), Scott N and Shilpa M. Everyone participated in the discussion and gave their valuable feedback on the topics we discussed, overall it was very productive.

There were 4 main topics we discussed at the table:


### 1. Extension developers write secure code

*With the proactive and nimble approach Magento has taken to core security, many time agencies and merchants find external 3rd party extension makers have not put in as much effort. How can we encourage their developers to take a more secure coding approach? Can Magento community maintain secure coding practices document like [technical guidelines, security](https://devdocs.magento.com/guides/v2.3/coding-standards/technical-guidelines.html#15-security)? Validate code using a tool like PHP CodeSniffer? What solutions already exist that we can rely on? What processes already exist that we can implement?*

**Static Scanners / RIPS:**

Third party code checking and code scanning is a complex process. [RIPS](http://rips-scanner.sourceforge.net/) work for some paths, they are also working on improving the support. We can add Regular Expressions to the old open source versions as well. However, we have to do lot of work to deal with the false positives because they don’t directly support Magento.

**Dynamic Scanners:**

Probably Dynamic Scanning is the better idea. Example, using [OWASP Zap](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) to test input fields of extensions. There are current efforts to get an easy to set up OWASP Zap fuzzer for Magento Extension makers.

There is a danger of reporting error in extensions without understanding the value of the error or making it easy to act on the error. Example, using tools that just dump a PDF of all the errors versus categorizing and ranking problems and putting them into bug tracker. We should have documentation of recommended fixes for the types of errors dynamic scanning provides.

**Vulnerabilities in extensions:**

A lot of extension providers are not prepared for a vulnerability in their extension. There are a few common problems with their approach. The problems we find with them, they are:

- Not fixing vulnerabilities and ignoring input from developer community, or
- Fixing vulnerabilities silently and not notifying their customers, or
- No way of notifying their customers of a new version with a fix.

There should be a process for responding to security vulnerabilities if extension makers want their extensions to be on the Marketplace. There should be consequences instead of enforcement when dealing with extension makers with vulnerabilities.

**Marketplace vs non-marketplace extensions:**

Unfortunately, most of the problems that we see are in extensions that are not from Marketplace, therefore enforcement of security policies may have the unintended consequence of reducing the number of extensions on the Magento Marketplace. One possible solution to extensions not on marketplace is that there may be a warning in Magento if it is code matched to an extension that is on the marketplace. This works for vendors that sell the same extension on Marketplace and on their own site.

One of the driving reasons for buying extensions from outside the marketplace is because updates from the Marketplace are too slow. The process is improving though.

It would be good if the marketplace extensions page would show the version that is on the Marketplace and show which past versions may be vulnerable.

**Known extension vulnerabilities database:**

Currently there is a community effort to track down vulnerabilities in Magento extensions (from the marketplace or not), you can find that open source list here: <https://github.com/gwillem/magevulndb>

Pre and post hooks in Github to track if an existing extension has a known vulnerability will not work but running from the admin that reaches to the centralized repo like magevulndb may work. There is a n98-magerun extension that will check your existing extensions against the list on magevulndb.

Hashes of the files can tie into the vulnerability database, but it may become resource heavy for all files. Hash of the system vs last known good version of itself is an alternative.

**Note to extension makers:**

While more secure development is important, it is extremely critical to take security more seriously in your support processes. We have a problem with unused admin users on stores with known username/passwords that were assigned to an extension maker for support purposes. There are ways around this, example, temporary admin accounts or not the same password for each support incidence by extension maker.

There is also a problem where extension developers put restrictions on the PHP versions of their extensions such that it cannot be upgraded. It would be good if you can configure SemVer support properly.

**Prevent use of easy and known passwords in admin:**

Wagento has the [Have I Been Pwned](https://blog.wagento.com/have-i-been-pwned) extension and there are possible other versions. It would be good if the HIBP extensions worked on the admin accounts too. Admin account needs more protection, so it makes more sense to implement this in admin login form as well.

**Making it easy for merchants:**

There is a lack of will on the part of merchants, so it is important that we make the tools we build as easy as possible for them to use/integrate. Yarn and NPM gives the developer a list of vulnerabilities but we don’t have that in Composer for PHP. [Roave](https://github.com/Roave/SecurityAdvisories) and [Sensio labs](https://github.com/sensiolabs/security-checker) have checkers for this sort of stuff.

**How System Integrators can help:**

One option to tackle extension updates is tackle it from the SI point of view. It would be great if sales people can commit to % of budget for security and structuring contracts with merchants so that budget is included by default. It frees SI to do what needs to be done so merchants don’t get the sticker shock of maintenance that they didn’t expect. If there are no urgent security updates, then the merchant gets that time as extra development/features.

There has been a lot of talk when it comes to security being expensive for SIs but there are not a lot of conflicts because of security hotfixes.


### 2. Better ways to report vulnerabilities on a merchant’s site

*Magento has a bug bounty program to report vulnerabilities in their code and websites. If a user or security researcher finds vulnerabilities in some Magento powered web store, not owned by Magento – an Adobe company, how can they reach out to the right person on the merchant’s team? How to pass the information given the sensitive nature of the issue? Should Magento accept [security.txt standard](https://securitytxt.org/)?*

**Security.txt extension:**

There is an open source extension for Magento to display contact information as per security.txt standard: <https://github.com/kalpmehta/securitytxt>

SI contact information should be on the security.txt since they are most likely responsible.

The nice thing is that Magento has good contact information for Commerce (Enterprise Edition) customers, this includes Version, URL, etc. which is passed to Magento during news check. Yet still you have to give Magento your email for access to the repo, so they do have access to many customers but attribution to stores are not always the easiest.

If merchants are not responding to contact when they’re hacked, the funny thing to do would be to call them out on twitter (never do that :D)


### 3. Code review in community-submitted Pull Requests

*Is Magento doing security code review when someone submits a PR to core code? What to check for when doing code reviews to identify security risks?*

**Escape HTML/JS before rendering:**

Currently, all the escapings in Magento are explicit, that means a Magento developer needs to escape output manually wherever needed, say with $block->escapeHtml() function calls in templates. By default, all the output through the echo language construct is not escaped. Potentially it could lead to unintended XSS vulnerabilities. The idea is to make the opposite default behavior so that all the default output should be escaped, say with escapeHtml function, while only exceptions (which no need to be escaped should be explicitly specified in code). The current task complicated with the fact that echo is not a function, but a language construct, thus it cannot be redefined.

**Considering backward compatibility:**

We need to take the backward compatibility requirements into account and prevent double escaping. Potentially a solution could be compiling the PHTML, this is heavyweight and complicated. Is there an easier way or faster way?

More info on template security here – <https://devdocs.magento.com/guides/v2.3/frontend-dev-guide/templates/template-security.html>

Discussed this topic in weekly Magento architecture call as well:

<https://github.com/magento/architecture/issues/165>

**Sanitize input before saving in DB:**

There are many places in the admin where you do not expect HTML code. Example, when saving Boolean values like yes/no, integer and decimal values for qty and pricing, most of the store configuration values, etc. Magento can restrict these all to disallow any HTML tags before saving to database. This can reduce the number of potential XSS when these values get rendered on the store front and admin.


### 4. Add Security topics in Developer certifications

*Magento U have been including more topics on security in the exams. Should there be more or of different levels or separate exams? There are more security questions on the Developer plus exam but not the others.*

**Include Security questions in existing certifications Vs. create new security certification?**

Magento has just started exploration of the training for security. They are optimizing for their plans of first training and maybe later certification. A separate certification.

Magento has gotten feedback that since security is such a broad topic the SI’s would like to see the certificate split up in the multiple levels. OWASP Top Ten at the lower levels to Forensics and more complex topics on the higher levels. There is an overwhelming yes to this plan.

**Lifetime validity of the certification Vs. certifications with expiry date:**

Certifications should have an expiration date since these sorts of skills evolve rapidly.

**Magento Security study material:**

Ideally, there shouldn’t be a monetary barrier to the study material related to Magento security. Probably the Magento Dev Docs is a good place for this.

Magento makes regular 5-minute training videos. These could also include the initial security topics, example, OWASP Top Ten.

By a large margin the most requested type of documentation are greenfield build security checklists. Probably Dev Docs is best place for a collaborative checklist.

Pablo brought some Ext DN pamphlets on Do’s and Don’ts. Also tips on secure Magento 2 development was very good. Here are those pamphlets that Piotr Kaminski shared on Twitter.

> Great resource from ⁦[@ext_dn](https://twitter.com/ext_dn?ref_src=twsrc%5Etfw)⁩ for Magento security [pic.twitter.com/lZLhDbK4pC](https://t.co/lZLhDbK4pC)
> 
> — Piotr Kaminski (@piotrekkaminski) [May 15, 2019](https://twitter.com/piotrekkaminski/status/1128794100243689472?ref_src=twsrc%5Etfw)

<script async="" charset="utf-8" src="https://platform.twitter.com/widgets.js"></script>

> More ⁦[@ext_dn](https://twitter.com/ext_dn?ref_src=twsrc%5Etfw)⁩ goodies. A must read for all Magento developers not only extension vendors. [pic.twitter.com/88roP0naxk](https://t.co/88roP0naxk)
> 
> — Piotr Kaminski (@piotrekkaminski) [May 15, 2019](https://twitter.com/piotrekkaminski/status/1128810027148431360?ref_src=twsrc%5Etfw)

<script async="" charset="utf-8" src="https://platform.twitter.com/widgets.js"></script>

—

With this we were out of time as Dev Exchange only provided 45 mins of time slot for every topic discussion. However, I believe it was good enough time to get the feedback and ideas from everyone participated. We actually started few minutes earlier though, I feel sorry for Lee as he had to introduce himself 3 times because of official announcement to start all the talks and all the background noise interrupting him J

If you have any ideas around Magento security, please post it in a comment!