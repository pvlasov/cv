# Pavel Vlasov Cover Letter

This document is complementary to my [CV](index.html). 
It is called a _cover letter_ because:

* One of the goals of the a cover letter is to communicate that you have something valuable to contribute.
* A cover letter is usually a companion artifact to a resume.

However, I don't have a resume, I have a CV, which is longer.
So this cover letter is not a "classic cover letter", it is more a white paper.
It contains descriptions of ideas which I've accumulated over the years observing how large software engineering organizations operate and challenges they face. 
As such, most of the ideas aim to improve internal working of such organizations. 
 
It is a long read and I hope you'll find something of interest for your org. 
Most likely some of the ideas wouldn't be applicable in your context.

Some of the ideas below can be categorized as explained below and some can be applicable to more than one area:

* Product/Service - how to build or improve an offering - something which the organization will benefit from.
* Procurement - how to find resources, e.g. people with right talents and some capacity to build/improve an offering or work on an idea.
* Delivery - how to get an offering to its consumers.
* Promotion - how to make potential consumers of offering existence and its potential value to them.

A brief note on terminology.

In this document the word _engineering_ means _“The action of working artfully to bring something about.”_.
For example, a more efficient organization, or a person ready for a their next role.

Also, the word _model_ in this document may mean the following:

* Something with a structure or explaining defining or explaining the structure of something else (meta-model).
* Partial representation of the underlying problem domain focusing on a particular aspect of it. A model is a map, not a territory. In this sense all models are wrong (by design), but some are useful.

This is not an academic paper and not a textbook, so you may have to use your judgment regarding the different aspects of the meaning of some terms.

* TOC
{:toc}

## MBSE

MBSE stands for [Model-Based Systems Engineering](https://en.wikipedia.org/wiki/Model-based_systems_engineering).
There are sophisticated MBSE tools such as [Capella](https://www.eclipse.org/capella/) for designing complex systems architecture. 

The approach to MBSE explained here can be described as:

* Pragmatic
* Democratic
* Elaborationist all the way to the runtime/end product

It came to be based on the following observations:

* When a group in an organization starts using a modeling tool while the rest of the organization doesn't use it then an [ivory tower](https://en.wikipedia.org/wiki/Ivory_tower) situation arises. Even if the underlying tooling is free there is a cost of learning.
* Developers even with the access to a graphical tool often edit the underlying resources such as XMI directly in a text editor. 

The approach is pragmatic because it is based on free open-source tooling and runtime and produces Maven jars which can be used in any Maven-based Java application, e.g. a micro-service.

It is democratic because it can be made a public good in an organization and doesn't require extensive training:

* If a person knows how right-click in the file explorer to create a new file they should be able to create meta-models.
* If a person knows how to create a bulleted list in MS Word or PowerPoint, they should be able to create/populated models.
* HTML documentation is generated from the models and published for everybody to see and understand - forming a "Ubiquitous language" of the organization.
* Model jars are published to to a Maven repository for Java developers to use them in their applications.

It is elaborationist because it supports model transformation pipelines - one model is transformed to another with adding details as needed until it gets transformed to a final consumable artifact, e.g. a static web site.

There is an aphorism "All models are wrong, but some are useful". If we define usefulness as positive ROI and short time to market, then with this approach to modeling it is easier to create a useful model because production and publication of a model requires less effort than alternative approaches, e.g. no need in an initial investment into a model editor.

![mbse](mbse.drawio.png] [^1]

[^1]: Created with [diagrams.net](https://www.diagrams.net/) desktop editor.


Pragmatic and democratic

Models cheaply 

...

directly edit unerlying XMI

Transformation pipelines - flow > action > resource > files (links - adm). Data provenance. page-template.xml

elaborationist vs translationalist approach

Translationalism vs elaborationism. Model - a partial description of reality on purpose. All models are wrong.

representation - a (partial) view into the model. E.g. diagram, properites table

## Code Generation

Solution instantiation. 

Generation model * configuration model => code

Parallel evolution and merging


## Delivery mechanisms

Cloud providers - API, CLI, IDE plug-ins

### Eclipse Ecosystem

### CLI


### Documentation as code

Both code generation and knowledge delivery mechanism

#### Maven sites

#### Application model

#### Journey model

#### Engineering model


## Organization engineering

Analogy with software system - kubernetes cluster. Disclaimer people/computers.

## Innovation pipeline

Engineering, aggregation. 
Innovation framework - tailored TOGAF?

Challenge/solution - generic, concrete.




Self-contained inner source