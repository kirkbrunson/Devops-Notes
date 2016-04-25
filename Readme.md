Notes on Udacity's [Intro to DevOps](https://www.udacity.com/course/intro-to-devops--ud611) course. See the [course wiki][17] for more.


# Purpose of DevOps:
- Integrates Agile and Lean principles in the operations life cycle


## Definition:

> DevOps is the practice of operations and development participating together in the entire service life cycle, from design and development to production support.

> A cultural and professional movement, focused on how we build and operate high velocity  organizations, born from the experiences of its practitioners.


## Problem statement:

Agile development has lead to greater development team productivity and product success. However, teams within the organization can still be siloed, and having an optimal silo doesn't guarantee optimal flow for the entire organization:
![Siloed teams](/img/silo.png)

To fix this DevOps integrates agile and lean principles to break the barrier between teams. This builds a better product idea to customer value flow.
![Integrated Flow](/img/flow.png)


## Concepts:

**CAMS: Devops is About CAMS**

- **Culture:** People over Process over Tools. People and process first.  If you don’t have culture, all automation attempts will be fruitless. 
- **Automation:** DevOps integrates development side automation and operations side automation, bringing these together in deploying automation.
- **Measurement:** You can't improve what you can't measure. DevOps monitors metrics as much as possible. Metrics relevant to operations, development, business operation, etc. 
- **Sharing:** Comprehensive stake holders create the loop back in the CAMS cycle. Shared input leads to shared responsibility and ownership.

Read the post [*What Devops Means to Me*][1] for more in depth discussion on CAMS. Additionally, read Atlassian's [Three ingredients for great software releases][3] for a concise overview of software releases.


## TL;DR:

Great software development involves the entire team from product management to operations. All your lean planning and iterative development won't mean a thing if you can't ship quickly. DevOps lives in this space.
![Devops Venn Diagram](/img/devops_venn.png)


### Read Further:
- [What is DevOps][2]
- [Agile Software Releases][3]
- [Chef DevOps][4]
- [The (Short) History of DevOps][5]
- [Introducing DevOps][6]



---



# The DevOps Environment:

## Problem statement:

Differences between development and production environments can be a source of tension between teams. We will use Packer to build deployment images for both dev and production environments.


## Solutions:

**Golden image:** Master image of machine contains all dependencies and can be reused without configuration.

- Fast boot & install
- Large upfront cost
- Immutable image
![Golden Image](/img/golden_image.png)


**Configuration Management:** Manages dependency installation on machines that have a common OS image. 

- Lighter build process
- Easy to update
- Slower startup
![Config Management](/img/config_manage.png)


Can also use a hybrid of the two approaches.


## Setup and tools:

See [project setup](setup.md) and install the software as described.

## Packer:

Per Packer's Getting Started: 
> Packer is an open source tool for creating identical machine images for multiple platforms from a single source configuration.

Next up, read the [Intro to Packer][7], [Packer Terminology][8], and the [template overview][9].

![Packer Overview](/img/packer_overview.png)

Now you should have a good understanding of what Packer is and what you can use it to accomplish. Read the following docs to continue:
- [Builders][10]
- [Provisioners][11]
- [Post-Processors][12]


At this point, you should make sure you've cloned the [course repo][13] as explained in setup. Follow the steps in that repo's readme to build your first packer box. 





---


# The Development Environment:


## Common Environments:

- **Local:** A developer's workstation.
- **Sandbox:** A dev server for the dev to work on their branch.
- **Integration:** Often a CI server where changes are tested and merged to the main branch.
- **Staging:** A mirror of production and has fairly recent data. 
- **Production:** The environment finally deployed to.

## Workflow: Development to Production:

Workflow uses VCS to sync changes (often using a [branching strategy][14]). Here's the idea:

![Basic Workflow](/img/basic_workflow.png)

