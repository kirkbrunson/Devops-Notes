Notes on Udacity's [Intro to DevOps](https://www.udacity.com/course/intro-to-devops--ud611) course.


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
See [project setup](setup.md).








### Read Further:
- [][]


[1]: https://www.chef.io/blog/2010/07/16/what-devops-means-to-me/
[2]: https://theagileadmin.com/what-is-devops/
[3]: https://www.atlassian.com/agile/release
[4]: https://www.chef.io/solutions/devops/
[5]: https://www.youtube.com/watch?v=o7-IuYS0iSE
[6]: http://brainfreez3.blogspot.com/2015/12/devops.html

