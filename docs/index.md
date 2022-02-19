# Pavel Vlasov

<table>
	<tr>
		<td rowspan=5><img src="pavel-vlasov.jpg"/></td>
		<td>E-Mail: <a href='ma&#105;lto&#58;pavel&#64;v&#37;6Ca&#115;o%76%2&#69;us'>p&#97;vel&#64;v&#108;a&#115;ov&#46;&#117;s</a></td>
	</tr>
	<tr>
		<td><a href="cover-letter.html">Cover Letter</a></td>
	</tr>
	<tr>
		<td><a href="https://www.linkedin.com/in/pavelvlasov">Linked-In Profile</a></td>
	</tr>
	<tr>
		<td><a href="https://github.com/pvlasov">GitHub</a></td>
	</tr>
	<tr>
		<td>Web site: <a href="https://nasdanika.org">Nasdanika</a></td>
	</tr>
	<tr>
		<td><a href="https://github.com/pvlasov/cv/blob/master/docs/index.md">Source</a></td>
	</tr>
</table>		
	
Over 28 years of experience in Information Technology with 25 of them in the Financial Services industry, which includes 20 years in banking.

* TOC
{:toc}

## Highlights

* Developer Experience
* Inner Source
* Innovation
* Cloud
* Java
* Eclipse development
* Model-based Systems Engineering

## Experience

### Citi Global Consumer Group

_Senior Vice President, 2005 - Present_

During my time at Citi Global Consumer group I worked in different parts of the CTO organization.

#### Engineering & Architecture

My current role is a **Chief Architect of Developer Experience** with immediate focus on improving developer experience for Java developers on OpenShift.

As part of larger Developer Experience efforts we've established a capability to develop and deliver a connected[^1], role-specific[^2], cross-referenced[^3], hyper-local[^4] visualized[^5] and interactive[^6] developer experience "as code"[^7] in a form of journeys[^8]. 
We've also documented OpenShift new solution journey using the above capability.

[^1]: Journey activities are connected to each other with transitions and calls. Generated context visualizations previous and subsequent activities - "You are here", so to speak.

[^2]: Activities are performed by roles. Support of simple activity to role reference as well as RACI matrix.

[^3]: Bi-directional references between activities, tools, roles and deliverables.

[^4]: Infinite nesting of activities allows to create highly focused activity documentation.

[^5]: Generated state diagram visualizaitons with ability to manually edit generated visualizations and manually create visualizations from scratch. 

[^6]: Generated state diagrams have clickable activity shapes navigating to the clicked activity documentation.

[^7]: Journeys are defined with YAML and Markdown stored in a source control system. Documentation is generated with a Maven build.

[^8]: Journey is a directed graph of activities performed by roles using tools and consuming and producing deliverables. Journey is a subclass of activity and as such journeys can be infinitely nested.


Our Developer Experience portfolio also includes the following items:

* **Documentation as code** - a practice for documenting artifacts stored in source repositories, e.g. Java libraries, with documentation sources stored in the same repository and documentation sites generated from those sources. The practice includes a capability of site federation - generation of a single site for multiple components from information retrieved from multiple source repositories. A prototype portal hosting documentation of 60+ components in 10+ domains was created by applying the practice. The practice allows to create self-contained projects with everything stored in a source repository including roadmap items, issue categories such as "Good first issue", persona definitions, and discussion forums. It allows to use a unified approach to community engagement - create a pull request. It is conducive to innovation as it allows to create an elaborated idea "as code" and then collaborate on it.
* **Code generation** - a practice for creating code generators using declarative YAML models and templates derived from reference implementations.
* **Eclipse ecosystem** - eclipse packages, eclipse plug-ins and update sites. Ability to build Citi-specific Eclpse packages, install approved third-party plug-ins and to build Citi-specific plug-ins including DX journey documentation plug-ins to bring DX to developers' fingertips.

Some of the above capabilities are already available for consumption while others were prototyped and await productization.

