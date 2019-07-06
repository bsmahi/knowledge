# Role of Annotations in Java - Part2

Java defines built-in annotations which are from java.lang.annotation package:

* **@Retention**:
    
    Specifies how the marked annotation is stored, whether in code only, compiled into the class, or available at runtime         through reflection.

    We have 3 types of Retention policy used or invoked by particular class:
    
    * **RetentionPolicy.SOURCE** - The marked annotation is retained only in the source level and is ignored by the compiler.
       ### Usage
       ```java
       @Retention(RetentionPolicy.SOURCE) // Make this annotation accessible at source code level
       public @interface Sampletest1 {
       } 
       ```
    
    * **RetentionPolicy.CLASS** - The marked annotation is retained by the compiler at compile time, but is ignored at 
                                   run-time by Java Virtual Machine (JVM).
       ### Usage
       ```java
        @Retention(RetentionPolicy.CLASS) // Make this annotation accessible at class level
        public @interface Sampletest2 {
        } 
       ```
    * **RetentionPolicy.RUNTIME** - The marked annotation is retained by the JVM so it can be used by the runtime                                                  environment.
        ### Usage
       ```java
        @Retention(RetentionPolicy.RUNTIME) // Make this annotation accessible at runtime via reflection.
        public @interface Sampletest3 {
        } 
       ```

   * **@Documented**: Marks another annotation for inclusion in the documentation. Annotations are not included by Javadoc                          comments. Use of @Documented annotation in the code enables tools like Javadoc to process it and include                      the annotation type information in the generated document. 
      ### Usage
      ```java
      import java.lang.annotation.Documented;
       /** 
       * Annotation to hold the AppStore Details.
       */
      
      @Documented
      public @interface AppStore {
         
         /* 'company' element is optinal because we provided default constant value. */
         String company() default "Apple"
         
         /* Mandatory elements of AppStore Annotation */
         String storename();
         String date();
         String storedescription();
      }
      
      ```
* **@Target**: 
      
    Marks another annotation to restrict what kind of Java elements the annotation may be applied to. **@Target** takes one       arguement, which must be constant from the **ElementType** enumeration. This argument specifies the type of declarations       to which the annotation can be applied. The constants are shown below along with the type of declaration to which they         correspond.
     
  * **ElementType.ANNOTATION_TYPE** - can be applied to an annotation type.
  * **ElementType.CONSTRUCTOR** - can be applied to a constructor.
  * **ElementType.FIELD** - can be applied to a field or property.
  * **ElementType.LOCAL_VARIABLE** - can be applied to a local variable.
  * **ElementType.METHOD**- can be applied to a method-level annotation.
  * **ElementType.PACKAGE**- can be applied to a package declaration.
  * **ElementType.PARAMETER**- can be applied to the parameters of a method.
  * **ElementType.TYPE**- can be applied to any element of a class
  
  ### Usage
  
  ```java
  imported java.lang.annotation.Target
  imported java.lang.annotation.ElementType
  
  @Target({ElementType.TYPE, ElementType.METHOD, ElementType.CONSTRUCTOR, ElementType.ANNOTATION_TYPE,
           ElementType.PACKAGE, ElementType.FILED, ElementType.LOCAL_VARIABLE})
  public @interface Author {
       ...
  }
  
  ```
  
* **@Inherited**:  




