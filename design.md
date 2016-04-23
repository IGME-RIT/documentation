---
layout: page
title: Design Documentation
permalink: /design/
---

# The Atlas Project Design Document

---

1. [Abstract](#abstract)
2. [Mission Objective](#mission-objective) 
3. [Constraints](#constraints)
4. [Target Audience](#target-audience)
5. [Resources](#resources)
    1. [Backend](#backend)
    3. [Contribution](#contribution)

---

## Abstract
This document describes the design of the [The Atlas Project](https://github.com/IGME-RIT/igme-rit.github.io/). It outlines the goal of the project, the target audience, and the constraints, and in doing so allows us to design the best project within those limitations.

## Mission Objective
Games education is rapidly approaching a critical juncture. As development tools have become more widely available and publishing restrictions soften, the demand for substantial resources to learn game development has grown tremendously. Likewise, as games and the techniques involved in producing them grow in complexity, the amount of subject coverage professors can give to their students has shrunk proportionally. As an accredited university program with access to industry resources and expertise, the [Interactive Games and Media (IGM)](https://www.rit.edu/gccis/igm/) program at the [Rochester Institute of Technology (RIT)](http://www.rit.edu/) is in an excellent position to look towards the future of games education and act towards the benefit of game developers worldwide. The goal of this project is to __produce a freely-accessible, highly-scalable tutorial platform populated with projects that explore game development topics and illustrate connections with other projects, while opening a door to the open-source community to contribute even more content.__ 

## Constraints
1. __The product should be highly-scalable.__ The site should be capable of handling any number of projects. The back-end should be able to handle a large set of user and project records and rate limits should be kept in mind.

2. __The product should be comprehensive, but imperfect.__ Reimplementing the entire IGM curriculum is a major undertaking well-beyond the scope of the project. Making projects is an important part of content-production, but it is too big a task to create content for all facets of the IGM programs. As such, the means in which projects are loaded from GitHub by the back-end and from the back-end by the front-end should be highly-modularized.

3. __The product should be built in the same spirit as the project.__ The Atlas Project is designed to make games education accessible to a wider breadth of people. As such, the internals of Atlas should be well-documented and OSS licensed. They should be hosted on a public source hosting platform such as GitHub and should serve as a referenceable real-world example of its technologies.

## Target Audience
__IGM Students__ - The Atlas Project lessons should be created with the IGM curriculum in mind. Initial concepts, practices and categories of coverage should be selected around the core and advanced offerings of the IGM department. Atlas also should consider covering that which the IGM curriculum should cover, but does not. It should present material clearly and concisely, and should not require experience outside of the material and its prerequisite tutorials.

__Non-IGM Students__ - The Atlas Project should reinforce important concepts and practices to IGM students, but it should be primarily designed with the public in mind. Tutorials should be accessible to anyone with access to GitHub and should not use RIT/IGM-specific terminology or require RIT credentials or IGM-restricted code in order to view and run.

## Resources
The Atlas Project will provide access to a potentially enormous selection of tutorials, as well as a system for processing contributions. This section describes the resources we will provide.

### Backend

The backend will be hosted on Heroku and run as an Express app. The backend is intended to provide unfettered access to the tutorial data to the client. If the client depended directly on GitHub, it would be based on GitHub's uptime and rate-limits. The backend will provide an endpoint for retrieving all tutorials, a query-endpoint to retrieve tutorials by name, and an endpoint to sync the backend with GitHub data. The sync endpoint requires that whomever invokes it is authenticated and designated as an admin on the IGME-RIT organization on GitHub.

#### App Dependencies
1. Node.js 4.x
2. [Express](https://www.npmjs.com/package/express)
3. [Lodash](https://www.npmjs.com/package/lodash)
4. [Mongoose](https://www.npmjs.com/package/mongoose)
5. [Octokat.js](https://www.npmjs.com/package/octokat)
6. [Passport](https://www.npmjs.com/package/passport)
7. [Q](https://www.npmjs.com/package/q)
8. [yaml.js](https://www.npmjs.com/package/yamljs)

#### Heroku Dependencies
1. [Hobby tier or higher](https://www.heroku.com/pricing) for maximum functionality
2. [MongoLab](https://elements.heroku.com/addons/mongolab) integration

### Contribution

The flow of contribution for new tutorials to Atlas will be as follows:

1. A feature request is made to the [contribute](https://github.com/igme-rit/contribute/issues) repository requesting a tutorial type.
2. The discussion will be used for maintainers and whomever would like to contribute a tutorial to guide its design.
3. A tutorial will be added to the [contribute](https://github.com/igme-rit/contribute/pulls) repository as a pull request to the root directory for triaging.
4. An active maintainer will inspect the tutorial and either approve it, provide feedback, or reject the submission.
5. An active maintainer will create an igme_config.yml in the root of the tutorial's folder for use with the Atlas front-end. 
6. An active maintainer will break off the tutorial into its own repository under the IGME-RIT organization and remove the tutorial from the [contribute](https://github.com/igme-rit/contribute) repository.

_Sample igme\_config.yml_

```yaml
title: Skybox
author:
  name: IGME-RIT
  email:
  github: igme-rit
description: This example demonstrates rendering a skybox.
language: C++
image:
  icon: https://cloud.githubusercontent.com/assets/10502938/13506660/28be0300-e14d-11e5-90e3-b194f14e52bd.PNG
  banner: https://cloud.githubusercontent.com/assets/10502938/13506660/28be0300-e14d-11e5-90e3-b194f14e52bd.PNG
tags:
  - C++
  - Graphics
extra_resources: # Links to additional or extra resources
  - 
connections: # Repository names of each parent connection
  - "normal-mapping-tutorial"
```
