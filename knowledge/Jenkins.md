
• Use Jenkins to perform Continuous Integration within your Software Development Lifecycle 
• Install Jenkins using a package manager or docker 
• Conﬁgure Jenkins “The DevOps way”, using Docker, Jobs DSL and Jenkinsﬁles 
• Use plugins to integrate Jenkins with popular development software 
• Conﬁgure the authentication and authorization options to tighten  security on your Jenkins UI

What is Jenkins

• Jenkins is an open source continuous integration (CI) and continuous delivery (CD) tool written in Java. 
• It’s an automation server used to build and deliver software projects 
• Jenkins was forked from another project called Hudson, after a dispute with Oracle 
• A major beneﬁt of using jenkins is that it has a lot of plugins available 
• There is easier to use CI software available, but Jenkins is open source, free and still very popular

What is CI / CD

• Continuous integration (CI) is the practice, in software engineering, of merging all developer working copies to a shared mainline several times a day. (Wikipedia) 
• Continuous delivery (CD) is a software engineering approach in which teams produce software in short cycles, ensuring that the software can be reliably released at any time.  
• In Practice: verify and publish work by triggering automated builds & tests 
• For every commit or at least once a day 
• All developers should push their changes to a version control, which should then be built and tested - which can be done by Jenkins 
• Jenkins doesn’t merge code nor it resolves code conﬂicts, that’s still for the developer to do (using for instance git and merge tools)


Beneﬁts

• Jenkins provides a feedback loop back to the developer to ﬁx build errors 
• Research has shown that it’s a lot quicker to have a developer ﬁx the error immediately (when the code is still fresh in memory) 
• Jenkins can publish every build of your software 
• This build already has gone through automated testing 
• When published and deployed to a dev/qa/staging server, you can advance the Software development lifecycle (SDLC) much quicker 
• The quicker you can go through an iteration of the SDLC the better


Jenkins Alternatives

• Self-hosted 
• Drone CI (Continuous delivery platform written in Go) 
• TeamCity (by Jetbrains) 
• Hosted (as a service) 
• Wercker 
• CircleCI 
• CodeShip 
• SemaphoreCI 
• Amazon AWS CI/CD tools

Installation methods

