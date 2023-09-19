# Introduction

This project provides connectors for Kafka Connect to read and write data to HttpSinkConnector.

# Documentation

Documentation on the connector is hosted on Confluent's
[docs site](https://docs.confluent.io/current/connect/kafka-connect-http/).

Source code is located in Confluent's
[docs repo](https://github.com/confluentinc/docs/tree/master/connect/kafka-connect-http). If changes
are made to configuration options for the connector, be sure to generate the RST docs (as described
below) and open a PR against the docs repo to publish those changes!

# Configs

Documentation on the configurations for each connector can be automatically generated via Maven.

To generate documentation for the sink connector:
```bash
mvn -Pdocs exec:java@sink-config-docs
```

To generate documentation for the source connector:
```bash
mvn -Pdocs exec:java@source-config-docs
```

# Development

## Builds

This project uses the normal Maven build lifecycle, and can be built
locally with

```bash
$ mvn clean install
```

The Jenkins builds run a few more checks via the `jenkins` profile:

```bash
$ mvn clean install -Pjenkins
```

## File Headers

### Generating headers

License headers can be automatically added and updated for files in the project:
```bash
mvn license:format
```

### Updating copyright years

Alternatively, if you've added a header that appears correct but are still getting this error, it's
possible the end date on the header format needs to be updated. You can do this by adjusting the
`${license.current.year}` property in the project's POM:

```xml
<project>
    <properties>
        <license.current.year>4761</license.current.year>
    </properties>
</project>
```

Or, if you're getting an error message despite not having altered any files, it's possible that the
start date on the header format needs to be updated to match the year the project was started. You
can do this by adjusting the `${license.first.year}` property in the project's POM:

```xml
<project>
    <properties>
        <license.first.year>2017</license.first.year>
    </properties>
</project>
```

By default, the value of the `${license.first.year}` property will match the value of the
`${project.inceptionYear}` property.

**NOTE**: The copyright header format must be identical for all files in a given module. This means
that if the inception year for the project is 2017 but a file is added in 2018, the copyright header
for the new file will still have to read "Copyright 2017 - 2018" (or something similar).

### Excluding files

If a file in your project should be excluded from license header validation, it can be excluded by
altering the project's POM:

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>com.mycila</groupId>
                <artifactId>license-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>some-file</exclude>
                        <exclude>some-directory/*</exclude>
                        <exclude>**/passwd</exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

Note that directories and shell glob patterns may also be excluded.

## License and Notice files

Some boilerplate has already been added to the common POM that enables license and notice files to
be automatically generated.

When dependencies change, make sure there is an existing a `licenses/`
directory in the root of your project:

```bash
$ mkdir -p licenses
```

Then, run the following command to automatically update the `licenses/`
directory with a file denoting the open source license and notice files 
for each of the dependencies:

```bash
$ mvn install -DskipTests -Plicense-sources
```

Commit any changes to the Git repository.

# Compatibility Matrix:

This connector has been tested against the following versions of Apache Kafka
and HttpSinkConnector:

|                          | AK 1.0             | AK 1.1        | AK 2.0        |
| ------------------------ | ------------------ | ------------- | ------------- |
| **HttpSinkConnector v1.2.3** | NOT COMPATIBLE (1) | OK            | OK            |

1. The connector needs header support in Connect.

# Integration Tests

Integration tests work out of the box for this connector; simply run them without any modifications.
