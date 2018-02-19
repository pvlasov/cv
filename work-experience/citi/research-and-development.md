# Research & Development

**Work in Progress**


### Tag Management Solution Selection
Participated in a tag management solution selection effort. Evaluated several leading tag management solutions. Created a test harness for comparing difference in web pages performance before and after deployment of the tag management solution. The harness used Selenium Web Driver to load pages in different browsers, [[https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html|Navigation Timing API]] to collect page load timings, and an OSGi/Equinox container with CDO/H2 model repository to store collected data, and Jetty to display stats (min, max, avg, deviation) and charts (using [[http://www.flotcharts.org/|Flot]]).

### Functional/Acceptance Testing Automation 

#### Web Applications
  * Established a process for automated functional testing of Web applications with [[http://docs.seleniumhq.org/projects/webdriver/|Selenium WebDriver]], [[http://junit.org/|JUnit]], and [[http://jenkins-ci.org/|Jenkins]]. 
  * Created JUnit-[[http://www8.hp.com/us/en/software-solutions/quality-center-quality-management/|HP Quality Center]] integration using annotations and Quality Center RESTful API's. 
  * Demonstrated execution of tests in different browsers on different operating systems with Jenkins multi-configuration (matrix) builds and with [[https://code.google.com/p/selenium/wiki/Grid2|Selenium Grid]].
  * Demonstrated different approaches to testing and reporting with plain JUnit, [[http://jbehave.org/|JBehave Web]], [[http://www.thucydides.info/|Thucydides]], and [[https://github.com/Nasdanika/server/wiki/webtest|Nasdanika WebTest]].

#### Mobile Applications
Demonstrated an approach to automating functional tests of Android applications in emulators and on real devices with [[http://selendroid.io/|Selendroid]], [[http://appium.io/|Appium]], and Selenium Grid.

### Continuous Delivery & Continuous Inspection 
  * Set up an environment and process for the R&D team to build and deploy Java libraries, J2EE Web applications and TIBCO Business Works processes with Jenkins [[http://maven.apache.org/|Maven]] builds, [[http://www.sonatype.org/nexus/|Sonatype Nexus OSS]], and SonarQube. Jenkins pulls sources from [[https://subversion.apache.org/|Subversion]] and [[https://jazz.net/products/rational-team-concert/|Rational Team Concert]]. 
  * Migrated several existing projects from Ant to Maven.
  * Set up a Continuous Delivery Wiki site with cookbooks and links to the tools and additional information.

### JavaScript API's
Demonstrated how banking domain model can be exposed as JavaScript API in accordance with Web-Oriented Architecture principles. JavaScript was generated from a model because hand-crafting would be labor-intensive and error-prone. The model was created in [[https://www.eclipse.org/modeling/emf/|Eclipse Modeling Framework (EMF)]] and populated either by importing XML schemas or manually using an EMF-generated editor. Generated JavaScript was used either in the browser or on [[http://nodejs.org/|Node.js]] and could retrieve server/back-end data in XML and JSON formats over HTTP and [[wp>WebSocket]]. Measured and compared network traffic using the new approach vs. current, which showed significant reduction. 

An overview of principles and technologies:
  * The API was organized into namespaces containing classes which in turn contained attributes and functions.
  * Multiple inheritance.
  * The model supported templates in [[http://olado.github.io/doT/index.html|doT.js]] which were compiled to JavaScript at generation time.
  * Templates could be parameterized or parameterless. Parameterless templates were generated as read-only properties, e.g. ''Customer.home'' would render customer home page. Parameterized templates were generated as functions.
  * Multi-resource (multi-file) models, e.g. global/core class definitions in one model resource or a set of resources and LOB/region specific definition another.
  * Lazy (on-demand) loading of classes, data (attributes), and functions/templates. 
  * Attributes were mapped to service calls. Once service call could retrieve multiple attributes and one attribute could be retrieved by multiple services. Conceptually services were overlapping fetch groups. 
  * Attributes could have validations associated with them.
  * Classes were loaded on demand in the browser with [[http://requirejs.org/|RequireJS]].
  * Functions/templates could be marked to be loaded on demand in the model - this feature was useful for network traffic optimization in case of large infrequently used templates.
  * Getters/setters were used to abstract API users from on-demand loading/partial population.
  * Synchronous and asynchronous modes - same API with asynchronous mode loading returning [[https://github.com/kriskowal/q|Q]] promises instead of data values.
  * Syntax highlighting editors for functions, services and templates code.
  * [[http://backbonejs.org/|Backbone.js]]-based single-page application.
  * A thin messaging layer over WebSocket emulating JMS request/reply API.
  * Node.js application was built with [[http://expressjs.com/|Express]], [[https://github.com/senchalabs/connect#readme|Connect]], and [[http://visionmedia.github.io/superagent/|SuperAgent]].
  * Computed attributes.
  * Metadata management - classes could have instance and class attributes and functions. Attributes could have default values. Class attributes, as well as instance attributes, could be loaded from services, which in case of class attributes could be static JSON or XML files. Class attributes could be considered as metadata, whereas instance attributes as data. Templates and functions could use both for rendering, e.g. render select or radio group based on a metadata attribute and populate it with items using a data attribute. This approach allowed to customize common (global) classes with region/LOB-specific metadata. From the developer perspective there were no difference between data and metadata - the difference was internal - scope (class or instance) and source of data.
  * QUnit test suite.

### Collaborative Decision Making
Implemented an intranet web application for collaborative decision making with [[wp>Analytic_hierarchy_process|AHP]]. The application was intended to be used to support product selection. The application model had two logical parts:
  * Domain/product/feature model allowed to organize software products into domains and associate features with products.
  * Evaluation model contained alternatives, criteria hierarchy and experts. 

Alternatives and criteria could be initialized from domain products and features or entered manually by the evaluation owner. Different experts could be assigned to different branches of criteria hierarchy. Experts' level of expertise in a given criteria group could be assigned by the evaluation owner - either using pre-defined values (Hi, Med, Low) or using pairwise comparisons of experts.

Experts evaluated alternatives using pairwise comparisons. From the comparisons the application computed ranking of alternatives, consistency for the evaluation in general and for each expert, progress - percentage of completed comparisons, and confidence level - weighed percentage of completed comparisons.

The application used [[https://wiki.eclipse.org/CDO|CDO]] repository to store the model and an Equinox/OSGi application with bundled Jetty as a server.

### Model-Based Development
Demonstrated opportunities to improve development productivity with modeling technologies such as:
  * [[https://www.eclipse.org/modeling/emf/|EMF]]
  * [[https://www.eclipse.org/modeling/gmp/|GMF]]
  * [[https://www.eclipse.org/sirius/|Sirius]]
  * CDO

In particular:
  * EMF banking model (Bank, Customer, Account, Transaction) with custom EMF resources facading back-end systems and transparent lazy loading of data using EMF proxies.
  * Application of [[https://www.eclipse.org/equinox/p2/|Equinox P2]] concepts extended with a notion of capacity for safe and efficient transactional deployment of multi-component systems to runtime environments.

#### RTC Adoption
Championed adoption of RTC by the R&D team.

#### Collaborative UML Modeling
Set up a process and infrastructure for collaborative UML modeling with [[http://www.sparxsystems.com/|Sparx Enterprise Architect]] and subversion for the model repository. Defined repository structure. 

Prepared detailed documentation explaining all steps in collaborative modeling from set up to visual model merging. 

Provided coaching and support for modeling teams.

Participated in POC's demonstrating model interchange between Enterprise Architect, [[http://www.tibco.com/products/automation/business-process-management|TIBCO BPM]], and [[http://www.blueprintsys.com/solution/|Blueprint]].

#### TIBCO BPM POC
Participated in a POC which leveraged TIBCO BPM. 
  * Installed and configured BPM server and prerequisites (LDAP, Oracle) into a cloud virtual machine. Created a process which interacted with [[http://www.tibco.com/products/automation/application-integration/activematrix-businessworks|TIBCO BW]] services. 
  * Knowledge transfer and coaching of the development team.

#### R&D infrastructure 
Set up and maintained infrastructure for the R&D team which consisted of virtual machines, high capacity workstation for storing large binary artifacts including video tutorials, a Wiki site, and some other applications.

#### Distributed Cache Evaluation 
Participated in a distributed cache evaluation, wrote a test harness and tests which we used to compare different distributed caching solutions. The harness and tests served the role of [[wp>Technology_Compatibility_Kit|TCK]].
