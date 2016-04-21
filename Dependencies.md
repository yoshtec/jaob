# Dependencies #

  * Java 6 (or I guess it could be run using Java 1.5 plus JAXB)
  * [OWL-API](http://owlapi.sourceforge.net/) for reading and writing ontologies.
  * [slf4j](http://www.slf4j.org/) Java Simple Logging Facade and an implementation thereof. I use [logback](http://logback.qos.ch/), but log4j could be used as well.
  * [CodeModel](http://codemodel.java.net/) for generating Java code from ontologies, it is not necessary for marshalling and unmarshalling.