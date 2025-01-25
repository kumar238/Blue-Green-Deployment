Started by user Harendra Barot
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/Blue-Green
[Pipeline] {
[Pipeline] tool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Declarative: Tool Install)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] }
[Pipeline] // stage
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Git Checkout)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] git
The recommended git tool is: NONE
using credential git-cred
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/Blue-Green/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/Sudoharry/Blue-Green-Deployment.git # timeout=10
Fetching upstream changes from https://github.com/Sudoharry/Blue-Green-Deployment.git
 > git --version # timeout=10
 > git --version # 'git version 2.43.0'
using GIT_ASKPASS to set credentials git-cred
 > git fetch --tags --force --progress -- https://github.com/Sudoharry/Blue-Green-Deployment.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 2a909416d0f8c9e0c7207d60ccf3f79e012b2ae1 (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 2a909416d0f8c9e0c7207d60ccf3f79e012b2ae1 # timeout=10
 > git branch -a -v --no-abbrev # timeout=10
 > git branch -D main # timeout=10
 > git checkout -b main 2a909416d0f8c9e0c7207d60ccf3f79e012b2ae1 # timeout=10
Commit message: "Update Jenkinsfile"
 > git rev-list --no-walk 2a909416d0f8c9e0c7207d60ccf3f79e012b2ae1 # timeout=10
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Compile)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ mvn compile
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------< com.example:bankapp >-------------------------
[INFO] Building bankapp 0.0.1-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[WARNING] The artifact mysql:mysql-connector-java:jar:8.0.33 has been relocated to com.mysql:mysql-connector-j:jar:8.0.33: MySQL Connector/J artifacts moved to reverse-DNS compliant Maven 2+ coordinates.
[INFO] 
[INFO] --- resources:3.3.1:resources (default-resources) @ bankapp ---
[INFO] Copying 1 resource from src/main/resources to target/classes
[INFO] Copying 5 resources from src/main/resources to target/classes
[INFO] 
[INFO] --- compiler:3.13.0:compile (default-compile) @ bankapp ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.453 s
[INFO] Finished at: 2025-01-24T08:44:30Z
[INFO] ------------------------------------------------------------------------
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Tests)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ mvn test -DskipTests=true
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------< com.example:bankapp >-------------------------
[INFO] Building bankapp 0.0.1-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[WARNING] The artifact mysql:mysql-connector-java:jar:8.0.33 has been relocated to com.mysql:mysql-connector-j:jar:8.0.33: MySQL Connector/J artifacts moved to reverse-DNS compliant Maven 2+ coordinates.
[INFO] 
[INFO] --- resources:3.3.1:resources (default-resources) @ bankapp ---
[INFO] Copying 1 resource from src/main/resources to target/classes
[INFO] Copying 5 resources from src/main/resources to target/classes
[INFO] 
[INFO] --- compiler:3.13.0:compile (default-compile) @ bankapp ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] 
[INFO] --- resources:3.3.1:testResources (default-testResources) @ bankapp ---
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Blue-Green/src/test/resources
[INFO] 
[INFO] --- compiler:3.13.0:testCompile (default-testCompile) @ bankapp ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] 
[INFO] --- surefire:3.2.5:test (default-test) @ bankapp ---
[INFO] Tests are skipped.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.781 s
[INFO] Finished at: 2025-01-24T08:44:34Z
[INFO] ------------------------------------------------------------------------
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Trivy FS Scan)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ trivy fs --format table -o fs.html .
2025-01-24T08:44:35Z	INFO	[vuln] Vulnerability scanning is enabled
2025-01-24T08:44:35Z	INFO	[secret] Secret scanning is enabled
2025-01-24T08:44:35Z	INFO	[secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2025-01-24T08:44:35Z	INFO	[secret] Please see also https://aquasecurity.github.io/trivy/v0.58/docs/scanner/secret#recommendation for faster secret detection
2025-01-24T08:44:35Z	INFO	Number of language-specific files	num=1
2025-01-24T08:44:35Z	INFO	[pom] Detecting vulnerabilities...
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (SonarQube Analysis)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] withSonarQubeEnv
Injecting SonarQube environment variables using the configuration: sonar
[Pipeline] {
[Pipeline] sh
+ /var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=nodejsmysql -Dsonar.projectName=nodejsmysql -Dsonar.java.binaries=target
08:44:36.929 INFO  Scanner configuration file: /var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar-scanner/conf/sonar-scanner.properties
08:44:36.933 INFO  Project root configuration file: NONE
08:44:36.953 INFO  SonarScanner CLI 7.0.0.4796
08:44:36.955 INFO  Java 17.0.13 Ubuntu (64-bit)
08:44:36.956 INFO  Linux 6.8.0-1021-aws amd64
08:44:36.992 INFO  User cache: /var/lib/jenkins/.sonar/cache
08:44:38.107 INFO  Communicating with SonarQube Server 9.9.8.100196
08:44:38.641 INFO  Load global settings
08:44:38.720 INFO  Load global settings (done) | time=80ms
08:44:38.722 INFO  Server id: 147B411E-AZSWsZE25bYaR0K39b97
08:44:38.726 INFO  User cache: /var/lib/jenkins/.sonar/cache
08:44:38.730 INFO  Load/download plugins
08:44:38.730 INFO  Load plugins index
08:44:38.775 INFO  Load plugins index (done) | time=45ms
08:44:38.871 INFO  Load/download plugins (done) | time=141ms
08:44:39.507 INFO  Process project properties
08:44:39.508 INFO  Process project properties (done) | time=1ms
08:44:39.511 INFO  Execute project builders
08:44:39.513 INFO  Execute project builders (done) | time=2ms
08:44:39.519 INFO  Project key: nodejsmysql
08:44:39.519 INFO  Base dir: /var/lib/jenkins/workspace/Blue-Green
08:44:39.520 INFO  Working dir: /var/lib/jenkins/workspace/Blue-Green/.scannerwork
08:44:39.529 INFO  Load project settings for component key: 'nodejsmysql'
08:44:39.549 INFO  Load project settings for component key: 'nodejsmysql' (done) | time=19ms
08:44:39.703 INFO  Auto-configuring with CI 'Jenkins'
08:44:39.707 INFO  Load quality profiles
08:44:39.753 INFO  Load quality profiles (done) | time=46ms
08:44:39.762 INFO  Load active rules
08:44:41.458 INFO  Load active rules (done) | time=1696ms
08:44:41.466 INFO  Load analysis cache
08:44:41.482 INFO  Load analysis cache (378 bytes) | time=16ms
08:44:41.554 INFO  Load project repositories
08:44:41.574 INFO  Load project repositories (done) | time=20ms
08:44:41.617 INFO  Indexing files...
08:44:41.618 INFO  Project configuration:
08:44:41.838 WARN  File '/var/lib/jenkins/workspace/Blue-Green/target/bankapp-0.0.1-SNAPSHOT.jar' is bigger than 20MB and as consequence is removed from the analysis scope.
08:44:41.879 INFO  32 files indexed
08:44:41.880 INFO  21 files ignored because of scm ignore settings
08:44:41.881 INFO  Quality profile for java: Sonar way
08:44:41.881 INFO  Quality profile for terraform: Sonar way
08:44:41.881 INFO  Quality profile for web: Sonar way
08:44:41.881 INFO  Quality profile for xml: Sonar way
08:44:41.881 INFO  Quality profile for yaml: Sonar way
08:44:41.881 INFO  ------------- Run sensors on module nodejsmysql
08:44:42.002 INFO  Load metrics repository
08:44:42.039 INFO  Load metrics repository (done) | time=37ms
08:44:43.747 INFO  Sensor JavaSensor [java]
08:44:43.752 INFO  Configured Java source version (sonar.java.source): none
08:44:43.757 INFO  JavaClasspath initialization
08:44:43.759 INFO  JavaClasspath initialization (done) | time=2ms
08:44:43.759 INFO  JavaTestClasspath initialization
08:44:43.759 INFO  JavaTestClasspath initialization (done) | time=0ms
08:44:43.770 INFO  Server-side caching is enabled. The Java analyzer will not try to leverage data from a previous analysis.
08:44:43.776 INFO  Using ECJ batch to parse 9 Main java source files with batch size 51 KB.
08:44:43.934 INFO  Starting batch processing.
08:44:44.643 INFO  The Java analyzer cannot skip unchanged files in this context. A full analysis is performed for all files.
08:44:45.852 INFO  100% analyzed
08:44:45.852 INFO  Batch processing: Done.
08:44:45.853 INFO  Did not optimize analysis for any files, performed a full analysis for all 9 files.
08:44:45.855 WARN  Dependencies/libraries were not provided for analysis of SOURCE files. The 'sonar.java.libraries' property is empty. Verify your configuration, as you might end up with less precise results.
08:44:45.856 WARN  Unresolved imports/types have been detected during analysis. Enable DEBUG mode to see them.
08:44:45.856 WARN  Use of preview features have been detected during analysis. Enable DEBUG mode to see them.
08:44:45.857 INFO  No "Test" source files to scan.
08:44:45.857 INFO  No "Generated" source files to scan.
08:44:45.857 INFO  Sensor JavaSensor [java] (done) | time=2111ms
08:44:45.857 INFO  Sensor JaCoCo XML Report Importer [jacoco]
08:44:45.858 INFO  'sonar.coverage.jacoco.xmlReportPaths' is not defined. Using default locations: target/site/jacoco/jacoco.xml,target/site/jacoco-it/jacoco.xml,build/reports/jacoco/test/jacocoTestReport.xml
08:44:45.858 INFO  No report imported, no coverage information will be imported by JaCoCo XML Report Importer
08:44:45.859 INFO  Sensor JaCoCo XML Report Importer [jacoco] (done) | time=2ms
08:44:45.859 INFO  Sensor IaC Terraform Sensor [iac]
08:44:45.863 INFO  3 source files to be analyzed
08:44:46.092 INFO  3/3 source files have been analyzed
08:44:46.092 INFO  Sensor IaC Terraform Sensor [iac] (done) | time=233ms
08:44:46.092 INFO  Sensor IaC CloudFormation Sensor [iac]
08:44:46.116 INFO  0 source files to be analyzed
08:44:46.132 INFO  0/0 source files have been analyzed
08:44:46.132 INFO  Sensor IaC CloudFormation Sensor [iac] (done) | time=40ms
08:44:46.132 INFO  Sensor IaC Kubernetes Sensor [iac]
08:44:46.154 INFO  4 source files to be analyzed
08:44:46.253 INFO  4/4 source files have been analyzed
08:44:46.254 INFO  Sensor IaC Kubernetes Sensor [iac] (done) | time=122ms
08:44:46.254 INFO  Sensor JavaScript inside YAML analysis [javascript]
08:44:46.263 INFO  No input files found for analysis
08:44:46.263 INFO  Hit the cache for 0 out of 0
08:44:46.264 INFO  Miss the cache for 0 out of 0
08:44:46.264 INFO  Sensor JavaScript inside YAML analysis [javascript] (done) | time=10ms
08:44:46.265 INFO  Sensor CSS Rules [javascript]
08:44:48.283 WARN  Error when running: 'node -v'. Is Node.js available during analysis?
08:44:48.283 INFO  Hit the cache for 0 out of 0
08:44:48.283 INFO  Miss the cache for 0 out of 0
08:44:48.284 INFO  Sensor CSS Rules [javascript] (done) | time=2019ms
08:44:48.284 INFO  Sensor C# Project Type Information [csharp]
08:44:48.284 INFO  Sensor C# Project Type Information [csharp] (done) | time=0ms
08:44:48.284 INFO  Sensor C# Analysis Log [csharp]
08:44:48.297 INFO  Sensor C# Analysis Log [csharp] (done) | time=13ms
08:44:48.297 INFO  Sensor C# Properties [csharp]
08:44:48.297 INFO  Sensor C# Properties [csharp] (done) | time=0ms
08:44:48.298 INFO  Sensor SurefireSensor [java]
08:44:48.298 INFO  parsing [/var/lib/jenkins/workspace/Blue-Green/target/surefire-reports]
08:44:48.299 INFO  Sensor SurefireSensor [java] (done) | time=2ms
08:44:48.299 INFO  Sensor HTML [web]
08:44:48.483 INFO  Sensor HTML [web] (done) | time=184ms
08:44:48.484 INFO  Sensor XML Sensor [xml]
08:44:48.497 INFO  1 source file to be analyzed
08:44:48.668 INFO  1/1 source file has been analyzed
08:44:48.668 INFO  Sensor XML Sensor [xml] (done) | time=184ms
08:44:48.669 INFO  Sensor TextAndSecretsSensor [text]
08:44:48.677 INFO  23 source files to be analyzed
08:44:48.767 INFO  23/23 source files have been analyzed
08:44:48.767 INFO  Sensor TextAndSecretsSensor [text] (done) | time=98ms
08:44:48.767 INFO  Sensor VB.NET Project Type Information [vbnet]
08:44:48.768 INFO  Sensor VB.NET Project Type Information [vbnet] (done) | time=1ms
08:44:48.768 INFO  Sensor VB.NET Analysis Log [vbnet]
08:44:48.782 INFO  Sensor VB.NET Analysis Log [vbnet] (done) | time=14ms
08:44:48.782 INFO  Sensor VB.NET Properties [vbnet]
08:44:48.782 INFO  Sensor VB.NET Properties [vbnet] (done) | time=0ms
08:44:48.782 INFO  Sensor IaC Docker Sensor [iac]
08:44:48.783 INFO  1 source file to be analyzed
08:44:48.828 INFO  1/1 source file has been analyzed
08:44:48.828 INFO  Sensor IaC Docker Sensor [iac] (done) | time=46ms
08:44:48.831 INFO  ------------- Run sensors on project
08:44:48.904 INFO  Sensor Analysis Warnings import [csharp]
08:44:48.905 INFO  Sensor Analysis Warnings import [csharp] (done) | time=1ms
08:44:48.905 INFO  Sensor Zero Coverage Sensor
08:44:48.928 INFO  Sensor Zero Coverage Sensor (done) | time=23ms
08:44:48.928 INFO  Sensor Java CPD Block Indexer
08:44:48.969 INFO  Sensor Java CPD Block Indexer (done) | time=41ms
08:44:48.978 INFO  SCM Publisher SCM provider for this project is: git
08:44:48.981 INFO  SCM Publisher 1 source file to be analyzed
08:44:49.020 INFO  SCM Publisher 0/1 source files have been analyzed (done) | time=37ms
08:44:49.020 WARN  Missing blame information for the following files:
08:44:49.021 WARN    * fs.html
08:44:49.021 WARN  This may lead to missing/broken features in SonarQube
08:44:49.034 INFO  CPD Executor 4 files had no CPD blocks
08:44:49.034 INFO  CPD Executor Calculating CPD for 10 files
08:44:49.063 INFO  CPD Executor CPD calculation finished (done) | time=28ms
08:44:49.173 INFO  Analysis report generated in 105ms, dir size=225.7 kB
08:44:49.222 INFO  Analysis report compressed in 49ms, zip size=68.6 kB
08:44:49.285 INFO  Analysis report uploaded in 62ms
08:44:49.287 INFO  ANALYSIS SUCCESSFUL, you can find the results at: http://35.154.248.151:9000/dashboard?id=nodejsmysql
08:44:49.287 INFO  Note that you will be able to access the updated dashboard once the server has processed the submitted analysis report
08:44:49.287 INFO  More about the report processing at http://35.154.248.151:9000/api/ce/task?id=AZSXfDzV5bYaR0K39l-K
08:44:49.814 INFO  Analysis total time: 10.839 s
08:44:49.815 INFO  EXECUTION SUCCESS
08:44:49.816 INFO  Total time: 12.932s
[Pipeline] }
[Pipeline] // withSonarQubeEnv
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ mvn package -DskipTests=true
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------< com.example:bankapp >-------------------------
[INFO] Building bankapp 0.0.1-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[WARNING] The artifact mysql:mysql-connector-java:jar:8.0.33 has been relocated to com.mysql:mysql-connector-j:jar:8.0.33: MySQL Connector/J artifacts moved to reverse-DNS compliant Maven 2+ coordinates.
[INFO] 
[INFO] --- resources:3.3.1:resources (default-resources) @ bankapp ---
[INFO] Copying 1 resource from src/main/resources to target/classes
[INFO] Copying 5 resources from src/main/resources to target/classes
[INFO] 
[INFO] --- compiler:3.13.0:compile (default-compile) @ bankapp ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] 
[INFO] --- resources:3.3.1:testResources (default-testResources) @ bankapp ---
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Blue-Green/src/test/resources
[INFO] 
[INFO] --- compiler:3.13.0:testCompile (default-testCompile) @ bankapp ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] 
[INFO] --- surefire:3.2.5:test (default-test) @ bankapp ---
[INFO] Tests are skipped.
[INFO] 
[INFO] --- jar:3.4.2:jar (default-jar) @ bankapp ---
[INFO] 
[INFO] --- spring-boot:3.3.3:repackage (repackage) @ bankapp ---
[INFO] Replacing main artifact /var/lib/jenkins/workspace/Blue-Green/target/bankapp-0.0.1-SNAPSHOT.jar with repackaged archive, adding nested dependencies in BOOT-INF/.
[INFO] The original artifact has been renamed to /var/lib/jenkins/workspace/Blue-Green/target/bankapp-0.0.1-SNAPSHOT.jar.original
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.294 s
[INFO] Finished at: 2025-01-24T08:44:54Z
[INFO] ------------------------------------------------------------------------
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Pulbish Artifacts to Nexus)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] withMaven
[withMaven] Options: []
[withMaven] Available options: 
[withMaven] using JDK installation provided by the build agent
[withMaven] using Maven global settings.xml 'maven-settings' with NO Maven servers credentials provided by Jenkins
[withMaven] using Maven installation 'maven3'
[withMaven] found Maven version: Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
[Pipeline] {
[Pipeline] sh
+ mvn deploy -DskipTests=true
----- withMaven Wrapper script -----
Picked up JAVA_TOOL_OPTIONS: -Dmaven.ext.class.path="/var/lib/jenkins/workspace/Blue-Green@tmp/withMaven1bdb24c7/pipeline-maven-spy.jar" -Dorg.jenkinsci.plugins.pipeline.maven.reportsFolder="/var/lib/jenkins/workspace/Blue-Green@tmp/withMaven1bdb24c7" 
Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
Maven home: /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven3
Java version: 17.0.13, vendor: Ubuntu, runtime: /usr/lib/jvm/java-17-openjdk-amd64
Default locale: en, platform encoding: UTF-8
OS name: "linux", version: "6.8.0-1021-aws", arch: "amd64", family: "unix"
[INFO] [jenkins-event-spy] Generate /var/lib/jenkins/workspace/Blue-Green@tmp/withMaven1bdb24c7/maven-spy-20250124-084456-82314280750686454425738.log.tmp ...
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------< com.example:bankapp >-------------------------
[INFO] Building bankapp 0.0.1-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[WARNING] The artifact mysql:mysql-connector-java:jar:8.0.33 has been relocated to com.mysql:mysql-connector-j:jar:8.0.33: MySQL Connector/J artifacts moved to reverse-DNS compliant Maven 2+ coordinates.
[INFO] 
[INFO] --- resources:3.3.1:resources (default-resources) @ bankapp ---
[INFO] Copying 1 resource from src/main/resources to target/classes
[INFO] Copying 5 resources from src/main/resources to target/classes
[INFO] 
[INFO] --- compiler:3.13.0:compile (default-compile) @ bankapp ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] 
[INFO] --- resources:3.3.1:testResources (default-testResources) @ bankapp ---
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Blue-Green/src/test/resources
[INFO] 
[INFO] --- compiler:3.13.0:testCompile (default-testCompile) @ bankapp ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] 
[INFO] --- surefire:3.2.5:test (default-test) @ bankapp ---
[INFO] Tests are skipped.
[INFO] 
[INFO] --- jar:3.4.2:jar (default-jar) @ bankapp ---
[INFO] 
[INFO] --- spring-boot:3.3.3:repackage (repackage) @ bankapp ---
[INFO] Replacing main artifact /var/lib/jenkins/workspace/Blue-Green/target/bankapp-0.0.1-SNAPSHOT.jar with repackaged archive, adding nested dependencies in BOOT-INF/.
[INFO] The original artifact has been renamed to /var/lib/jenkins/workspace/Blue-Green/target/bankapp-0.0.1-SNAPSHOT.jar.original
[INFO] 
[INFO] --- install:3.1.3:install (default-install) @ bankapp ---
[INFO] Installing /var/lib/jenkins/workspace/Blue-Green/pom.xml to /var/lib/jenkins/.m2/repository/com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-SNAPSHOT.pom
[INFO] Installing /var/lib/jenkins/workspace/Blue-Green/target/bankapp-0.0.1-SNAPSHOT.jar to /var/lib/jenkins/.m2/repository/com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-SNAPSHOT.jar
[INFO] 
[INFO] --- deploy:3.1.3:deploy (default-deploy) @ bankapp ---
[INFO] Downloading from maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/maven-metadata.xml
[INFO] Downloaded from maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/maven-metadata.xml (768 B at 7.5 kB/s)
[INFO] Uploading to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-20250124.084456-4.pom
[INFO] Uploaded to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-20250124.084456-4.pom (2.6 kB at 47 kB/s)
[INFO] Uploading to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-20250124.084456-4.jar
[INFO] Uploaded to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-20250124.084456-4.jar (52 MB at 30 MB/s)
[INFO] Downloading from maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/maven-metadata.xml
[INFO] Downloaded from maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/maven-metadata.xml (278 B at 15 kB/s)
[INFO] Uploading to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/maven-metadata.xml
[INFO] Uploaded to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/0.0.1-SNAPSHOT/maven-metadata.xml (768 B at 18 kB/s)
[INFO] Uploading to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/maven-metadata.xml
[INFO] Uploaded to maven-snapshots: http://52.66.199.174:8081/repository/maven-snapshots/com/example/bankapp/maven-metadata.xml (278 B at 5.2 kB/s)
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  5.005 s
[INFO] Finished at: 2025-01-24T08:45:01Z
[INFO] ------------------------------------------------------------------------
[INFO] [jenkins-event-spy] Generated /var/lib/jenkins/workspace/Blue-Green@tmp/withMaven1bdb24c7/maven-spy-20250124-084456-82314280750686454425738.log
[Pipeline] }
[withMaven] artifactsPublisher - Archive artifact pom.xml under com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-SNAPSHOT.pom
[withMaven] artifactsPublisher - Archive artifact target/bankapp-0.0.1-SNAPSHOT.jar under com/example/bankapp/0.0.1-SNAPSHOT/bankapp-0.0.1-SNAPSHOT.jar
[withMaven] junitPublisher - Archive test results for Maven artifact com.example:bankapp:jar:0.0.1-SNAPSHOT generated by maven-surefire-plugin:test (default-test): target/surefire-reports/*.xml
[withMaven] junitPublisher - Jenkins JUnit Attachments Plugin not found, can't publish test attachments.
[withMaven] junitPublisher - Jenkins JUnit Flaky Test Handler Plugin not found, can't publish JUnit flaky tests reports.
Recording test results
No test report files were found. Configuration error?
None of the test reports contained any result
[Checks API] No suitable checks publisher found.
[withMaven] Jenkins FindBugs Plugin not found, don't display org.codehaus.mojo:findbugs-maven-plugin:findbugs results in pipeline screen.
[withMaven] jgivenPublisher - Jenkins JGiven Plugin not found, do not archive jgiven reports.
[withMaven] Jenkins Task Scanner Plugin not found, don't display results of source code scanning for 'TODO' and 'FIXME' in pipeline screen.
[withMaven] Publishers: Pipeline Graph Publisher: 1 ms, Generated Artifacts Publisher: 173 ms, Junit Publisher: 9 ms, Findbugs Publisher: 2 ms
[Pipeline] // withMaven
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Docker build & Tag Image)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] withDockerRegistry
$ docker login -u harendrabarot -p ******** https://index.docker.io/v1/
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /var/lib/jenkins/workspace/Blue-Green@tmp/76ce9a1b-0995-4d72-86fc-b9c8cd6c565c/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credential-stores

Login Succeeded
[Pipeline] {
[Pipeline] sh
+ docker build -t harendrabarot/bankapp:blue .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 208B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/eclipse-temurin:17-jdk-alpine
#2 ...

#3 [auth] library/eclipse-temurin:pull token for registry-1.docker.io
#3 DONE 0.0s

#2 [internal] load metadata for docker.io/library/eclipse-temurin:17-jdk-alpine
#2 DONE 1.4s

#4 [internal] load .dockerignore
#4 transferring context: 2B done
#4 DONE 0.0s

#5 [1/3] FROM docker.io/library/eclipse-temurin:17-jdk-alpine@sha256:d60e19d7da3a1bebbde66f740841d822c0e518aebf99a4403da16bb34f0373f8
#5 DONE 0.0s

#6 [internal] load build context
#6 transferring context: 52.33MB 0.5s done
#6 DONE 0.5s

#7 [2/3] COPY target/*.jar /usr/src/app/app.jar
#7 CACHED

#8 [3/3] WORKDIR /usr/src/app
#8 CACHED

#9 exporting to image
#9 exporting layers done
#9 writing image sha256:de58c106ca3c660a2e5ed5ea82834adba3f90882b2164065f8d8dac62e0c0a2b done
#9 naming to docker.io/harendrabarot/bankapp:blue done
#9 DONE 0.0s

 [33m1 warning found (use docker --debug to expand):
[0m - LegacyKeyValueFormat: "ENV key=value" should be used instead of legacy "ENV key value" format (line 5)
[Pipeline] }
[Pipeline] // withDockerRegistry
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Trivy image Scan)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ trivy image --format table -o fs.html harendrabarot/bankapp:blue
2025-01-24T08:45:07Z	INFO	[vuln] Vulnerability scanning is enabled
2025-01-24T08:45:07Z	INFO	[secret] Secret scanning is enabled
2025-01-24T08:45:07Z	INFO	[secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2025-01-24T08:45:07Z	INFO	[secret] Please see also https://aquasecurity.github.io/trivy/v0.58/docs/scanner/secret#recommendation for faster secret detection
2025-01-24T08:45:07Z	INFO	Detected OS	family="alpine" version="3.21.2"
2025-01-24T08:45:07Z	WARN	This OS version is not on the EOL list	family="alpine" version="3.21"
2025-01-24T08:45:07Z	INFO	[alpine] Detecting vulnerabilities...	os_version="3.21" repository="3.21" pkg_num=76
2025-01-24T08:45:07Z	INFO	Number of language-specific files	num=1
2025-01-24T08:45:07Z	INFO	[jar] Detecting vulnerabilities...
2025-01-24T08:45:07Z	INFO	Table result includes only package filenames. Use '--format json' option to get the full path to the package file.
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Docker Push Image)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] withDockerRegistry
$ docker login -u harendrabarot -p ******** https://index.docker.io/v1/
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /var/lib/jenkins/workspace/Blue-Green@tmp/0731e784-585f-4838-bc2e-8175b115ed4f/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credential-stores

Login Succeeded
[Pipeline] {
[Pipeline] sh
+ docker push harendrabarot/bankapp:blue
The push refers to repository [docker.io/harendrabarot/bankapp]
5f70bf18a086: Preparing
2b6b581d8946: Preparing
c4ef0b0c441d: Preparing
4b086c2dcc54: Preparing
d1e443b86c84: Preparing
0468ec7f7926: Preparing
a0904247e36a: Preparing
0468ec7f7926: Waiting
a0904247e36a: Waiting
2b6b581d8946: Layer already exists
d1e443b86c84: Layer already exists
5f70bf18a086: Layer already exists
c4ef0b0c441d: Layer already exists
4b086c2dcc54: Layer already exists
0468ec7f7926: Layer already exists
a0904247e36a: Layer already exists
blue: digest: sha256:bce636b7a74f51cc3459a7164875c4cc8c0c33c4e2241f2425307bd2262b20c3 size: 1786
[Pipeline] }
[Pipeline] // withDockerRegistry
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Deploy MySQL Deployment and Service)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] withKubeConfig
[Pipeline] {
[Pipeline] sh
+ kubectl apply -f mysql-ds.yml -n webapps
deployment.apps/mysql configured
service/mysql-service unchanged
[Pipeline] }
[kubernetes-cli] kubectl configuration cleaned up
[Pipeline] // withKubeConfig
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Deploy SVC-APP)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] withKubeConfig
[Pipeline] {
[Pipeline] sh
+ kubectl get svc bankapp-service -n webapps
NAME              TYPE           CLUSTER-IP     EXTERNAL-IP                                                              PORT(S)        AGE
bankapp-service   LoadBalancer   172.20.45.27   a8fa4d5a4a5d0491595acd08433fb696-26129209.ap-south-1.elb.amazonaws.com   80:31059/TCP   18m
[Pipeline] }
[kubernetes-cli] kubectl configuration cleaned up
[Pipeline] // withKubeConfig
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Deploy to Kubernetes)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] withKubeConfig
[Pipeline] {
[Pipeline] sh
+ kubectl apply -f app-deployment-blue.yml -n webapps
deployment.apps/bankapp-blue configured
[Pipeline] }
[kubernetes-cli] kubectl configuration cleaned up
[Pipeline] // withKubeConfig
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Switch Traffic Between Blue & Green Environment)
Stage "Switch Traffic Between Blue & Green Environment" skipped due to when conditional
[Pipeline] getContext
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Verify Deployment)
[Pipeline] tool
[Pipeline] envVarsForTool
[Pipeline] withEnv
[Pipeline] {
[Pipeline] script
[Pipeline] {
[Pipeline] withKubeConfig
[Pipeline] {
[Pipeline] sh
+ kubectl get pods -l version=blue -n webapps
NAME                            READY   STATUS    RESTARTS   AGE
bankapp-blue-76cc99cfff-j8l54   1/1     Running   0          18m
+ kubectl get svc bankapp-service -n webapps
NAME              TYPE           CLUSTER-IP     EXTERNAL-IP                                                              PORT(S)        AGE
bankapp-service   LoadBalancer   172.20.45.27   a8fa4d5a4a5d0491595acd08433fb696-26129209.ap-south-1.elb.amazonaws.com   80:31059/TCP   18m
[Pipeline] }
[kubernetes-cli] kubectl configuration cleaned up
[Pipeline] // withKubeConfig
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