To prioritize our pipeline we use developer personas with goals and we align our efforts to persona goals.
Developer personas and their goals are defined using a variety of techniques including analysis of survey results.

As part of the Developer Experience efforts we've established a concept of the knowledge continuum similar to the [TOGAF Enterprise Continuum](https://pubs.opengroup.org/architecture/togaf9-doc/arch/chap35.html) with thir-party documentation being most generic, documentation for internal libraries and services being in the middle, and journey activity documentation being most to specific.


I'm also participating in several company-wide efforts, e.g.

* Defining a capability to run OpenShift clusters on developer workstations to provide a tight local development loop.
* [InnerSource](https://en.wikipedia.org/wiki/Inner_source). As part of this effort I've created an intranet site hosting GCT InnerSource body of knowledge including Trusted Committer Get Started Guide. I've also created several starter projects for inner source components as well as documentation-as-code sites for existing components.

#### Product owner of Citi Cloud Platform Integration Services domain.

_June 2017 - July 2019_

Product owner of the Cloud & Integration Services team. The team owned more than 30 software platform components used by application development teams. 
The components owned by the team were organized into four "pillars":

* Cloud enablement.
* Distributed data services, which covers:
    * Caching solutions such as GemFire,
    * No-SQL databases such as MongoDB,
    * Relational databases,
    * Data synchronization and reconciliation.
* Integration.
* Productivity, which includes:
    * Eclipse plug-ins such as specialized editors and project/workspace wizards.
    * "Nexus Advisors" - a family of model-driven web applications providing insight into different aspects of the Citi cloud:
        * Microservice configuration files.
        * Maven dependencies.
        * Cloud Foundry applications and instances.
    * Microservice configuration editor - a [Master-detail EMF editor](https://github.com/Nasdanika/presentation#master-detail-form-and-viewer) with a custom ResourceFactory and Resource implementations which transparently parsed YAML configuration file into a service configuration model and saved the model into a YAML file.    
    * Model-driven development and code generation in general as the foundation for the above items.
    * Eclipse IDE packages with pre-installed plug-ins.
    * Docker machine and image registry which contains images with pre-installed cloud components such as config server and Eureka to simplify local development and testing.       

When I became a product owner the previous product owner moved to another position within Citi taking the most of the team with them. 
The remaining 3 people had been with the team for a few months and one of them eventually left the team. 
People who joined our team were totally new to Citi. So the new team of 8 developers plus the product owner and the scrum master had to quickly get a grasp of what we came to own. 
We achieved it by "dividing and conquering" - each component was assigned a primary and a secondary owner. 
The owners created and deployed to the Citi intranet Maven sites for components they own.
The sites featured component overview, Java API documentation, roadmap and changelog pages. 
Microservice sites also feature generated REST API documentation.

We've also created and deployed a Maven team site for the team which lists components grouped in categories (pillars) and sub-categories. Component listings provided links to the component sites. 
All the sites have the same style. The breadcrumbs of the team site and the component sites provide a uniform experience of main site/child site.

The primary target audience of the component/team sites were developers and architects who use our components. The component/team sites had releases tied to sprints. 

In addition to the component and team sites we've set up a team wiki where we capture and refine team processes, e.g. the component site publishing process. 
The team wiki's target audience was the team, although some other teams have started following our processes as well. The wiki evolved continuously.  

In this role I wore two hats - a product owner and a dev lead of the Productivity pillar. Worked with the team "customers" to understand their needs and built roadmaps which then were elaborated into features and stories in the team backlog.
Before a start of a new sprint stories were prioritized and assigned to the team members with capacity and skillset in mind. 

In addition to the team wiki I've also established and maintained a wiki for the architecture organization where multiple teams contributed.

#### Application Modernization

_September 2016 - June 2017_

In September 2016 I left the R&D team to become a lead of the Application Modernization domain of the Citi Nexus Platform. 
The focus of the team was to provide solutions for conversion of monolithic applications into micro-services. 

One of the monoliths which we worked with was a Java Web Application project with:

* 14 thousand Java classes organized into a thousand of packages. 
* 2.5 million lines of code.
* About 180 thousands methods and 75 thousands fields. 
* Approximately 80% of code resided in packages with circular dependencies which made it very difficult to modularize the application.
* About two hundred thousand of non-Java assets such as images, JavaScript files, configuration files, JSP's.

The above metrics do not include dependencies, just the application per se. 

First we started with [Sonargraph-Explorer](https://www.hello2morrow.com/products/sonargraph/explorer) to get a feeling of what we were facing. 
Sonagraph is a very nice tool but because of the huge number of classes involved in the circular dependency "black hole" we needed a more advanced tooling.

First we created an [Ecore](https://www.eclipse.org/modeling/emf/)/[CDO](https://wiki.eclipse.org/CDO) model of the Java language which included not only declarative things as in the ``java.lang.reflect`` package, but also call trees, field references and bi-directional inheritance references. 
After that we created a model loader which leveraged [ASM](http://asm.ow2.org/) to walk through the bytecode and populate the model.

Once we had the model and the loader we created a model-driven web application to browse loaded models in order to get better understanding of the codebase - "Analysis repository". 
The application used [PlantUML](plantuml.com) to visualize the model via class context diagrams and method sequence diagrams.
After we loaded several modules the application repository had about 2 million objects - packages, classes, methods, fields. The performance was not lightning fast, but acceptable and the repository database was about 250 megabytes.    

Using ASM we also created a code instrumentation tool which would take a jar file and data collection endpoint URL as input and output a jar with bytecode instrumented to report call trees to the endpoint.
We've also added a data collection endpoint to the Analysis repository.   
Collection of runtime call tree information was intended to complement static analysis by recording reflective calls.

The next step for us was creation of an Eclipse plug-in for module extraction. Given a number of entry points (classes, methods) the plug-in was able to extract a sub-set of the source project codebase traceable from the entry points.
In classes the plug-in would only extract class members traceable from the entry points. E.g. if a class had a hundred members but only ten of them were traceable from the sources the plug-in would extract only those ten. 

The plug-in used the loader module and [Eclipse JDT](https://www.eclipse.org/jdt/) to analyze source code, and JDT refactoring capabilities to extract the code into a new module.

The plug-in was implemented as a multi-form editor with one page/form presenting a source checkbox tree allowing the user to select entry points. Other pages/forms collected additional extraction parameters. 
Module extraction configuration was stored in JSON with transparent loading to an EMF model and saving the EMF model to JSON. The editor used [EMF Data Bindings](http://www.vogella.com/tutorials/EclipseDataBindingEMF/article.html) with TransactionalEditingDomain to support Undo/Redo of complex model manipulations.

We've set up a team wiki where we documented our work and also collected "how-to's" for different technologies which we used - JDT, JFace Data Bindings, EMF, ...         

#### Research & Development

* **Tag Management Solution Selection** - Participated in a tag management solution selection effort. Evaluated several leading tag management solutions. Created a test harness for comparing difference in web pages performance before and after deployment of the tag management solution. The harness used Selenium Web Driver to load pages in different browsers, [Navigation Timing API](https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html) to collect page load timings, and an OSGi/Equinox container with CDO/H2 model repository to store collected data, and Jetty to display stats (min, max, avg, deviation) and charts using [Flot](http://www.flotcharts.org/).

* **Functional/Acceptance Testing Automation** 
    * Web applications
        * Established a process for automated functional testing of Web applications with [Selenium WebDriver](http://docs.seleniumhq.org/projects/webdriver/), [JUnit](http://junit.org/), and [Jenkins](http://jenkins-ci.org/). 
        * Created JUnit-[HP Quality Center](http://www8.hp.com/us/en/software-solutions/quality-center-quality-management/) integration using annotations and Quality Center RESTful API's. 
        * Demonstrated execution of tests in different browsers on different operating systems with Jenkins multi-configuration (matrix) builds and with [Selenium Grid](https://code.google.com/p/selenium/wiki/Grid2).
        * Demonstrated different approaches to testing and reporting with plain JUnit, [JBehave Web](http://jbehave.org/), and [Thucydides](http://www.thucydides.info/).
    * Mobile Applications - Demonstrated an approach to automating functional tests of Android applications in emulators and on real devices with [Selendroid](http://selendroid.io/), [Appium](http://appium.io/), and Selenium Grid.
* **Continuous Delivery & Continuous Inspection**
    * Set up an environment and process for the R&D team to build and deploy Java libraries, J2EE Web applications and TIBCO Business Works processes with Jenkins [Maven](http://maven.apache.org/) builds, [Sonatype Nexus OSS](http://www.sonatype.org/nexus/), and SonarQube. Jenkins pulls sources from [Subversion](https://subversion.apache.org/) and [Rational Team Concert](https://jazz.net/products/rational-team-concert/). 
    * Migrated several existing projects from Ant to Maven.
    * Set up a Continuous Delivery Wiki site with cookbooks and links to the tools and additional information.
* **JavaScript API's** - demonstrated how banking domain model can be exposed as JavaScript API in accordance with Web-Oriented Architecture principles. JavaScript was generated from a model because hand-crafting would be labor-intensive and error-prone. The model was created in [Eclipse Modeling Framework (EMF)](https://www.eclipse.org/modeling/emf/) and populated either by importing XML schemas or manually using an EMF-generated editor. Generated JavaScript was used either in the browser or on [Node.js](http://nodejs.org/) and could retrieve server/back-end data in XML and JSON formats over HTTP and [WebSocket](https://en.wikipedia.org/wiki/WebSocket). Measured and compared network traffic using the new approach vs. current, which showed significant reduction. An overview of principles and technologies:
    * The API was organized into namespaces containing classes which in turn contained attributes and functions.
    * Multiple inheritance.
    * The model supported templates in [doT.js](http://olado.github.io/doT/index.html) which were compiled to JavaScript at generation time.
    * Templates could be parameterized or parameterless. Parameterless templates were generated as read-only properties, e.g. ''Customer.home'' would render customer home page. Parameterized templates were generated as functions.
    * Multi-resource (multi-file) models, e.g. global/core class definitions in one model resource or a set of resources and LOB/region specific definition another.
    * Lazy (on-demand) loading of classes, data (attributes), and functions/templates. 
    * Attributes were mapped to service calls. Once service call could retrieve multiple attributes and one attribute could be retrieved by multiple services. Conceptually services were overlapping fetch groups. 
    * Attributes could have validations associated with them.
    * Classes were loaded on demand in the browser with [RequireJS](http://requirejs.org/).
    * Functions/templates could be marked to be loaded on demand in the model - this feature was useful for network traffic optimization in case of large infrequently used templates.
    * Getters/setters were used to abstract API users from on-demand loading/partial population.
    * Synchronous and asynchronous modes - same API with asynchronous mode loading returning [Q](https://github.com/kriskowal/q) promises instead of data values.
    * Syntax highlighting editors for functions, services and templates code.
    * [Backbone.js](http://backbonejs.org/)-based single-page application.
    * A thin messaging layer over WebSocket emulating JMS request/reply API.
    * Node.js application was built with [Express](http://expressjs.com/), [Connect](https://github.com/senchalabs/connect#readme), and [SuperAgent](http://visionmedia.github.io/superagent/).
    * Computed attributes.
    * Metadata management - classes could have instance and class attributes and functions. Attributes could have default values. Class attributes, as well as instance attributes, could be loaded from services, which in case of class attributes could be static JSON or XML files. Class attributes could be considered as metadata, whereas instance attributes as data. Templates and functions could use both for rendering, e.g. render select or radio group based on a metadata attribute and populate it with items using a data attribute. This approach allowed to customize common (global) classes with region/LOB-specific metadata. From the developer perspective there were no difference between data and metadata - the difference was internal - scope (class or instance) and source of data.
    * QUnit test suite.
* **Collaborative Decision Making** - implemented an intranet web application for collaborative decision making with [AHP](https://en.wikipedia.org/wiki/Analytic_hierarchy_process). The application was intended to be used to support product selection. The application model had two logical parts: 1) Domain/product/feature model allowed to organize software products into domains and associate features with products. 2) Evaluation model contained alternatives, criteria hierarchy and experts. Alternatives and criteria could be initialized from domain products and features or entered manually by the evaluation owner. Different experts could be assigned to different branches of criteria hierarchy. Experts' level of expertise in a given criteria group could be assigned by the evaluation owner - either using pre-defined values (Hi, Med, Low) or using pairwise comparisons of experts. Experts evaluated alternatives using pairwise comparisons. From the comparisons the application computed ranking of alternatives, consistency for the evaluation in general and for each expert, progress - percentage of completed comparisons, and confidence level - weighed percentage of completed comparisons. The application used [CDO](https://wiki.eclipse.org/CDO) repository to store the model and an Equinox/OSGi application with bundled Jetty as a server.

* **Model-Based Development** - demonstrated opportunities to improve development productivity with modeling technologies such as [EMF](https://www.eclipse.org/modeling/emf/), [GMF](https://www.eclipse.org/modeling/gmp/), [Sirius](https://www.eclipse.org/sirius/), CDO. In particular:
    * EMF banking model (Bank, Customer, Account, Transaction) with custom EMF resources facading back-end systems and transparent lazy loading of data using EMF proxies.
    * Application of [Equinox P2](https://www.eclipse.org/equinox/p2/) concepts extended with a notion of capacity for safe and efficient transactional deployment of multi-component systems to runtime environments.
* **RTC Adoption** - Championed adoption of RTC by the R&D team.
* **Collaborative UML Modeling** - Set up a process and infrastructure for collaborative UML modeling with [Sparx Enterprise Architect](http://www.sparxsystems.com/) and subversion for the model repository. Defined repository structure. Prepared detailed documentation explaining all steps in collaborative modeling from set up to visual model merging. Provided coaching and support for modeling teams. Participated in POC's demonstrating model interchange between Enterprise Architect, [TIBCO BPM](http://www.tibco.com/products/automation/business-process-management), and [Blueprint](http://www.blueprintsys.com/solution/).
* **TIBCO BPM POC** - Participated in a POC which leveraged TIBCO BPM. Installed and configured BPM server and prerequisites (LDAP, Oracle) into a cloud virtual machine. Created a process which interacted with [TIBCO BW](http://www.tibco.com/products/automation/application-integration/activematrix-businessworks) services. Knowledge transfer and coaching of the development team.
* **R&D infrastructure** - Set up and maintained infrastructure for the R&D team which consisted of virtual machines, high capacity workstation for storing large binary artifacts including video tutorials, a Wiki site, and some other applications.
* **Distributed Cache Evaluation** - Participated in a distributed cache evaluation, wrote a test harness and tests which we used to compare different distributed caching solutions. The harness and tests served the role of a [Technology Compatibility Kit](https://en.wikipedia.org/wiki/Technology_Compatibility_Kit).
* **Cloud console** - a web application which used REST API's to retrieve information about different objects in the private cloud and generate recommendation using custom rules, e.g. reduce or increase memory or CPU.

#### Shared Technology Services

Focused on integration components using [JMS](https://www.oracle.com/java/technologies/java-message-service.html), [J2EE Connector Architecture](https://www.oracle.com/java/technologies/javaee/j2ee-connector-architecture.html), [Tibco EMS](https://www.tibco.com/products/tibco-enterprise-message-service) and [Tibco BW](https://www.tibco.com/products/tibco-businessworks).

#### Sawgrass Integration Architect

Sawgrass is a Citi Cards call center application.
I was responsible for the architecture of the middleware components which included:

* WebSphere J2EE resource adapter sending and receiving messages to ESB. The connector functionality included:
    * Marshalling/unmarshalling between XML and a Java Object Model 
    * Caching
    * JMS connection pooling, load balancing, liveness checks and recovery
* Tibco BW layer
* Mainframe communication component. The component functionality included translation between XML and a binary format, caching with complex invalidation policies, querying of mainframe responses to return a smaller data set. Querying included pagination support.
* XML-Binary codec library generated from XML files which in turn were generated from mainframe metadata. 
 
 In parallel with the primary responsibilities I also participated in the following efforts:
 
 * Telephony integration applet.
 * Established an automated code review process for Java code with custom inspectors (validation rules) performing deep analysis of code such as navigating call trees. The inspectors were specific to the application framework we used.
 * Implemented automated quality inspection of Tibco BW and Chordiant flows.
 * Implemented an SOA utility performing custom WSDL validation, cleanup and transformations.
 * Implemented a resilient JMS driver for fault tolerance.

Technologies used: 

* Tibco EMS
* Tibco BW
* J2EE Resource adapters
* Berkeley DB
* IBM MQ

### iGate Global Solutions

_Technical Architect, 2000 - 2005_

* Integrated automated code review system with the automated build process. This solution enabled automated quality checks of source code delivered by offshore contractors.
* Implemented automated build application and process, resulting in 2 U.S. patents and generating savings through a personnel reduction , fewer production outages and shorter release cycle. 
* Implemented a number of middleware components.  

### Bank of Moscow

_Head of IT Department, 1999 - 2000_

Managed 4 IT professionals who supported the branch’s computer park (70 desktops and 4 servers), network and telecommunications. Supported/administered hosted applications and developed custom applications and modules. 

  * Set up the branch IT infrastructure from scratch.
  * Developed an electronic payments broker that enabled bank’s operations.
  * Implemented VoIP with the central office, creating significant savings in phone bills. 
  * Managed Y2K compliance and certification.
  * Implemented bank’s mail system with Microsoft Exchange server and Microsoft Outlook and connected system with the central office Exchange Network to improve communications and saving on phone calls.

### Incombank

_Senior Specialist, 1996 - 1999_

Managed telecommunications, electronic fund transfer systems and development of branch-specific software. 
  * Developed a number of automated solutions to reduce payment handling time and processing cost, and increase robustness of payment processing. 
  * Implemented a business intelligence solution that helped marketing department to concentrate efforts on acquiring most significant clients.  
  * Participated in implementation of the first payment card system in Khabarovsk (Golden Crown)

### Procyon

_Software Developer, 1993 - 1995_

FoxPro 2.6 development.

## Education 

[Novosibirsk State University](https://en.wikipedia.org/wiki/Novosibirsk_State_University) - Master of Science in [Plasma Physics](https://research.nsu.ru/en/organisations/%D0%BA%D0%B0%D1%84%D0%B5%D0%B4%D1%80%D0%B0-%D1%84%D0%B8%D0%B7%D0%B8%D0%BA%D0%B8-%D0%BF%D0%BB%D0%B0%D0%B7%D0%BC%D1%8B-%D1%84%D1%84),  1988 - 1993

## Certifications

* [AWS Certified Solutions Architect - Associate](https://www.credly.com/badges/bbfc0c20-d5ff-4df8-bc0f-f7fd52bba347)
* J2EE Architect - Sun Microsystems
* Java Developer - Sun Microsystems
* Java Programmer - Sun Microsystems
* TIBCO Trained Professional

## Patents

* Methods and systems for deploying computer source code
    * [Patent 1](https://patents.google.com/patent/US20050044531)
    * [Patent 2](https://patents.google.com/patent/US20050015762A1)

---

   
   
<html>   
<script async src="https://www.googletagmanager.com/gtag/js?id=G-1584WH6CVM"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-1584WH6CVM');
</script>    
    
</html>    