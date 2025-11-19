# ${groupId}:{artifactId} extension for WildFly

This project was created from the archetype "wildfly-extension-archetype".

It is composed of 3 Maven modules:

* ${artifactId}-extension
  * it contains the Java code that is installed in WildFly to add the extension and its subsystems.
* ${artifactId}-feature-pack
  * it creates a Feature Pack to provision the extension and install it in a WildFly installation
* ${artifactId—-testsuite
  * it provisions a WildFly installation with the feature pack and test that its features are working as expected

# Build the project

Execute the command:

```
mvn install
```

# Extension documentation

The documentation that describe the feature pack, its layers and the subsystem it provides is generated when the feature 
pack is built at ${artifactId}-feature-pack/target/${artifactId}-feature-pack-${version}-doc.zip)

# Run the WildFly server

Once the project has been built, you can run a WildFly server with the extension installed by executing the command:

```
./${artifactId}-testsuite/target/server/bin/standalone.sh
```

# Use this extension in your own server

To install this extension in your own server, you must provision its feature pack as shown in the tracker-testsuite/pom.xml:

```
            <plugin>
                <groupId>org.wildfly.plugins</groupId>
                <artifactId>wildfly-maven-plugin</artifactId>
                <configuration>
                    <feature-packs>
                        <feature-pack>
                            <groupId>org.wildfly</groupId>
                            <artifactId>wildfly-galleon-pack</artifactId>
                            <version>${version.wildfly}</version>
                        </feature-pack>
                        <feature-pack>
                            <groupId>${groupId}</groupId>
                            <artifactId>${artifactId}-feature-pack</artifactId>
                            <version>${version}</version>
                        </feature-pack>
                    </feature-packs>
                    <layers>
                        <!-- layer provided by the feature pack -->
                        <layer>${artifactId}</layer>
                        <!-- and other layers that are required to run your applications -->
                    </layers>
                </configuration>
            </plugin>
```

