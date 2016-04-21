# Full Examples #

## Matryoshka ##
The Matryoshka ontology just contains one class Matryoshka which has some data properties (Color and Size) asserted and an object property Data "contains" and the reverse for it "contained\_in", as those little Puppets can be put into each other.

### Interface Matryoshka ###
```java

package com.yoshtec.owl.testclasses.matryoshka;

import com.yoshtec.owl.annotations.OwlClass;

@OwlClass(uri="http://www.yoshtec.com/ontology/test/matryoshka#Matryoshka")
public interface Matryoshka {

public String getColor();

public void setColor(String color);

public Integer getSize();

public void setSize(Integer size);

public Matryoshka getContained_in();

public void setContained_in(Matryoshka contained_in);

public Matryoshka getContains();

public void setContains(Matryoshka contains);
}
```

### Data Class MatryoshkaImpl ###
```java

package com.yoshtec.owl.testclasses.matryoshka;

import com.yoshtec.owl.annotations.OwlDataProperty;
import com.yoshtec.owl.annotations.OwlDataType;
import com.yoshtec.owl.annotations.OwlIndividualId;
import com.yoshtec.owl.annotations.OwlObjectProperty;
import com.yoshtec.owl.annotations.oprop.OwlInverseObjectProperty;

public class MatryoshkaImpl implements Matryoshka {

@OwlDataProperty(uri="http://www.yoshtec.com/ontology/test/matryoshka#Color")
@OwlDataType(uri="http://www.w3.org/2001/XMLSchema#string")
private String color = null;

@OwlDataProperty(uri="http://www.yoshtec.com/ontology/test/matryoshka#Size")
@OwlDataType(uri="http://www.w3.org/2001/XMLSchema#int")
private Integer size = null;

@OwlObjectProperty(uri="http://www.yoshtec.com/ontology/test/matryoshka#Contained_in")
@OwlDataType(uri="http://www.yoshtec.com/ontology/test/matryoshka#Matryoshka")
private Matryoshka contained_in = null;

@OwlObjectProperty(uri="http://www.yoshtec.com/ontology/test/matryoshka#Contains")
@OwlInverseObjectProperty(inverse="http://www.yoshtec.com/ontology/test/matryoshka#Contains")
@OwlDataType(uri="http://www.yoshtec.com/ontology/test/matryoshka#Matryoshka")
private Matryoshka contains = null;

@OwlIndividualId
private String name = null;

public MatryoshkaImpl(){

}

public MatryoshkaImpl(String name){
this.name = name;
}

public String toString(){
return String.format("Matryoshka %s, %s, %s", name, color, size );
}

// setters and getters implemented
}
```

### Test and Marshall ###
```java

@Test
public void testMarshallerMatryoshka1() throws Exception {
Matryoshka darth = new MatryoshkaImpl("DarthVader");
darth.setColor("Black");
darth.setSize(10);

Matryoshka anakin = new MatryoshkaImpl("AnakinSkywalker");
anakin.setColor("Brown");
anakin.setSize(9);

darth.setContains(anakin);
anakin.setContained_in(darth);

ArrayList<Object> a = new ArrayList<Object>();
a.add(darth);

Marshaller marshaller = new Marshaller();
marshaller.marshal( a , URI.create("MatryoshkaInds.owl"), (new File("otest/MatryoshkaInds1.owl")).toURI());

}
```

### Output ###

```xml

<?xml version="1.0"?>


<!DOCTYPE rdf:RDF [
<!ENTITY owl "http://www.w3.org/2002/07/owl#" >
<!ENTITY owl2 "http://www.w3.org/2006/12/owl2#" >
<!ENTITY xsd "http://www.w3.org/2001/XMLSchema#" >
<!ENTITY owl2xml "http://www.w3.org/2006/12/owl2-xml#" >
<!ENTITY rdfs "http://www.w3.org/2000/01/rdf-schema#" >
<!ENTITY rdf "http://www.w3.org/1999/02/22-rdf-syntax-ns#" >
<!ENTITY matryoshka "http://www.yoshtec.com/ontology/test/matryoshka#" >
]>


<rdf:RDF xmlns="MatryoshkaInds.owl#"
xml:base="MatryoshkaInds.owl"
xmlns:matryoshka="http://www.yoshtec.com/ontology/test/matryoshka#"
xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
xmlns:owl="http://www.w3.org/2002/07/owl#"
xmlns:owl2xml="http://www.w3.org/2006/12/owl2-xml#"
xmlns:xsd="http://www.w3.org/2001/XMLSchema#"
xmlns:owl2="http://www.w3.org/2006/12/owl2#"
xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#">
<owl:Ontology rdf:about="">
<owl:imports rdf:resource="http://www.yoshtec.com/ontology/test/matryoshka"/>


Unknown end tag for &lt;/Ontology&gt;



<!-- http://www.yoshtec.com/ontology/test/matryoshka#Contained_in -->

<owl:ObjectProperty rdf:about="&matryoshka;Contained_in"/>

<!-- http://www.yoshtec.com/ontology/test/matryoshka#Contains -->

<owl:ObjectProperty rdf:about="&matryoshka;Contains"/>

<!-- http://www.yoshtec.com/ontology/test/matryoshka#Color -->

<owl:DatatypeProperty rdf:about="&matryoshka;Color"/>

<!-- http://www.yoshtec.com/ontology/test/matryoshka#Size -->

<owl:DatatypeProperty rdf:about="&matryoshka;Size"/>

<!-- http://www.yoshtec.com/ontology/test/matryoshka#Matryoshka -->

<owl:Class rdf:about="&matryoshka;Matryoshka"/>

<!-- #AnakinSkywalker -->

<matryoshka:Matryoshka rdf:about="#AnakinSkywalker">
<matryoshka:Size rdf:datatype="&xsd;int">9

Unknown end tag for &lt;/Size&gt;


<matryoshka:Color rdf:datatype="&xsd;string">Brown

Unknown end tag for &lt;/Color&gt;


<matryoshka:Contained_in rdf:resource="#DarthVader"/>


Unknown end tag for &lt;/Matryoshka&gt;



<!-- #DarthVader -->

<matryoshka:Matryoshka rdf:about="#DarthVader">
<matryoshka:Size rdf:datatype="&xsd;int">10

Unknown end tag for &lt;/Size&gt;


<matryoshka:Color rdf:datatype="&xsd;string">Black

Unknown end tag for &lt;/Color&gt;


<matryoshka:Contains rdf:resource="#AnakinSkywalker"/>


Unknown end tag for &lt;/Matryoshka&gt;




Unknown end tag for &lt;/RDF&gt;



```