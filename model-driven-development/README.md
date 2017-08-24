# Model-Driven Development

This article is about model-driven development and the benefits it can bring to software development in large distributed organizations.

My favorite definition of software development, which I heard many years ago from Ivar Jackobson, goes as follows - _"Software development is a process of binding decisions to make them executable"_.

Based on this definition we can say that in order to efficiently build good software we need:

* Good decisions. 
* Efficient binding process.

Metaphorically speaking, to build a good house one needs quality bricks (decisions) and mortar (binding process).

To make a good decision one needs to possess good knowledge of the problem. In enterprise software development the knowledge required to build a software system is distributed among multiple groups
- business knows what to build, developers know how to build, and infrastructure knows about the systems the new system will have to integrate with and also where and how to deploy the new system.
Thus, enterprise software development involves extraction of knowledge from a particular group, conversion of that knowledge to decisions which are then bound together into an executable system.

The process of knowledge extraction and decision making in a non-trivial one because different groups operate in different domains, so they think and speak in different languages - business speaks in terms of
customers and products, developers in terms of classes and threads, and infrastructure in terms of data centers and servers.       

So this article explains how modeling can be leveraged to capture and disseminate domain/organizational knowledge, and reduce amount of manual effort and errors. 
  
## A very quick overview of EMF (Core)

Let's start with a quick look at [EMF](https://www.eclipse.org/modeling/emf/) because some modeling and code generation tools mentioned below are part of EMF, and some are based on EMF - these tools/frameworks are developed by the author and are available at [Eclipse Marketplace](https://marketplace.eclipse.org/) and/or [GitHub](https://github.com/nasdanika). 

In EMF one develops applications in the following way:

