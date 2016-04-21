## OWL Concepts understood by JAOB ##
  * Classes
    * owl:Thing
    * Named Classes
    * ObjectUnionOf
  * Properties (Data and Object)
    * Functional Properties
    * Inverse (only during code generation)
  * Individuals for marshalling and unmarshalling
  * Annotations:
    * Comments
    * Labels
  * Imports

## OWL Concepts not understood and not currently handled ##
  * Classes
    * ClassIntersectionOf
    * Individuals as Class operators (ObjectOneOf)
  * Sub Properties (Data and Object) which means they are currently treated  as normal Properties without any special relation
  * Annotations
    * Individuals
    * etc.
  * Individuals as constants
  * Everything else not specifically mentioned in in the understood section ;)