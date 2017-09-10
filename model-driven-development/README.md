# Model-Driven Development

This article is about model-driven development and the benefits it can bring to software development in large distributed organizations.

My favorite definition of software development, which I heard many years ago from Ivar Jackobson, goes as follows - _"Software development is a process of binding decisions to make them executable"_.

Based on this definition we can say that in order to efficiently build good software we need:

* Good decisions. 
* Efficient binding process.

Metaphorically speaking, to build a good house one needs quality bricks (decisions) and mortar (binding process).

Making a good decision requires deep knowledge of the problem and the domain. In enterprise software development such knowledge is distributed among multiple groups - business 
knows what to build, developers know how to build, and infrastructure knows about the systems the new system will have to integrate with and also where and how to deploy the new system.
Thus, enterprise software development involves extraction of knowledge from a number of groups, conversion of that knowledge to decisions which are then bound together into an executable system.

The process of knowledge extraction and decision making is a non-trivial one because different groups operate in different domains, they think and speak in different languages. 
Business speaks in terms of customers and products, developers in terms of classes and threads, and infrastructure in terms of data centers and servers.       

You may ask what modeling got to do with knowledge extraction and decision making and decision binding. In this article we'll deal primarily with [domain models](https://en.wikipedia.org/wiki/Domain_model), 
which are abstract representations of the knowledge and activities that govern a particular _application_ or [problem domain](https://en.wikipedia.org/wiki/Problem_domain). 
So, by their definition, domain models shall be useful for capturing and sharing knowledge.

It is important to keep in mind that all models are wrong - they don't describe reality in its entirety, but only some aspects of it relevant to the problem at hand. As such a particular model may  be quite useful to solve one problem and totally useless for another. 
For example, a map is a model of territory. The map is not the territory it describes and it shouldn't be. There may be different maps describing the same territory and highlighting different aspects, with each map being useful for its particular purpose.

So read on to find out how (domain) modeling can be leveraged to capture and disseminate domain/organizational knowledge, and reduce amount of manual effort, errors, and inefficiencies in software development practices.
There is a [companion presentation](https://www.slideshare.net/PavelVlasov2/modeldriven-development-and-code-generation) which contains key points and illustration. It might be a good idea to go through the presentation before reading this article - to get a general idea and decide whether it is of interest for you at all.  
  
## A very quick overview of EMF (Core)

Let's start with a quick look at [EMF](https://www.eclipse.org/modeling/emf/) because some modeling and code generation tools mentioned below are part of EMF, and some are based on EMF - these tools/frameworks are developed by the author and are available at [Eclipse Marketplace](https://marketplace.eclipse.org/) and/or [GitHub](https://github.com/nasdanika). 

In EMF one develops applications in the following way:

* Creates a domain model using either a [graphical editor](https://www.eclipse.org/ecoretools/), a tree editor, or [EMF-Forms based editor](https://www.eclipse.org/community/eclipse_newsletter/2016/february/article1.php). My preference is to start with a diagram editor to capture main model elements and their relationships and then switch to the tree editor for fine-tuning. A very important thing about the domain model is that it may define not only data - classes, attributes and references, but also behavior - operations.
* Generates model code and optionally edit and editor code.
* Implements business logic either as EOperations, or as external classes working on the model, or as a combination of thereof. 

One of salient features of EMF is automated merging of generated and hand-crafted code. And a nice thing is that one can use this functionality in their [own code](https://github.com/Nasdanika/codegen/blob/118f9dc88f5f568d144564c6c5f623c0ce32ce74/org.nasdanika.codegen/src/org/nasdanika/codegen/java/impl/CompilationUnitImpl.java#L159).
While code generation and modeling provide immense benefits, manual coding is still required. With auto-merging a person writing method implementations operates in the context of code generated from a model. The generated code provides higher level structure and plumbing allowing the developer to focus on coding a particular piece of functionality. 

It is also possible to create models with [XCore](https://wiki.eclipse.org/Xcore), but I faced some issues trying to persist XCore-generated models into a CDO repository.

[XText](https://www.eclipse.org/Xtext/) uses EMF as common data layer, i.e. it generates EMF models from grammars and parses its DSL's sources into EMF models.

Once you have a model it can be:

* [Stored to and loaded from XML](https://gist.github.com/pvlasov/dec50db2d0e8e33aac19f7f18e6e081e).
* [Persisted to a repository](https://wiki.eclipse.org/CDO) for concurrent transactional access. 
* Edited in a generated tree editor.
* Edited in a diagram editor created with [Sirius](https://eclipse.org/sirius/overview.html).
* Viewed and edited in Web UI using either [EMF Client Platform](https://eclipse.org/ecp/) or [Nasdanika CDO Web Bundle](https://github.com/Nasdanika/server/tree/master/org.nasdanika.cdo.web).     
* Edited in an XText-generated editor with syntax highlighting and error checking.

Also models can cross-reference each other so a large logical model may be broken into several resources (e.g. files) with different lifecycles and owned/maintained by different teams.

There are many more cool features of EMF such as transparent support of bi-directional references, change recording, CDO transaction handlers, validations, transparent resolution of proxy objects, ... but it's enough for a start.
You can check the web pages of different EMF technologies mentioned above to learn about how they can help you to build software better. 
In the following sections I'm going to provide a quick overview of Nasdanika CDO Web Bundle and Code Generators and explain several usage scenarios.

EMF provides the following benefits:

* Organizational/domain knowledge can be captured in models. The models can be annotated with additional information, e.g. descriptions of model elements. 
* Model documentation can be published to internet/intranet so it is available to a wide audience to (re)view, refine and form a common understanding of the problem domain. 
* Information can be entered into the models using a wide variety of generated editors - diagram, web, text, tree, forms - with validation of data being entered. 

## Nasdanika CDO Web Bundle

Nasdanika CDO Web Bundle ``org.nasdanika.cdo.web`` allows to interact with objects stored in a CDO repository over HTTP. It does it in the following way:

* Each CDO object has a URL, something like ``http://myserver/myapp/router/objects/L123``, containment-path URL's are also supported. Multiple route classes can be registered for a model class and the request path after the object path part is matched against registered routes. If there is a matching route, that route is invoked to perform processing. Dispatching routes allow to route requests to Java methods and/or EOperations using annotations and reflection.
* Contextual execution - for each request the routing servlet opens a transaction and "merges" HTTP request context and CDO transaction request context.
* A number of annotations are provided to declaratively match processing methods to request values, check authorization, apply repository locks and bind values to arguments of request processing methods/EOperations, e.g. request header value or OSGi service.
* Object/feature/operation level access control can be implemented declaratively in the model or programmatically. It also can be checked declaratively using method annotations or programmatically. In the latter case the application may modify its behavior based on principal/subject entitlements.
* User authentication can be performed externally (SSO). 
* It is also possible to retrieve group membership from external systems, e.g. LDAP. 

All of this reduces amount of plumbing code - developers create routes, which can be thought as micro web applications focusing on a particular Web UI functionality. 
With dispatching routes developers wire methods to requests using annotations and naming conventions and then focus on the request processing logic.
This process is similar to object-oriented development - like in OO languages behavior (methods) is bound to data (classes with fields), routes (behavior) are bound to data (CDO objects). 
And CDO objects may have their own behavior, which makes them much more powerful than "dumb" data structures supported by other persistent mechanisms.
Similarly to OO languages sub-classes can override behavior - routes registered for a sub-class take precedence in matching over super-class routes.

Metaphorically speaking, Nasdanika CDO Web route method is a "cubicle" with a phone, network connectivity, etc. So there is no need to, say, look up database objects - code is already executed in the context of an object, the same applies to services - they can be injected as method arguments using annotations.    

The difference between this bundle and ECP is that ECP leverages [RAP](https://www.eclipse.org/rap/) and RAP is a Web widget toolkit with SWT API. 
This is a very powerful approach because it allows to expose existing SWT UI's to the web, but it doesn't support per-feature access control and non-widget requests, e.g. REST API calls.  
     
[Application rendering](https://github.com/Nasdanika/server/blob/master/org.nasdanika.cdo.web/doc/application-rendering.md) part of the bundle renders [Bootstrap](http://getbootstrap.com/)-based Web UI
using model metadata. Default rendering can be customized with model annotations and/or resource bundles properties and by overriding rendering methods. 
This approach follows 90/9/1 rule - 90% of time the default rendering does the job, 9% of time customizations can be achieved using annotations and a rendering method override is required in 1% of cases.

Web UI elements for documented model elements feature help icons with tooltips. Mouse click on such icons opens a documentation dialog or navigates to the integrated model documentation (see below). This feature, along with the UI following the structure of the domain model, helps users to understand the UI behavior by studying the model documentation.  

This bundle was used to build a number of intranet web applications, including the [Cloud Console](../work-experience/citi/#cloud-console), [Analysis Repository](../work-experience/citi/#analysis-repository), and [Collaborative Decision Making](../work-experience/citi/#collaborative-decision-making). 


### Possible usage scenario - automate internal ad-hoc processes

Over the years I've seen the following situation many-many times - some internal systems don't integrate or don't support some domain concepts. 
In such situations the void is filled by Excel spreadsheets having hundreds and sometimes thousands of rows. 
Many people spend hours populating and updating them, and e-mailing around the organization.

WaterGile example: System A supports Epics, Features, Stories and Tasks. System B supports Projects. Epics must me mapped to Projects with some supporting information.   

Replacing such a spreadsheet with an intranet web application would provide the following advantages:

* Access control.
* Data validation.
* Scheduled automated notifications and escalations.
* Over time it may be possible to integrate some of the involved systems with the application even if they can't be integrated with each other.

## Nasdanika CDO Web Doc Bundle

[``org.nasdanika.cdo.web.doc``](https://github.com/Nasdanika/server/tree/master/org.nasdanika.cdo.web.doc) is a "companion" bundle for ``org.nasdanika.cdo.web``. It provides functionality for serving integrated documentation:

* Bundles, components and services information, including auto-generated dynamic UML diagrams. This allows to take a glimpse into the running application to better understand relationships between different application parts.
* Models documentation, also including auto-generated dynamic UML class diagrams. Such diagrams help in understanding of relationships between model elements.
* Hand-crafted documentation, e.g. user or developer manuals. The documentation may reference model elements and bundles/components. Also hand-crafted documentation can be "mounted" to model elements. 

Models documentation is treated as [markdown](https://en.wikipedia.org/wiki/Markdown), the bundle provides a number of rendering, link resolution, and other plug-ins, e.g. a plug-in for generating UML diagrams with [PlantUML](http://plantuml.com/). 

The [Documentation System Overview](https://server-side-java-development-for-innovators.books.nasdanika.org/chapter-0-setup/documentation-system-overview.html) chapter of the [Server-side Java Development for Innovators](https://server-side-java-development-for-innovators.books.nasdanika.org/) online book provides additional, although a bit outdated, information, including screenshots.

## Code Generation

This section explains advantages of model-driven approaches to code generation. 
The code generation approach explained below consists of capturing knowledge in models and then transforming those models to some output which either changes behavior of executable software 
(e.g. micro-services configuration files), or to an executable software itself, e.g. a Java/Maven project which build output is a micro-service.

Custom models and model editors, including web applications built with, say, Nasdanika CDO Web bundle can help with the extraction part - people can capture knowledge in structured and validated models as opposed to loosely structured media such as text documents or spreadsheets.     

This process may be compared to multiplication - application of automated transformation to multiple inputs - as opposed to addition - manually coding output for each input. 
As with multiplication and addition there is a break-even point - e.g. if the transformation shall be applied only once, then it is more efficient to do it manually, but if it is going to be 
applied many times over, it may make sense to do it manually once, then parameterize, templatize and automate.

In my experience, transformations/templates tend to become too complex and difficult to understand pretty quickly. 
Sections below outline several tools and approaches which help to simplify the transformation/code generation process and keep it clear and understandable.         

### Nasdanika Codegen

#### Generators model

There are multiple ways to generate code. For example, Eclipse resources API to work with projects, files, and folders; JDT API to work with packages and compilation units; JMerger to automatically merge generated and hand-crafted code, different template engines, ...

[Nasdanika Codegen](https://github.com/Nasdanika/codegen) provides a model which abstracts multiple generation approaches. 
It also provides a model editor and abstract classes for creating wizards and multi-form editors to collect input from users to be used as input for the generation models.
Users of the model and the editor operate with the concepts of Eclipse IDE - projects, folders, files, packages, classes, interfaces, methods, etc. instead of disparate low-level API's to generate those. 

Using the generator model editor experts in a particular technology, say Spring Boot, can create generator models in a visual way and without having to deal with low-level generation API's. 
Also the model and the editor makes it easier to understand the generation process and refine it, as well to modify it when requirements change. 
This would be an example of expertise/knowledge capturing and multiplication - code generation expertise captured in the generators implementations is multiplied by the Spring Boot expertise captured in the generator model.
And both of them are multiplied by user input provided in a wizard, e.g. Maven group ID, version, and root package name, producing generated code. 

The generator model allows to assemble Java classes from multiple pieces. 

Generator controllers can be used to pull additional information from different sources. For example, a controller may use [Apache POI](https://poi.apache.org/) to read Microsoft Word and Excel documents stored in SharePoint. 
In a prototype I was able to read hundreds of tables with thousands of rows representing mainframe data structures. This data could be used to generate either a mainframe access layer or a mainframe ECore model which then could be used to generate
bounded contexts and Anti-Corruption Layers for micro-services (see below).     

#### Wizard model and EMF Forms based wizard

There is a [wizard](http://www.nasdanika.org/products/codegen/apidocs/org.nasdanika.codegen.editor/apidocs/org/nasdanika/codegen/presentation/AbstractModelCodegenWizard.html) which takes an input model and renders wizard pages using EMF Forms or [EObjectRenderer](http://www.nasdanika.org/products/presentation/apidocs/org.nasdanika.presentation/apidocs/org/nasdanika/presentation/EObjectRenderer.html).
This approach makes building code generation wizards much easier because developers don't need to work on the UI code except for edge cases. 

### Nasdanika Codegen Ecore

[Nasdanika Codegen Ecore](https://github.com/Nasdanika/codegen-ecore) allows to generate code for selected elements of the source model using selected generation targets. 
Generation targets may contribute configuration model elements to allows users to customize generation. EMF Forms or EObjectRenderer are used to render the configuration model elements thus freeing the generator developers from having to work with SWT/JFace. 

Speaking in [Domain-Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) terms, it allows to generate Bounded Context and Anti-Corruption Layer from the canonical domain model and generators for a particular back-end. 

#### Example

An organization may have a canonical domain model which is a superset of data elements and operations used by different lines of business and systems. In a simple case that model may represent a database schema. 
A particular system (e.g. a micro-service) may operate on a tiny fraction of model elements. For example, Transaction class may contain dozens of attributes in the canonical model, but "Account details"
micro-service may need only transaction date, amount, and description attributes. It may also want to cache them.

This is how this problem can be solved with Nasdanika Codegen Ecore:

* The canonical model is stored as Ecore model. In addition to being input to the generator it can also be hosted on an intranet Nasdanika documentation server (Information center), helping the organization to speak the "Ubiquitous language".
* A generation target is created for a particular back-end or several back-ends.
* The micro-service team uses the editor to select classes and attributes of the canonical model which are used by their code. They also may configure the generation target, e.g. specify format pattern for the date, and configure caching.
* Then the micro-service team generates bounded context classes or interfaces and Anti-Corruption Layer classes. Because the bounded context classes are generated from the canonical model they will be the same for all back-ends, only the Anti-Corruption Layer will change. And because the bounded context classes don't change, the micro-service code also would require only minor changes to switch to another back-end or to support several back-ends.         

#### Web UI Generation Target

[Nasdanika Codegen Ecore Web UI Generation Target](https://github.com/Nasdanika/codegen-ecore-web-ui) is a concrete example of the above scenario. 
In this case the repository model is used as the input model to select elements to be exposed through the Web UI. The generator model can be used to configure how the elements are to be exposed.
The generator target outputs rendering and routing classes as well as resource bundles to be used by the Nasdanika CDO Web Bundle Application Rendering framework. 

The generation is performed by a generator model created with the Nasdanika Codegen and accompanied by several controllers. With this target the output is created by "multiplication" of three models:

* Target generator model.
* Target configuration model.
* Selection model.

## Call for action

I hope that article will help you to discern more opportunities to improve software development practices in your organization as well as give you some ideas regarding how it can be done. 

Below are some steps you may take:

* Start thinking about software development in terms of decisions binding and knowledge extraction, capturing, dissemination, and transformation - especially multiplication.
* Capture domain knowledge in documented models and host model documentation on the intranet.
* Capture repetitive coding patterns in generation model and create wizards for materializing those patterns.
* Improve knowledge gathering - ask people for possible contribution - enter data into Word/Excel document and save on SharePoint, give them a tool, e.g. an intranet web application or a specialized GUI model editor. Many a micle makes a muckle.
* Incorporate code generation into the build process - code generators do not require GUI and may be invoked in a headless fashion from an [IApplication](http://help.eclipse.org/oxygen/topic/org.eclipse.platform.doc.isv/reference/api/org/eclipse/equinox/app/IApplication.html) implementation. Using an example above there can be a process monitoring SharePoint file with mainframe data structures definitions for modifications and triggering generation of Ecore model from the file. This way knowledge is automatically propagated - mainframe people don't have to learn new tools and techniques - they just update the file following a pre-defined format, and the rest is taken care of by generators.
* Create web applications based on captured domain models to automate and improve internal processes.
* When adopting a new technology use your best talent to prototype and identify patterns and create code generators which will be used over and over throughout the organization in a robust and repeatable way instead or in addition to creation of presentations and cookbooks. Experts are hard to come by and even harder to scale. 
* Convert existing cookbooks to code generators where it makes sense.

## References

* [Nasdanika](https://github.com/Nasdanika).
* [Companion presentation](https://www.slideshare.net/PavelVlasov2/modeldriven-development-and-code-generation) - key points and illustrations.

## Appendix: Chronology

Work in progress - How the vision evolved - AWK, Antlr/Hammurapi/Jsel, SQL compiler. 
Tried different metadata - database - limited, no behavior. XML - too much work to set up tooling/schema.