* Creates a domain model using either a [graphical editor](https://www.eclipse.org/ecoretools/), a tree editor, or [EMF-Forms based editor](https://www.eclipse.org/community/eclipse_newsletter/2016/february/article1.php). My preference is to start with a diagram editor to capture main model elements and their relationships and then switch to the tree editor for fine-tuning. A very important thing about the domain model is that it may define not only data - classes, attributes and references, but also behavior - operations.
* Generates model code and optionally edit and editor code.
* Implements business logic either as EOperations, or as external classes working on the model, or as a combination of thereof. 

One of very strong features of EMF is automated merging of generated and hand-crafted code. And a nice thing is that one can use this functionality in their [own code](https://github.com/Nasdanika/codegen/blob/118f9dc88f5f568d144564c6c5f623c0ce32ce74/org.nasdanika.codegen/src/org/nasdanika/codegen/java/impl/CompilationUnitImpl.java#L159). 

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

There are many more cool features of EMF, e.g. transparent support of bi-directional references, change recording, CDO transaction handlers, validations, transparent resolution of proxy objects, ... but it's enough for a start.
You can check the web pages of different EMF technologies mentioned above to learn about how they can help you to build software better. 
In the following sections I'm going to provide a quick overview of Nasdanika CDO Web Bundle and Code Generators and explain several usage scenarios.

EMF provides the following benefits:

* Organizational/domain knowledge can be captured in models. The models can be annotated with additional information, e.g. descriptions of model elements. 
* Model documentation can be published to internet/intranet so it is available to a wide audience for (re)view, refine and form a common understanding of the problem domain. 
* Information can be entered into the models using a wide variety of generated editors - diagram, web, text, tree, forms - with validation of data being entered. 

## Nasdanika CDO Web Bundle

Nasdanika CDO Web Bundle ``org.nasdanika.cdo.web`` allows to interact with objects stored in a CDO repository over HTTP. It does it in the following way:

* Each CDO object has a URL, something like ``http://myserver/myapp/router/objects/L123``. Multiple route classes can be registered for a model class and the request path after the object path part is matched against registered routes. If there is a route for path, that route is invoked to perform processing. Dispatching routes allow to route requests to Java methods and/or EOperations.
* Contextual execution - for each request the routing servlet opens a transaction and "merges" HTTP request context and CDO transaction request context.
* A number of annotations are provided to declaratively match processing methods to request values, check authorization, apply repository locks and bind values to arguments of request processing methods/EOperations, e.g. request header value or OSGi service.
* Object/feature/operation level access control can be implemented declaratively in the model or programmatically. It also can be checked declaratively using method annotations or programmatically. In the latter case the application may modify its behavior based on principal entitlements.

All of this reduces amount of plumbing code - developers create routes, which can be thought as micro web applications focusing on a particular Web UI functionality. 
With dispatching routes developers wire methods to requests with annotations and naming conventions and then focus on the request processing logic.      
This process is similar to object-oriented development - like in OO languages behavior is bound to data, routes (behavior) are bound to data (CDO objects). 
And CDO objects may have their own behavior, which makes them much more powerful than "dumb" data structures supported by other persistent mechanisms.
Similarly to OO languages sub-classes can override behavior - routes registered for a sub-class take precedence in matching over super-class routes.

Metaphorically speaking Nasdanika CDO Web route method is a "cubicle" with a phone, network connectivity, etc. So there is no need to, say, look up database objects - code is already executed in the context of an object, the same applies to services - they can be injected as method arguments using annotations.    

The difference between this bundle and ECP is that ECP leverages [RAP](https://www.eclipse.org/rap/) and RAP is a Web widget toolkit which looks to the rest of the application as SWT components. 
This is a very powerful approach because it allows to expose existing SWT UI's to the web, but it doesn't support per-feature access control and non-widget requests, e.g. REST API calls.  
     
[Application rendering](https://github.com/Nasdanika/server/blob/master/org.nasdanika.cdo.web/doc/application-rendering.md) part of the bundle renders [Bootstrap](http://getbootstrap.com/)-based Web UI
using model metadata. Default rendering can be customized with model annotations and/or resource bundles properties and by overriding rendering methods. 
This approach follows 90/9/1 rule - 90% of time the default rendering does the job, 9% of time customizations maybe achieved using annotations and a rendering method override is required in 1% of cases.

Web UI elements for documented model elements feature help icons with tooltips. Mouse click on such icons opens a documentation dialog or navigates to the integrated model documentation (see below). This feature, along with the UI following the structure of the domain model, helps users to understand the UI behavior by studying the model documentation.  

This bundle was used to build a number of intranet web applications, including the [Cloud Console](../work-experience/citi/#cloud-console). 

## Nasdanika CDO Web Doc Bundle

[``org.nasdanika.cdo.web.doc``](https://github.com/Nasdanika/server/tree/master/org.nasdanika.cdo.web.doc) is a "companion" bundle for the ``org.nasdanika.cdo.web``. It provides functionality for serving integrated documentation:

* Bundles, components and services information, including auto-generated dynamic UML diagrams. This allows to take a glimpse into the running application to better understand relationships between different application parts.
* Models documentation, also including auto-generated dynamic UML class diagrams. Such diagrams help in understanding of relationships between model elements.
* Hand-crafted documentation, e.g. user or developer manuals. The documentation may reference model elements and bundles/components.  

Models documentation is treated as [markdown](https://en.wikipedia.org/wiki/Markdown), the bundle provides a number of rendering, link resolution, and other plug-ins, e.g. a plug-in for generating UML diagrams with [PlantUML](http://plantuml.com/). 

Also hand-crafted documentation can be "mounted" to model elements.

The [Documentation System Overview](https://server-side-java-development-for-innovators.books.nasdanika.org/chapter-0-setup/documentation-system-overview.html) chapter of the [Server-side Java Development for Innovators](https://server-side-java-development-for-innovators.books.nasdanika.org/) online book provides additional, although a bit outdated, information, including screenshots.

## Code Generation

This section explains advantages of model-driven approaches to code generation. The picture below demonstrates the process of code generation, 
although it also applies to software development in general - knowledge required to build a software system is extracted from the organization and then transformed into executable software. 

![tree](code-generation-tree.png)

Custom models and model editors, including web applications built with, say, Nasdanika CDO Web bundle can help with the extraction part - people can capture knowledge in structured and validated models as opposed to loosely structured media such as text documents or spreadsheets.   
  
Code generation, or model transformation to speak more generally, helps in transforming input data/model into output data/model, which can be either used by an executable software or
be an executable software itself. For example, an XML file can be transformed into Java sources using templates.

This process may be compared to multiplication - application of automated transformation to multiple inputs - as opposed to addition - manually coding output for each input. 
As with multiplication and addition there is a break-even point - e.g. if the transformation shall be applied only once, then it is more efficient to do it manually, but if it is going to be 
applied many times over, it may make sense to do it manually once, then parameterize, templatize and automate.

In my experience, transformations/templates tend to become too complex and difficult to understand pretty quickly. 
Sections below outline several tools and approaches which help to simplify the transformation/code generation process and keep it clear and understandable.         

### Nasdanika Codegen

#### Generators model

There are multiple ways to generate code. For example, Eclipse resources API to work with projects, files, and folders; JDT API to work with packages and compilation units; JMerger to automatically merge generated and hand-crafted code, different template engines, ...

[Nasdanika Codegen](https://github.com/Nasdanika/codegen) provides a model which abstracts multiple generation approaches.
It also provides a model editor and abstract classes for creating code generation wizards. 

Using the generator model editor experts in a particular technology, say Spring Boot, can create generator models in a visual way and without having to deal with low-level generation API's. 
Also the model and the editor makes it easier to understand the generation process and refine it, as well to modify it when requirements change.   

#### Wizard model and EMF Forms based wizard

There is a [wizard](http://www.nasdanika.org/products/codegen/apidocs/org.nasdanika.codegen.editor/apidocs/org/nasdanika/codegen/presentation/AbstractModelCodegenWizard.html) which takes an input model and renders wizard pages using EMF Forms or [EObjectRenderer](http://www.nasdanika.org/products/presentation/apidocs/org.nasdanika.presentation/apidocs/org/nasdanika/presentation/EObjectRenderer.html).
This approach makes building code generation wizards much easier developers don't need to work on the UI code except for edge cases. 
Also this approach demonstrates "models and knowledge multiplication" - the wizard model is used to collect knowledge from users, and the generation model is used to capture the expertise of developers. 
Then the two models are "multiplied" by producing generated code.

### Nasdanika Codegen Ecore

[Nasdanika Codegen Ecore](https://github.com/Nasdanika/codegen-ecore) allows to generate code for selected elements of the source model using selected generation targets.

Speaking in [Domain-Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) terms it allows to generated Bounded Context and Anti-Corruption Layer from a canonical model and generators for a particular back-end. 

#### Example

An organization may have a canonical domain model which is a superset of data elements and operations used by different systems. In a simple case that model may represent a database schema. 
A particular system (e.g. a micro-service) may operate on a tiny fraction of model elements. E.g. Transaction class may contain dozens of attributes in the canonical model, but "Account details"
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




The core modeling technology, on which most of the other technologies mentioned in this article are built, is  - Eclipse Modeling Framework.    

80/20 principle. No coding is a myth - 2000 characters-long XPath expressions. As little coding as possible - heighten the level of abstraction.





improving communication

Tree picture.

extracting knowledge

speak to SME's using their language.

90% mistakes due to poor communication

Links to resume pages.


Vast enterprise metadata, including Word and Excel documents - example of pulling out mainframe data definitions from a Word document using Apache POE. Pull from SP, read Word doc.

Pull from SVN.

Information center, static model doc generation - in progress.

Codegen wizard model - minimal if any coding, saving the model for later re-use, possibility of using the Web UI for filling-out the model and then generating code.

Why CDO - XML and repo persistence.

Overview of model projects and their purpose - security - role-base access, how it is different from CDO security, cdo.web, code generators - ecore - bounded context, ...

Annotations - markdown, YAML. Validations. Multiple representations - editor, web, diagram (Sirius), grammar (XText/XCore). EMF Forms simplify user input.

Merging of manual and generated code. A person writing method implementations operates in the bounded context of the generated model - they can focus on the method to implement and higher level structure is generated from the models.

 
Codegen - constructing Java classes from pieces - different pieces might be owned by different teams and pull information from different sources.

Tried different metadata - database - limited, no behavior. XML - too much work to set up tooling/schema.

Early/late binding - generate-in, configuration at runtime

Problems with late binding: 

* No control 
    * Developers may mess at development time - misinterpret the design document.
    * Operations may mess at deployment time. 
* Hard to troubleshoot - limited access to production and too many permutations of configuration.

Effective knowledge is important in large organizations - repetitive patterns specific to the organization. Cookbooks are subject to interpretations, and sometimes don't get updated due to time pressures.


Addition vs. multiplication.

Improvement of internal processes.

Knowledge gathering - ask people of possible contribution - enter data into Word/Excel document and save on SharePoint, give them a tool, e.g. an intranet web application. Many a micle makes a muckle.


Right time binding.

Avoid EMF dependency - generate code and/or XML/JSON/YAML configuration.

Code merging, transformation. 

Mainframe -> MS Word - Apache POI -> model.

Screenshots - Generator model, Ecore editor - check, Generated doc (Info center and static later).

Multiple representaion of the same model - XText - https://www.eclipse.org/Xtext/, Sirius - https://www.eclipse.org/sirius/, different parts of the overall model may be created/edited by different editors.

compilation/translation vs interpretation

Merging - not everything can be generated.

To demonstrate the value of (Model-Driven) Code Generation I'm going to refer to [Building a pipeline vs. hauling buckets](http://www.getmotivation.com/prosperity/wealth-pipline-Robert-Kiyosaki.htm) story by Robert Kiyosaki.

If you think about enterprise software development in terms of the above definition and pipline vs. buckets metaphor, you will likely realize that in  many traditional development processes 
"buckets" of knowledge are hauled over and over for each new project - from one person or group to another through documents or conversations. 
Similar to the story, along the way the knowledge spills (people forget), gets dirty (misinterpretation) and becomes stale (gets outdated).

Also there is a great deal of manual binding of decisions - e.g. writing repetitive database access code which follows the same pattern for hundreds if not thousands of fields.  
   
Some of disadvantages of manual decision binding, such as repetitive coding mentioned above, are:

* Low speed of change propagation - if the database structure changes or the access pattern changes, then access code shall be manually re-coded. What actually happens more often is that the new and better pattern is never implemented - due to the risk of touching working code, and required time and effort - "What goes in, stays in".
* High cost.
* High probability of error - the old "To err is human".




## Knowledge pipeline

Command line generation, build pipeline, rule engine, multiple inputs

Kiosaki - http://www.reducestressnow.net/pipeline/ - Are you Hauling Buckets - or Building a Pipeline?

talk to SME - carry, spill. Pipeline - knowledge carried along and transformed automatically. Takes time to build. Makes sense for repetitive processes.

Organizational knowledge delivered to customers as executable software.

Alternative cost college education vs. work. 

Extending CI/CD pipeline.

Generation process can be customized 
Word POI (almost real life) example - controller pulling info from MLI's using config property (URL) to generate java beans. 



## Summary

create models, intranet web apps, generator models, enhance knowledge extraction, extend ci/cd pipeline

use your best talent to prototype and identify patterns and create code generators which will be used over and over throughout the organization in a robust and repeatable way

de-clog knowledge pipelines. 


## Chronology

How the vision evolved - AWK, Antlr/Hammurapi/Jsel, SQL compiler. 