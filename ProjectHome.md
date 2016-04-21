This lib allows you to map Java Objects to OWL (it is similar to JAXB)

Please Look at the Fork at:
https://github.com/okkam-it/jaob


While Testing some Java OWL-APIs for filling data (individuals) into OWL ontologies I figured, that it is quite hard to do so. Especially if you already have a Java object data structure in your project and just want to put out some data. As I worked with JAXB and JPA which make use of annotations, I thought to myself that such kind of binding could be used to save Java objects to ontologies. Here is the solution (in a very early alpha stage) I came up with.

JAOB can achieve the following:

  1. **Reading** and **Writing OWL** Ontologies from Java
    * Marshalling annotated objects to an ontology
    * Unmarshal OWL Ontology Individuals to their corresponding Java objects
  1. **Generate Java code** from an Ontology
    * It will create Interfaces Classes with corresponding annotations for marshalling and unmarshalling.
  1. **Generate an Ontology** from Annotated Java Classes
    * It will create classes and properties from the annotated Java classes. (Currently still has a lot of shortcommings!)

For further info take a look at the [Usage](Usage.md) page.