---
isChild: true
anchor: building_and_deploying_your_application
---

## 建立及部署應用程式 {#building_and_deploying_your_application_title}

如果你發現自己在（手動）上傳檔案前，需要手動處理資料庫 schema 改變，或是手動執行測試，先想一想！在更新版本時，每個額外的人工部署任務都會增加嚴重錯誤的可能性。當你進行簡單的更新時，或是建構網站，或是持續整合（ continuous integration ）策略， [自動化部署](http://en.wikipedia.org/wiki/Build_automation) 會是你的好朋友。

你可能會想要自動化的任務有：

* 相依性管理
* 編譯，最小化 assets
* 執行測試
* 建立文件
* 打包 
* 部署 


### Build Automation Tools

Build tools can be described as a collection of scripts that handle common tasks of software deployment. The build 
tool is not a part of your software, it acts on your software from 'outside'.

There are many open source tools available to help you with build automation, some are written in PHP others aren't. 
This shouldn't hold you back from using them, if they're better suited for the specific job. Here are a few examples:

[Phing](http://www.phing.info/) is the easiest way to get started with automated deployment in the PHP world. With 
Phing you can control your packaging, deployment or testing process from within a simple XML build file. Phing (which 
is based on [Apache Ant](http://ant.apache.org/)) provides a rich set of tasks usually needed to install or update a 
web app and can be extended with additional custom tasks, written in PHP.

[Capistrano](https://github.com/capistrano/capistrano/wiki) is a system for *intermediate-to-advanced programmers* to 
execute commands in a structured, repeatable way on one or more remote machines. It is pre-configured for deploying 
Ruby on Rails applications, however people are **successfully deploying PHP systems** with it. Successful use of 
Capistrano depends on a working knowledge of Ruby and Rake.

Dave Gardner's blog post [PHP Deployment with Capistrano](http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/) 
is a good starting point for PHP developers interested in Capistrano.

[Chef](http://www.opscode.com/chef/) is more than a deployment framework, it is a very powerful Ruby based system 
integration framework that doesn't just deploy your app but can build your whole server environment or virtual boxes.

Chef resources for PHP developers:

* [Three part blog series about deploying a LAMP application with Chef, Vagrant, and EC2](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [Chef Cookbook which installs and configures PHP 5.3 and the PEAR package management system](https://github.com/opscode-cookbooks/php)
* [Chef video tutorial series by Opscode, the makers of chef](https://www.youtube.com/playlist?list=PLrmstJpucjzWKt1eWLv88ZFY4R1jW8amR)
Further reading:

* [Automate your project with Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)

### Continuous Integration

> Continuous Integration is a software development practice where members of a team integrate their work frequently, 
> usually each person integrates at least daily — leading to multiple integrations per day. Many teams find that this 
> approach leads to significantly reduced integration problems and allows a team to develop cohesive software more 
> rapidly.

*-- Martin Fowler*

There are different ways to implement continuous integration for PHP. Recently [Travis CI](https://travis-ci.org/) has 
done a great job of making continuous integration a reality even for small projects. Travis CI is a hosted continuous 
integration service for the open source community. It is integrated with GitHub and offers first class support for many 
languages including PHP.

Further reading:

* [Continuous Integration with Jenkins](http://jenkins-ci.org/)
* [Continuous Integration with PHPCI](http://www.phptesting.org/)
* [Continuous Integration with Teamcity](http://www.jetbrains.com/teamcity/)
