As JAOB is inspired mainly by JAXB it uses Annotations to map Java objects to OWL Individuals.




# Annotate Java Beans #

## Classes ##

A Java Class or Interface can be mapped to a OWL Class via the `@OwlClass` Annotation:

```java

@OwlClass(uri="http://MyOntoUri#MyClass")
public class MyClass{
//...
}
```

## Properties ##
A Data Property can be mapped to a class variable (later should be possible via setter getter pairs two):

```java

@OwlClass(uri="http://MyOntoUri#MyClass")
public class MyClass{

@OwlDataProperty(uri="http://MyOntoUri#MyNameProp")
@OwlFunctionalDataProperty
@OwlDatatype(uri="http://www.w3.org/2001/XMLSchema#string")
private String name = null;
//...
}
```

By Using the data type annotation the marshaller knows how to set the the value in the ontology. It is currently not possible to use more than one datatype for data properties.

You can also use lists or collections in general for Properties:

```java

@OwlClass(uri="http://MyOntoUri#MyClass")
public class MyClass{

@OwlDataProperty(uri="http://MyOntoUri#MyNickNameProp")
@OwlDatatype(uri="http://www.w3.org/2001/XMLSchema#string")
private List<String> nicknames = null;
//...
}
```

The same holds for Object Properties:

```java

@OwlClass(uri="http://MyOntoUri#MyClass")
public class MyClass{

@OwlObjectProperty(uri="http://MyOntoUri#MyObjectProp")
@OwlDatatype(uri="http://MyOntoUri#MyClass")
private List<MyClass> classes = null;
//...
}
```

A special case is the name of the Individual, usually in an RDF representation of an OWL `rdf:about` or `rdf:ID` which can be handled as well:

```java

@OwlClass(uri="http://MyOntoUri#MyClass")
public class MyClass{

@OwlIndividualId
private String name = null;
//...
}
```

# Marshalling an Unmarshalling #
Marshalling can be done through the marshaller:

```java

Marshaller marshaller = new Marshaller();
marshaller.marshal(
objectscollection ,
URI.create("MyOntology.owl"),
(new File("MyOntology.owl")).toURI());
```

Unmarshalling works the other way around:

```java


UnMarshaller unmarshaller = new UnMarshaller();

// need to register the classes that shall be instantiated before:
un.registerClass(MatryoshkaImpl.class);

Collection<Object> objects = unmarshaller.unmarshal(
URI.create("MyOntology.owl"),
(new File("MyOntology.owl")).toURI());

```

The registering of classes has the advantage, that you can create a complex Ontology, then run the code generator get a bunch of classes out of it, and then you could create a subclass of an generated class which then shall be instantiated instead of the original generated code (this could not be done with jaxb for instance). All you have to do for it is `implement` an Interface that is annotated with the `@OwlClass` annotation or subclass a class with this annotation.

# Code Generation #

```java

Codegen codegen = new Codegen();

// the java package to create the classes in
codegen.setJavaPackageName("matryoshkatest");

// Ontology loading parameters
codegen.setOntologyUri("http://www.yoshtec.com/ontology/test/matryoshka");
codegen.setOntologyPhysicalUri( new File("test/matryoshka.owl").toURI().toString());

// where to write the source to
codegen.setJavaSourceFolder(new File("otest"));

// will generate "indName" String fields with @OwlIndividualId annotation and implementations
codegen.setGenerateIdField(true);
codegen.setIdFieldName("indName");

// generate code
codegen.genCode();
```