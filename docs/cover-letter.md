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

It is elaborationist because it supports model transformation pipelines - one model is transformed to another with adding details as needed until it gets transformed to a final consumable artifact, e.g. a static web site or generated code.

There is an aphorism "All models are wrong, but some are useful". If we define usefulness as positive ROI and short time to market, then with this approach to modeling it is easier to create a useful model because production and publication of a model requires less effort than alternative approaches, e.g. no need in an initial investment into a model editor.

The value proposition of this approach:

* Low code (modeling and generation) and low tech (ability to load from YAML and other resources which do not require specialized editors) result in low cost.
* Meta-model provides common "ubiquitous" language.
* Model documentation makes this language widely available.
* Visualizations of the model structure make it easier to grasp the model. Package diagrams provide the "big picture".
* Class context and inheritance diagrams provide a focused view of a particular class and the classes it collaborates with.
* Documentation is linked to model elements which provides fine-grained structure and makes it easier to capture and find details.
* Documentation may contain diagrams defined in text. E.g. documentation for a class may contain a component diagram, for an attribute a state diagram, and for an operation a sequence diagram.
* Loading from different resources provides an abstraction layer allowing developers focus on business rather than integration logic.
* Structured data captured in a "low-tech" way - as text. No need in hosting databases. Data can be produced by both humans and systems. Capabilities of modern computers can easily handle models with millions of elements - it might not be enough to process runtime data such as log entries, but is more than enough to model organizations, software systems, cloud deployments, etc. Runtime data can be pulled in an aggregated form.

The below diagram shows the elements of the approach: 

![mbse](mbse.drawio.png) [^1]

