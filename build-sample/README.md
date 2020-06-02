# Alloy Build (DRAFT)

*TODO: move this content to main readme, when completed*

The alloy project builds with Apache Maven, which takes care of:
- Invoking sub-module build systems, like `npm`
- Manage project version lifecycle
- Creating uber JARs
- Run unit and integration testing
- Send testing metrics to https://sonarcloud.io/code?id=org.finos.alloy%3Aalloy-parent
- Deploy snapshot JARs to https://oss.sonatype.org/#nexus-search;quick~org.finos.alloy
- Release Docker image to https://hub.docker.com/u/finos
- Deploy released JARs to Maven Central (TODO)
- Run a release process that invoke all steps above in a transactional fashion (TODO)

## Requisites
1. Please follow https://finosfoundation.atlassian.net/wiki/spaces/FDX/pages/75530342/Continuous+Integration#ContinuousIntegration-Continuous(artifact)deploymentinJava to get credentials for oss.sonatype.org and consequentially Maven Central.
2. Apache Maven 3.x - `mvn -v`
3. JRE 8+ (to confirm)

## Local run

### Build the project and run tests
```
mvn package
```
JAR file is built into `build-sample/server/target/alloy-server-0.1-SNAPSHOT.jar`.

### Submit metrics to SonarCube
```
mvn install -Psonar
```
You must have `SONAR_TOKEN` environment variable set

### Deploy JARs to oss.sonatype.org
```
mvn deploy
```
You must have `CI_DEPLOY_USERNAME` and `CI_DEPLOY_PASSWORD` environment variables set

### Push image to Docker Hub
```
mvn deploy -Pdocker
```
You must have `DOCKER_USERNAME` and `DOCKER_PASSWORD` environment variables set

### Release (TODO)
```
mvn release:prepare release:perform -Prelease
```
See https://finosfoundation.atlassian.net/wiki/spaces/FDX/pages/75530322/Java#Java-Release