• On the Cloud using docker (works on AWS, DigitalOcean, Google Cloud, Azure) 
• www.virtualbox.org can run ubuntu in a VM locally 
• www.vagrantup.com together with virtualbox can spin up a running ubuntu instance in minutes (see my other DevOps course for an introduction to Vagrant) 
• Docker for windows can run docker on a windows PC (https://docs.docker.com/docker-for- windows/) 
• Docker for mac can run docker on a mac (https://docs.docker.com/docker-for-mac/) 
• Jenkins is written in java, so you can also run it without docker on any OS 
• Still I recommend docker for this course 
• Even when using linux and docker, you can still run jenkins slaves on Microsoft Windows to build applications that need a Microsoft Windows OS

What is docker?

• Docker is the most popular container software 
• Docker Engine
• The Docker runtime 
• Software to make run docker images 
• Docker Hub
• Online service to store and fetch docker images 
• Also allows you to build docker images online
• Isolation: you ship a binary with all the dependencies  
• No more “it works on my machine, but not in production” 
• Closer parity between dev, QA, and production environments 
• Docker makes development teams able to ship faster  
• You can run the same docker image, unchanged, on laptops, data center VMs, and Cloud providers. 
• Docker uses Linux Containers (a kernel feature) for operating system-level isolation

 

Containers on Cloud Providers
 

Why use docker to start Jenkins?

• Everyone will have the same container image of Jenkins 
• Regardless of your Operating System 
• You can run docker on an ubuntu on DigitalOcean, but also on a Mac, on Windows, etc 
• You can easily upgrade jenkins by pulling the latest container image 
• You can modify the jenkins container image by creating your own Dockerﬁle 
• Or modify the Dockerﬁle I have for jenkins in my github repository

Infrastructure as code and automation

• Jenkins allows you to use a web UI to input all the build parameters 
• This leads to: 
• No proper audit trail
• No easy history of changes
• Segregation between Jenkins admins and developers 
• Users (often developers) will have to contact a Jenkins administrator to make changes 
• Long lead times for changes 
• Difﬁcult to backup and restore (e.g. how to restore just one setting to how it was the day before)
• The solution is to completely write jobs as code and save it in version control 
• Version Control (git / subversion / mercurial) gives you a history and audit trail 
• Easy roll back to older versions of jobs and build instructions 
• Allows operations to give more control to the developers 
• Developers can bundle the jenkins build instructions with their own project repository (e.g. a Jenkinsﬁle in their project directory) 
• This is what a company that wants to embrace DevOps should do: allow developers to control their own builds



Job DSL and Jenkins Pipelines

• In the next sections, I’ll cover 2 Jenkins capabilities to enable Jenkins to be a true DevOps tool within your software organization: 
• Jenkins Job DSL
• Write code that creates and modiﬁes jenkins jobs automatically 
• Jenkins Pipeline (Jenkinsﬁle)
• Bundle the build parameters within the project 
• Allow developers to change jenkins build parameters 
• Enable audit trail, history, rollbacks using version control

Jenkins Job DSL

• The Jenkins Job DSL is a plugin that allows you to deﬁne jobs in a programmatic form with minimal effort 
• DSL stands for Domain Speciﬁc Language 
• You can describe jobs using a Groovy based language 
• Think about Groovy as a scripting language for the Java platform 
• It’s similar to java, but simpler, because it’s much more dynamic
• The Jenkins Job DSL plugin was designed to make it easier to manage jobs
• If you don’t have a lot of jobs, using the UI is the easiest way 
• When the jobs grow, maintaining becomes difﬁcult and a lot of work
• The Jenkins Plugin solves this problem, and you get a lot of extra beneﬁts: 
• Version control, history, audit log, easier job restore when something goes wrong

Jenkins Pipelines

• Jenkins Pipelines allow you to write the Jenkins build steps in code
• 1) Build steps allow you to write build (compile), test, deploy in code
• 2) Code means you can put this code in version control
 
Jenkins Pipelines vs Job DSL

• How are Jenkins Pipelines different than the Jenkins Job DSL?
• They both have the capability to write all your CI/CD in code 
• The difference is in implementation in Jenkins 
• Jenkins Job DSLs creates new jobs based on the code you write 
• The Jenkins Pipelines is a job type, you can create a Jenkins pipeline job that will handle the uild/test/deployment of one project
• Can I now start using pipelines and forget everything about Jenkins Job DSL? 
• You could use Jenkins Job DSLs to create new pipeline jobs 
• Until now we’ve only created freestyle projects with the Jenkins Job DSL 
• Another possibility would be to use an “Organization folder”, which is a feature of Jenkins Pipelines to detect the project repositories, removing the need to add new jobs 
• It’ll really depend on your needs for what option you’ll need to go

Jenkins Pipelines

• The pipeline is a speciﬁc job type that can be created using the Jenkins UI or the Jenkins Job DSLs 
• You can choose to write the pipeline in Jenkins DSL (declarative pipeline) or in groovy (scripted pipeline) 
• Groovy is a scripting language for the java platform, syntactically very similar to Java and it runs in the JVM (Java Virtual Machine) 
• Under the hood the Jenkins DSL is interpreted by groovy

Docker Pipeline plugin

• The docker pipeline plugin, let’s you spin up any container within your pipeline 
• I just used the same plugin in the previous demo, to build/push images 
• You can not only build new containers, but also run existing containers 
• This is useful for when you don’t want to bundle development tools with your production container, but you still want to run all stages in an isolated environment 
• You can build/test your application ﬁrst with an existing container with all the development tools 
• As a next step, you can build a new container, much tinier, with only the runtime environment