[^1]: Created with [diagrams.net](https://www.diagrams.net/) desktop editor.

### Domain model

Developers capture the problem domain knowledge in Ecore models as classes with attributes, references and operations.
Classes and other classifiers - Enums and Data types are organized into packages.
Models can cross-reference each other - one model can use or extend classes from another model.

Documentation is generated from the models with [Nasdanika HTML Ecore](https://docs.nasdanika.org/modules/html/modules/ecore/index.html) and published to a web/intranet sites.
A documentation site may contain documentation generated from multiple models. 
[Documentation example](https://docs.nasdanika.org/modules/core/modules/flow/index.html).

The model may contain validation and business logic. 

Java code is generated from the models and can be packaged and deployed as a Maven jar. [Example](https://mvnrepository.com/artifact/org.nasdanika.core/flow).

### Loading logic and Integrations

Ecore supports loading and saving from/to XMI files out of the box. 
With [CDO](https://www.eclipse.org/cdo/) is is possible to store models in a number of databases.

[Nasdanika EMF](https://docs.nasdanika.org/modules/core/modules/emf/index.html) provides ability to load models from any key-value source - YAML, JSON, ... 
If the source is YAML the loading logic may inject source markers into model elements - file, line, and column. 
And if the YAML is in a Git repository then a Git marker can be injected adding information about remotes and commit id allowing to trace the origin of a model element.
This may be important in scenarios where models are loaded from multiple resources or when there are multiple model transformations - the transformation logic may either copy the elements as-is along with their markers, or it may copy and retain the markers for traceability/auditability.

Developers may implement custom resources and resource factories to load model elements. 
E.g. an Excel file with a specifc structure can be loaded using a custom resource leveraging [Apache POI](https://poi.apache.org/). 
An issue object might be loaded from an issue tracking system using Java or REST API,
or an aggregated metrics object may be loaded from a monitoring system.

Loaded models may be used in Java applications to serve both as a model and anti-corruption level abstracting higher levels from storage implementation details.

### Resources

Models are loaded from local or remote resources identified by a URI, not necessarily a URL. 
It is possible to specify which resource factory to use for a particular URI, one way is extension matching.
As such a resource set - which you can think of as a single logical model - may be loaded from multiple different resources. 
Some of these resources may be human-crafted, some may be backed by automated systems. 

### Representations

A representation is a view of a model.
There might be different representations intended for different uses by different modelers.
In an organization a single "logical" models may leverage multiple representations and editing approaches for 
different parts of it. 
For example:

* Some modelers can input data in YAML/JSON format following load specification part of the published meta-model documentation.
* Some others may enter data into Excel spreadsheets in a shared location, e.g. OneDrive, not even being aware that they are "modelers".
* Some groups may used specialized representations/editors.  

This section outlines some of representation options.

#### HTML

Models can be used to generate HTML sites.
Dynamic behavior can be achieved in two ways:

* Single-page applications embedded into static content. Examples:
    * [All Issues](https://docs.nasdanika.org/all-issues.html) page with configurable columns and filtering.
    * [Site Search](https://docs.nasdanika.org/search.html)
    
[Nasdanika HTML EMF](https://docs.nasdanika.org/modules/html/modules/emf/index.html) provides base classes for creating site generators. 

HTML sites are read-only representations and as such they may also be considered to be transformation/generation targets explained below.

One flavor of HTML output is Eclipse Help - a "site" which can be "mounted" into the Eclipse Help System.

#### Eclipse tooling

##### Tree editors

Generation of a tree editor is a built-in functionality of [Ecore Tools](https://www.eclipse.org/ecoretools/). 
However, you'd need to deliver the editor to your modelers, which may be a challenge - see the [Eclipse ecosystem](#eclipse-ecosystem) section. 
E.g. not all of your modelers may know how to use Eclipse or have an ability to install it in their environment.

##### Diagram editors

Diagrams editors can be created with [Eclipse Sirius](https://www.eclipse.org/sirius/). 
While being a very powerful modeling technique, diagram editors require considerable investment. 
With Sirius, which makes creation of diagram editors very easy, the investment is not so much into building an editor, but more into training and adoption.

##### Form editors

Form editors can be created using [JFace Data Binding for EMF](https://www.vogella.com/tutorials/EclipseDataBindingEMF/article.html). 

##### Text editors

Text editors with syntax validation, highlighting, and auto-completion can be created with [Xtext](https://www.eclipse.org/Xtext/).

#### In-browser editors

Models can also be edited in a web browser using:

* [Sirius Web](https://www.eclipse.org/sirius/sirius-web.html)
* Form editors and other Eclipse UI using [Eclipse RAP](https://www.eclipse.org/rap/)

### Transformation/Generation Targets

Oftentimes in order to become useful a model needs to be transformed to another model or to some other format.
The target format is sometimes called a "Generation target" and the act of transformation is called "generation".

This section provides several examples of transformations and generations targets.

The first example is Nasdanika.org site which is generated from several models:

* Ecore models are transformed to [application models](https://docs.nasdanika.org/modules/html/modules/models/modules/app/index.html) by HTML Ecore. Diagram are generated from the models.
* Some of [Engineering model](https://docs.nasdanika.org/modules/engineering/modules/model/index.html) elements use the above generated models as "action prototypes". The engineering model is loaded from multiple YAML, Markdown, and drawio files stored in multiple Git repositories. After loading it is stored to an XMI format. Then it gets transformed to an application model.
* The application model is then combined with a [page template](https://github.com/Nasdanika/nasdanika.github.io/blob/main/engineering/page-template.yml) to produce a [resource model](https://docs.nasdanika.org/modules/core/modules/exec/modules/model/index.html).
* Then static HTML site files are generated from the resource model and a search index JavaScript file is generated from the site files.

[Nasdanika TOGAF ADM](https://docs.nasdanika.org/togaf/adm/activities/adm/index.html) flow model site is generated in a similar way:

* [Flow model](https://docs.nasdanika.org/modules/core/modules/flow/index.html) -> application model.
* Application model + page template -> resource model.
* Resource model -> HTML site.

### Using models in Java code

It is also possible to use a loaded model directly without a transformation.
E.g. if some Java application/microservice has a complex configuration it may be beneficial to create a configuration model and publish model documentation, which includes load specifications.

Then, the generated model jar file can be used to load configuration from, say, YAML and validate it.
The application would read its configuration using model API's, which may also contain configuration-specific logic.

With this approach configurations may be validated/tested separately from the application.
They can be "pre-validated" and "pre-deployed" - loaded from YAML and other resources, saved as XMI and deployed to a binary repository, maybe as a Maven jar.

Having a configuration model also opens an opportunity to use Eclipse-based editors instead of or in addition to working with YAML or JSON in a text editor. 

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