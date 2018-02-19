# Pavel Vlasov 

![picture](pavel-vlasov.jpg)

E-Mail: ``pavel@vlasov.us``

Linked-In Profile: www.linkedin.com/in/pavelvlasov

GitHub: https://github.com/pvlasov

## Strengths

* Java.
* [Model-Driven Development and Code Generation](model-driven-development/README.md).
* Cloud technologies - Spring Boot, Pivotal Cloud Foundry, AWS, Docker, ...
* Integration.

## Experience

24 years of experience. 

| Company  | Title | Period |
| ------------- | ------------- | ----- |
| [Citi Global Consumer Group](work-experience/citi/README.md) | Senior Vice President | 2005 - Present |
| [iGate Global Solutions](work-experience/igate/README.md) | Technical Architect | 2000 - 2005 |
| [Bank of Moscow](work-experience/bank-of-moscow/README.md) | Manager of IT Department | 1999 - 2000 |
| [Incombank](work-experience/inkombank/README.md) | Senior Specialist | 1996 - 1999 |
| [Procyon](work-experience/procyon/README.md) | Software Developer | 1993 - 1995 |

## Open source contributions

* [Nasdanika](open-source/nasdanika/README.md)
* [Hammurapi](open-source/hammurapi/README.md)

## Education 

Novosibirsk State University - Master of Science in Plasma Physics - 1988 to 1993

## Ideal position

A lead of a team of highly skilled and motivated professionals focusing on closing gaps in internal automation
through creation of organization-specific Eclipse plug-ins, intranet web applications and other tools leveraging model-driven development and code generation. 

Throughout my career I've seen many times over gaps in internal automation which, if closed, would bring significant benefits to the organization. Some organizations recognize
such gaps and proactively close them, while others just talk about them. The problem with the latter kind of organizations is that their problems cannot be efficiently addressed by the tools/solutions
available in the industry because the problems are specific to the organization. E.g. it might be a particular internal data format or a process. At the same time such problems cannot be solved
by the teams which face them because they don't have skills or time to address the problem. In other words, they are so busy hauling buckets of water that they don't have time/skills to build a pipeline.
They might as well be unaware of existing tools/technologies which can help solving their problems because these tools/technologies are not their area of expertise.
Another reason preventing such internal automation might be economies of scale where multiple teams are doing very similar things which can be automated, but even if team members have skills and time 
it doesn't make sense for them to automate something because the cost of automation is more than the benefit. At the same time at the organization level such automation would help multiple teams and result in significant saves.

Examples:

* Automation of the payment entry process in a bank branch. The head office could not address this problem in a branch because the problem was specific to the branch's region and third-parties which the branch had to interact with. Payments had to be entered in 3 different systems manually. It lead to delays in payment processing and human errors. Integration of the systems tripled the capacity of the payments processing department.
* Build automation. It was in pre-Jenkins/early-Maven times. We built a distributed build server with build nodes executing Ant scripts. The Web UI was driving the nodes using RMI. The build system was integrated with an automated code review system and was handling hundreds of builds per day.
* Cloud advisor - an intranet web application inspecting different aspects of Pivotal Cloud Foundry and providing optimization advices, e.g. advising to adjust memory or disk quotas.
* Configuration advisor - an intranet web application inspecting micro-services YAML configuration files for errors and compliance with service configuration "schema". Inspection was done by periodic polling of configuration repositories and as part of the configuration deployment build by leveraging a custom-build Maven plug-in.
* Configuration editor - an Eclipse plug-in which allows for editing micro-service configurations. The editor is aware of configuration elements supported by a particular micro-service, constrains user input to those elements and also provides validations, e.g. it detects duplicate names in Zuul routes and overlapping patterns. Both the editor and Configuration Advisor use the same configuration models and validation rules.  
* Dependency advisor - inspects Maven project dependencies during a build. Reports errors or warnings. E.g. use of an obsolete Tomcat version or absence of a mandatory dependency. The advisor also records dependencies and displays dependency metrics at version, artifact, group and organization level, e.g. how many artifacts produced by team A are used by team B.        

## Certifications

TODO

## Publications

TODO - articles in JavaWorld, online book (work in progress)

## Patent Applications

TODO