Docker Pipeline plugin

• Spinning up new docker containers lets you bring in any new tool, easily 
• You can specify exactly what dependencies you want, at any stage in the job 
• You can start a database during the test stage to run tests on 
• After the database tests have been concluded, the container can be removed, together with all the data 
• Next time you run a new database container during tests, you’ll have a brand new container again 
• This also works for multiple builds at the same time (think multiple git branches), every build has its own database container

Email integration

• The goal is to alert the developer of a broken build as soon as possible 
• The earlier you give a developer feedback of something that is wrong,the better 
• This increases the productivity of the developer team tremendously 
• The longer it takes for a developer to know he needs to ﬁx a bug,the more time it’ll take to resolve 
• The developer will able to ﬁx the code the quickest, when the code a developer wrote is still fresh in his memory
• Every time when a developer commits a change in version control, the build in jenkins should start 
• Changes from version control can either be pulled or pushed: 
• Pull: Jenkins polls the version control every x minutes 
• Push: The version control system (e.g. Github, Bitbucket) will send a notiﬁcation (push) to Jenkins (using http requests) 
• You can use the Github Plugin and Bitbucket to conﬁgure the push notiﬁcations

Slack Integration

• Slack is a chat and collaboration tool, comparable with Atlassian’s HipChat 
• It’s a new and popular team communication tool, that is much better than using Skype or older enterprise chat tools for collaboration 
• Slack (or hipchat) is better than its competitors, because it allows you to integrate all your tools within slack, to avoid switching between apps 
• ChatOps is a collaboration mode that connects people, tools,processes, and automation in a transparant workﬂow [1] 
• It allows you to do conversation driven collaboration, while having your tools integrated and keeping you up to date of the state of your systems
GitHub / Bitbucket Integration
• Up until now I’ve always added git repositories manually 
• If you have a lot of repositories, you don’t want to add every single repository manually 
• It is then more interesting to have Jenkins auto-detect new repositories 
• A developer could then create a new repository for a new (micro) service, add a Jenkinsﬁle, and the project will automatically be built in Jenkins
• The implementation differs from which version control provider you’re using 
• When using GitHub: the GitHub Branch Source plugin will scan all the branches and repositories in a GitHub organization and build them via Jenkins Pipelines 
• When using Bitbucket: the Bitbucket branch source plugin can scan team/project folders and automatically projects

JFrog Integration

• In the previous demos I’ve always submitted the Docker image to the docker registry (Docker Hub) 
• This resulting image is in Jenkins called “The artifact” 
• It’s the resulting binary from a build 
• It can be a docker image, or a .jar ﬁle, a .tgz/.zip ﬁle, really anything 
• These artifacts, the result of your build, you want to store somewhere 
• JFrog Artifactory is a product that can store for you the artifacts resulting from a build
• You can either download Artifactory for free and run it yourself, or you can use their hosted version 
• In the demo I’ll use the hosted version 
• It’s best practice to store all the artifacts of the builds that are getting deployed 
• If you need to roll back, you have the artifact already available 
• You are 100% sure about the binary if you’re promoting the same version from dev to staging or from staging to production 
• No lengthy rebuilds
• JFrog integration is done using a JFrog Plugin 
• The JFrog plugin allows you to add extra steps to your Jenkinsﬁle 
• One of the last steps of the build will be to send the artifact to JFrog 
• In this step, you can put a conditional, to only do this for develop/master branch, not for feature branches
• Sometimes you want to integrate an API, but there is no plugin available 
• Even if there is a plugin available, it can lack the features you want 
• You might want to get more information from an endpoint (e.g. the full JSON from the request) 
• You want to do a POST or PUT request on the API 
• One solution is to write your own Jenkins Plugin
• But this requires a lot of effort 
• And is not always feasible, as a developer, you might not have access to Jenkins Plugins
• Another solution is to use functionality in the Jenkins pipelines to do http requests
• You only need one plugin: the http request plugin 
• This plugin can do a generic HTTP request on any API 
• It’s up to you (the developer / SysOps / DevOps) to write the code to do the requests and interpret them 
• This is where groovy becomes handy, because groovy allows you to do scripting within the Jenkinsﬁle

