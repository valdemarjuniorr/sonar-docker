# Sonar Docker

## Description

Start a SonarQube server with a Postgres database to run SonarQube analysis on your projects locally.

## Requirements
- maven
- docker-compose
- At least the minimal version of Java supported by your SonarQube server is in use

## How to start

First clone the project:

```bash
$ git clone git@github.com:valdemarjuniorr/sonar-docker.git
$ cd sonar-docker
```

It's basically just run the following command to start the SonarQube server:

```bash
docker-compose up -d
```

or simply:

```bash
make start
```
You can access the SonarQube server at [http://localhost:9000](http://localhost:9000).

## How to use

There are two ways to run the analysis on your project:

- Editing a [global settings](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-maven/#global-settings) in the settings.xml file, located in `<MAVEN_HOME>/conf` or `~/.m2`, to set the plugin prefix and optionally the SonarQube server URL. For example:

```xml
<settings>
  <pluginGroups>
    <pluginGroup>org.sonarsource.scanner.maven</pluginGroup>
  </pluginGroups>
  <profiles>
    <profile>
      <id>sonar</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <!-- Optional URL to server. Default value is http://localhost:9000 -->
        <sonar.host.url>
          http://myserver:9000
        </sonar.host.url>
      </properties>
    </profile>
  </profiles>
</settings>
```

To [analyze a project](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-maven/#analyzing) consists of running a Maven goal `sonar:sonar` from the directory where the project's POM is located,
but you need to pass an [authentication token](https://docs.sonarsource.com/sonarqube/latest/user-guide/user-account/generating-and-using-tokens/) using one of the following options:

```bash
mvn clean install sonar:sonar -Dsonar.token=myAuthenticationToken
```

## References
- [SonarQube](https://docs.sonarsource.com/sonarqube/latest/)