![Branching Model](/img/branching_model.jpg)
Taken from [Frederic Dewinne's The Continuous Talk](http://www.slideshare.net/continuousphp/the-continuous-talk).



## CI: Continuous Integration:

###  Overview:
CI integrates changes into existing code bases by watches a branch for changes. When changes are committed, the CI server spawns a build process, and then runs tests on the build artifacts. Read [this post][15] for more.

[Jenkins][16] is the CI tool that we'll use for this course. If you've launched your cloud provider account and built a packer box in lesson 2, you're good to go. If not, follow [these instructions][17] to do this now.

Run:
```
packer build -only=<cloud service target> control-server.json
``` 

Navigate to your instance's `IP/jenkins` url. Eg: `123.456.78.9/jenkins` and login with `vagrant`, `vagrant` as credentials. Explore your dashboard or the [one here][18] to familiarize yourself with the layout. Then read the getting started to become familiar with [Jenkins Pipelines][19]. Additionally, you'll want to have a look at the console's [build pipeline](https://wiki.jenkins-ci.org/display/JENKINS/Build+Pipeline+Plugin). 

Boxes represent steps to run and their color represent's their status. Green == Passing, Yellow == Running, Blue == Queued, Red == Failed. Note that you can change these under "Configure":
![Jenkins Build Pipeline](/img/build_pipeline.png)


## Testing:

### Overview:

Testing helps identify bugs and ensure the quality of our code.

### Types:

- **Unit Tests:** Written alongside code to test behavior of individual functions or classes.
- **Regression Tests:** Written for debugging to verify that a bug is fixed and not reintroduced.
- **Smoke Tests:** Preliminary test to make sure the system works before testing further.
- **System Integration Tests:** Tests whole system including dependencies (apis, databases, etc).
- **Acceptance Tests:** Verifies the system implements the user facing features as planned.
- **Manual QA Tests:** Approval process to continue deployment.

For more, see Udacity's [Software Testing: How to Make Software Fail][20].

[Bug tracking][21] is also important. Having a unified place to identify, track, and collaborate on bugs makes resolving them faster. Read this article on [why to use a issue tracking system][22].

Now we have automated from deployment process from the developer's local machine to a staging area by building environments and testing them as discussed above. At this point, our code should be in a staging environment. The last step between Continuous Integration and [Continuous Deployment][23] is a manual trigger.



## Monitoring:

### Overview:
Good monitoring is a critical feedback loop for the organization, and should be widely accessible for different organizational units . For marketing and sales, this can provide KPIs such as traffic, growth, pageviews, etc. For development, monitoring can identify bugs. For Ops, it can provide facts about your infrastructure utilization such as CPU usage, response codes, or network bandwidth.

### Data Sources:
- **External Probing:** External interaction with system, recording the results. Eg: test queries.
- **Application stats:** Queries per second, latency, etc
- **Environment stats:** Memory profiling, etc
- **Host stats:** Load avg, disk errors, etc
- **Logs** 

### Data Products:
- Alerts
- Performance analysis
- Capacity prediction
- Growth measurement
- Debugging metrics


### Monitoring Tools:

Picking which to use depends on your needs. For small projects, something small and easy to set up is better than a comprehensive suite meant to manage hundreds or thousands of nodes and services. One the other hand, if you have a huge system, you should pick a system that is meant to be very scalable. 

Here's a few common tools:

- [Nagios][24] and [Zabbix][25] - comprehensive solutions for monitoring large infrastructure, but maybe too big and complex for small projects.
- [Graphite][26]: Opensource database and a graphing solution for storing and displaying monitoring data.
- [InfluxDB][27]: an open-source distributed time series database for metrics, events, and analytics.
- [StatsD][28]: Simple daemon for easy stats aggregation, by Etsy. Read about the philosophy behind it in the article by it's creators - [Measure Anything, Measure Everything][29]
- [Grafana][30]: metrics dashboard and graph editor for Graphite and InfluxDB
- [PagerDuty][31]: incident resolution lifecycle management platform that integrates with over 100 other systems to streamline the process for large organisations.
- [Logstash][32]: log storage and search system, works well with - [Kibana][33] graphing and visualization software.


![Monitoring Overview](/img/monitoring_overview.png)



---

Congrats! You've reached the end Intro to DevOps. Be sure to continue learning by checking out the resources in the [course wiki][17].




[1]: https://www.chef.io/blog/2010/07/16/what-devops-means-to-me/
[2]: https://theagileadmin.com/what-is-devops/
[3]: https://www.atlassian.com/agile/release
[4]: https://www.chef.io/solutions/devops/
[5]: https://www.youtube.com/watch?v=o7-IuYS0iSE
[6]: http://brainfreez3.blogspot.com/2015/12/devops.html


[7]: https://www.packer.io/intro/index.html
[8]: https://www.packer.io/docs/basics/terminology.html
[9]: https://www.packer.io/docs/templates/introduction.html
[10]: https://www.packer.io/docs/templates/builders.html
[11]: https://www.packer.io/docs/templates/provisioners.html
[12]: https://www.packer.io/docs/templates/post-processors.html

[13]: https://github.com/udacity/devops-intro-project
[14]: https://www.atlassian.com/continuous-delivery/continuous-delivery-workflows-with-feature-branching-and-gitflow
[15]: https://www.atlassian.com/agile/continuous-integration
[16]: https://jenkins.io/
[17]: https://www.udacity.com/wiki/ud611
[18]: https://ci.jenkins.io/
[19]: https://jenkins.io/doc/pipeline/
[20]: https://www.udacity.com/course/software-testing--cs258
[21]: https://en.wikipedia.org/wiki/Bug_tracking_system
[22]: https://sifterapp.com/academy/overview/why/
[23]: http://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley-ebook/dp/B003YMNVC0


[24]: https://www.nagios.org/
[25]: http://www.zabbix.com/
[26]: http://graphite.wikidot.com/
[27]: https://influxdb.com/
[28]: https://github.com/etsy/statsd
[29]: https://codeascraft.com/2011/02/15/measure-anything-measure-everything/
[30]: http://grafana.org/
[31]: https://www.pagerduty.com/
[32]: https://www.elastic.co/products/logstash
[33]: https://www.elastic.co/products/kibana
