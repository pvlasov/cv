# Cloud & Integration Services

Product owner of Citi Nexus Platform Cloud & Integration Services domain.

July 2017 - Present.

In July 2017 I assumed the role of the product owner of the Cloud & Integration Services team. The team owns more than 30 software platform components used by application development teams. 
The components owned by the team are organized into four "pillars":

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

When I became a product owner the previous product owner moved to another position within Citi taking the most of the team with them. The remaining 3 people had been with the team for a few months and
one of them eventually left the team. People to joined our team were totally new to Citi. So the new team of 8 developers plus the product owner and the scrum master had to quickly get a grasp of what we came to own. We achieved it by "dividing and conquering" - each component was assigned a primary and a secondary owner. The owners created and deployed to the Citi intranet Maven sites for components they own.
The sites feature component overview, Java API documentation, roadmap and changelog pages. 
Microservice sites also feature generated REST API documentation.

We've also created and deployed a Maven team site for the team which lists components grouped in categories (pillars) and sub-categories. Component listings provide links to the component sites. 
All the sites have the same style. The breadcrumbs of the team site and the component sites provide a uniform experience of main site/child site.   

In this role I wear two hats - the product owner and a dev lead of the Productivity pillar. I work with the team "customers" to understand their needs. 
From that I build roadmaps which then get elaborated into features and stories in the team backlog. Before a start of a new sprint stories are prioritized and assigned to the team members with capacity and skillset in mind. 