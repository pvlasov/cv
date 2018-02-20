# Application Modernization

September 2016 - June 2017

In September 2016 I left the R&D team to become a lead of the Application Modernization domain of the Citi Nexus Platform. 
The focus of the team was to provide solutions for conversion of monolithic applications into micro-services. 

One of the monoliths which we worked with was a Java Web Application project with:

* 14 thousand Java classes organized into a thousand of packages. 
* 2.5 million lines of code.
* ~180 thousands methods and ~75 thousands fields. 
* ~80% of code resided in packages with circular dependencies which made it very difficult to modularize the application.
* About two hundred thousand of non-Java assets such as images, JavaScript files, configuration files, JSP's.

The above metrics do not include dependencies, just the application per se. 

First we started with [Sonargraph-Explorer](https://www.hello2morrow.com/products/sonargraph/explorer) to get a feeling of what we were facing. 
Sonagraph is a very nice tool but because of the huge number of classes involved in the circular dependency "black hole" we needed a more advanced tooling.

First we created an [Ecore](https://www.eclipse.org/modeling/emf/)/[CDO](https://wiki.eclipse.org/CDO) model of the Java language which included not only declarative things as in the ``java.lang.reflect`` package, but also call trees, field references and bi-directional inheritance references. 
After that we created a model loader which leveraged [ASM](http://asm.ow2.org/) to walk through the bytecode and populate the model.

Once we had the model and the loader we created a model-driven web application to browse loaded models in order to get better understanding of the codebase - "Analysis repository". 
The application used [PlantUML](plantuml.com) to visualize the model via class context diagrams and method sequence diagrams.
After we loaded several modules the application repository had about 2 million objects - packages, classes, methods, fields. The performance was not lightning fast, but acceptable and the repository database was about 250 megabytes.    

Using ASM we also created a code instrumentation tool which would take a jar file and data collection endpoint URL as input and output a jar with bytecode instrumented to report call trees to the endpoint. We've also added a data collection endpoint to the Analysis repository.   
Collection of runtime call tree information was intended to complement static analysis by recording reflective calls.

The next step for us was creation of an Eclipse plug-in for module extraction. Given a number of entry points (classes, methods) the plug-in was able to extract a sub-set of the source project codebase traceable from the entry points. In classes the plug-in would only extract class members traceable from the entry points. E.g. if a class had a hundred members but only ten of them were traceable from the sources the plug-in would extract only those ten. 

The plug-in used the loader module and [Eclipse JDT](https://www.eclipse.org/jdt/) to analyze source code and JDT refactoring capabilities to extract the code into a new module.

The plug-in was implemented as a multi-form editor with one page/form presenting a source checkbox tree allowing the user to select entry points. Other pages/forms collected additional extraction parameters. 
Module extraction configuration was stored in JSON with transparent loading to an EMF model and saving the EMF model to JSON. The editor used [EMF Data Bindings](http://www.vogella.com/tutorials/EclipseDataBindingEMF/article.html) with TransactionalEditingDomain to support Undo/Redo of complex model manipulations.
        