# Role of Annotations in Java - Part3

## Annotation Processing

When Java source code is compiled, annotations can be processed by compiler plug-ins called **Annotation Processors**.
Processors can produce informational messages or create additional Java source files or resources, which in turn may be
compiled and processed. However, annotation processors cannot modify the annotated code itself. 

The Java compiler conditionally stores annotation metadata in the class files, if the annotation has a  ```RetentionPolicy```
of ```#CLASS#``` or ```#RUNTIME#```. Later, the JVM or other programs can look for the metadata to determine how to interact with the program elements or change
their behavior.

In addition to processing an annotation using an annotation processor, a Java programmer can write their own code that uses reflections to process the annotation. Java SE5 supports a new interface that is defined in the ```java.lang.reflect``` package. This package contains the interface called ```AnnotatedElement``` that is implemented by the Java reflection classes including ```Class```, ```Constructor```, ```Field```, ```Method```, and ```Package```. The implementations of this interface are used to represent an annotated element of the program currently running in the Java Virtual Machine. This interface allows annotations to be read reflectively.

The ```AnnotatedElement``` interface provides access to annotations having ```RUNTIME``` retention. This access is provided by the ```getAnnotation```, ```getAnnotations```, and ```isAnnotationPresent``` methods. Because annotation types are compiled and stored in byte code files just like classes, the annotations returned by these methods can be queried just like any regular Java object. A complete example of processing an annotation is provided below:

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

// This is the annotation to be processed
// Default for Target is all Java Elements
// Change retention policy to RUNTIME (default is CLASS)
@Retention(RetentionPolicy.RUNTIME)
public @interface TypeHeader {
    // Default value specified for developer attribute
    String developer() default "Unknown";
    String lastModified();
    String [] teamMembers();
    int meaningOfLife();
}

```
```java
// This is the annotation being applied to a class
@TypeHeader(developer = "Mahendra Rao",
    lastModified = "2014-04-14",
    teamMembers = { "Sravan", "Sudheer", "PuneethSai" },
    meaningOfLife = 82)

public class SetCustomAnnotation {
    // Class contents go here
}
```
```java
// This is the example code that processes the annotation
import java.lang.annotation.Annotation;
import java.lang.reflect.AnnotatedElement;

public class UseCustomAnnotation {
    public static void main(String [] args) {
        Class<SetCustomAnnotation> classObject = SetCustomAnnotation.class;
        readAnnotation(classObject);
    }

    static void readAnnotation(AnnotatedElement element) {
        try {
            System.out.println("Annotation element values: \n");
            if (element.isAnnotationPresent(TypeHeader.class)) {
                // getAnnotation returns Annotation type
                Annotation singleAnnotation = 
                        element.getAnnotation(TypeHeader.class);
                TypeHeader header = (TypeHeader) singleAnnotation;

                System.out.println("Developer: " + header.developer());
                System.out.println("Last Modified: " + header.lastModified());

                // teamMembers returned as String []
                System.out.print("Team members: ");
                for (String member : header.teamMembers())
                    System.out.print(member + ", ");
                System.out.print("\n");

                System.out.println("Meaning of Life: "+ header.meaningOfLife());
            }
        } catch (Exception exception) {
            exception.printStackTrace();
        }
    }
}

```

*Conclusion*

Finally, Applications had to define their meta-data in some configuration files and usually these meta-data were externalized from the Application. Now, they can directly define this meta-data information in the source code. The concept of Annotating elements in Java is gaining much popularity because of its robustness and simplicity of usage. When effectively applied on Java elements, Annotations can be of great use.