Sonarqube

• Sonarqube continuously inspects your software project on code quality 
• It can report on: 
• Bugs (code issues) 
• Vulnerabilities (security issues) 
• Code smells (maintainability related issues) 
• Technical debt (estimated time required to ﬁx) 
• Code coverage (test coverage of code)
• Sonarqube is a very popular piece of software that is often integrated with Jenkins 
• In Jenkins it’s just a build step 
• the code needs to be scanned by the sonar-scanner 
• the sonar-scanner sends its results to the Sonarqube server 
• The sonarqube server needs to be installed 
• Sonarqube server also uses a database to maintain its state
• One possible solution: 
• Install database and sonarqube as a docker container on the master node 
• We can use docker-compose to manage the containers 
• Docker-compose is a handy tool from Docker that can spin up containers based on a container deﬁnition in yaml format 
• We’ll have 3 containers, a Jenkins container, a database container, and sonarqube

Jenkins Slaves

• Currently, only one node (one droplet) is hosting the jenkins web UI and doing all the builds 
• In production environments, you typically want to host the Jenkins web UI on a small master node, and have one or more worker nodes (Jenkins Slaves) 
• Using worker nodes, you can easily expand your build capacity 
• Typically one worker has one or more build executors (building slots) 
• If a Jenkins node has 2 executors, only 2 builds can run in parallel 
• Other builds will get queued
• Static or manual scaling: 
• You can have more workers during working hours (or no workers outside working hours) 
• You can add more workers ad-hoc, when necessary 
• During periods when a lot of code is created 
• During periods when developers have to wait long for for their builds to be ﬁnished 
• i.e. the jobs stay a long time in the queue
• Dynamic worker scaling 
• You have plugins that can scale Jenkins slaves for you 
• The Amazon EC2 Plugin: if your jenkins build cluster gets overloaded, the plugin will start new slave nodes automatically using the AWS EC2 API. If after some time the nodes are idle, they’ll automatically get killed 
• Docker plugin: This plugin uses a docker host to spin up a slave container, run a jenkins build in it, and tear it down 
• Amazon ECS Plugin: Same as docker plugin, but the host is now a docker  orchestrator, the EC2 Container Engine, which can host the docker containers and scale out when necessary 
• Builds can be executed on speciﬁc nodes 
• Nodes can be labeled 
• e.g. “windows64-node” 
• Builds can then be conﬁgured to only run on nodes with a speciﬁc label 
• This can be conﬁgured in the UI or using the Jenkinsﬁle
• Reduced cost: only have the capacity you really need 
• Slaves are easily replaceable: if a slave crashes, in can be spun up again 
• The master can run on a separate node that isn’t affected by the CPU/Memory load that builds generate 
• i.e. the UI will always be responsive 
• You can respond to sudden surges in builds, capacity can be added on the ﬂy 
• Even with manual scaling, you can quickly spin up a new machine as a Jenkins slave
• It’s important to standardize your Jenkins slaves 
• Don’t manually install tools on the slaves 
• Use Plugins to provide tools (NodeJS, Docker, Java, Maven) 
• Use Docker to provide images that can build jobs, and use the Docker pipeline plugin to execute builds in a speciﬁc docker image 
• A slave should be disposable, you should be able to throw it away and start it again from scratch
• There are 2 solutions I’ll demo: 
• Master node connects to slave over SSH 
• I’ll set up a new machine and let the master connect to the slave 
• Slave node connects to master over JNLP 
• The slave will initiate the contact 
• Good solution for windows slaves 
• Useful if the slave is behind a ﬁrewall

