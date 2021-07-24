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


