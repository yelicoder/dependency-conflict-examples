# Plural Sight Surviving Dependency with Maven

### Example 1
* NoSuchMethodError
* NoSuchFiledError
* NoClassDefFoundError
```
mvn dependency:tree
mvn dependency:tree -Dverbose
mvn dependency:tree -Dverbose|grep guava
mvn dependency:tree -Dverbose -Dincludes=com.google.guava:guava
```
* There can only be ONE version
  * Classpath - First class wins
  * Maven - Nearest dependency wins. The deeper you go to the dependency tree, the less likely it will be picked up
* Use Maven Enforcer
  * Convergence vs Upper bound
  * https://maven.apache.org/enforcer/enforcer-rules/dependencyConvergence.html
  * add maven-enforcer-plugin in pom.xml then run "mvn verify"
  * Upper bound if higher version is backwards compatible. 
    * If convergency or upper bound fails, excluding offending dependencies or use Dependency Management
  * exclusion may have some issues
  * Dependency management force/overwrite all dependency of the same artifact use the same version defined in dependency management
* Newest version doesn't always work! You many need use both old and new versions
  * Eg: System classpath has older version of Guava (Hadoooop!)
  * Shade + Relocation :(

### example-3c
* access to google cloud: export GOOGLE_APPLICATION_CREDENTIALS="/Users/yeli/Documents/data/access/googleCloud/cybernetic-day-320818-9a3ec20570a9.json"

```
mvn dependency:tree -Dverbose -Dincludes=com.google.guava

com.google.guava:guava-jdk5:jar:17.0:compile

same jar file, different artifactId
```
* This is not picked up by the "requireUpperBound"
* use "banDuplicateClasses" https://www.mojohaus.org/extra-enforcer-rules/banDuplicateClasses.html
```
java.lang.NoClassDefFoundError: io/grpc/MethodDescriptor$PrototypeMarshaller
```

### bom file
* Multi-module projects Produce a BOM!
* BOM should not overreach!
* ONLY modules within the multi-project project
* No transitive dependency

### Linkage Checker
https://github.com/GoogleCloudPlatform/cloud-opensource-java/wiki/Linkage-Checker-Enforcer-Rule


