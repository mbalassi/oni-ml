# Configure Spark-ML environment under Eclipse

## Download and install Java language

Navigate to http://www.oracle.com/technetwork/java/javase/downloads/index.html and download Oracle JDK. Configure
JAVA_HOME and PATH according to the installation.

## Download and install Scala language

Navigate to http://www.scala-lang.org/download and download the recent version of Scala language. Unarchive the tgz file
and set up the environment as described under http://www.scala-lang.org/download/install.html.

## Download and install ScalaIDE

Navigate to http://scala-ide.org and download the recent version od Scala IDE.

## Create a Maven driven Scala project

- Start ScalaIDE.
- In Package Explorer clik on the blank area with right mouse button, then New->Scala Porject.
- If the name of the project is 'test', click on the name of the project with the right mouse button, then Configure->Convert to Maven Project.
- Fill in the project details of pom.xml.
- Replace pom.xml content with the following lines:
```
	<properties>
		<maven.compiler.source>1.8</maven.compiler.source>
		<maven.compiler.target>1.8</maven.compiler.target>
		<encoding>UTF-8</encoding>
		<scala.version>2.11.8</scala.version>
	</properties>

	<repositories>
		<repository>
			<id>scala-tools.org</id>
			<name>Scala-tools Maven2 Repository</name>
			<url>http://scala-tools.org/repo-releases</url>
		</repository>
		<repository>
			<id>central</id>
			<name>Maven Repository Switchboard</name>
			<layout>default</layout>
			<url>http://repo1.maven.org/maven2</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</repository>
	</repositories>

	<dependencies>
		<dependency>
			<groupId>org.apache.spark</groupId>
			<artifactId>spark-core_2.11</artifactId>
			<version>2.0.1</version>
		</dependency>
		<dependency>
			<groupId>org.apache.spark</groupId>
			<artifactId>spark-sql_2.11</artifactId>
			<version>2.0.1</version>
		</dependency>
		<dependency>
			<groupId>org.apache.spark</groupId>
			<artifactId>spark-mllib_2.11</artifactId>
			<version>2.0.1</version>
		</dependency>
		<dependency>
			<groupId>com.databricks</groupId>
			<artifactId>spark-csv_2.11</artifactId>
			<version>1.5.0</version>
		</dependency>
		<dependency>
			<groupId>org.scala-lang</groupId>
			<artifactId>scala-library</artifactId>
			<version>${scala.version}</version>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.scala-tools</groupId>
				<artifactId>maven-scala-plugin</artifactId>
				<executions>
					<execution>
						<goals>
							<goal>compile</goal>
							<goal>testCompile</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<sourceDir>src/main/scala</sourceDir>
					<jvmArgs>
						<jvmArg>-Xms64m</jvmArg>
						<jvmArg>-Xmx1024m</jvmArg>
					</jvmArgs>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-assembly-plugin</artifactId>
				<version>2.4</version>
				<configuration>
					<descriptorRefs>
						<descriptorRef>jar-with-dependencies</descriptorRef>
					</descriptorRefs>
					<archive>
						<manifest>
							<mainClass>kaggle.allstate.Allstate</mainClass>
						</manifest>
					</archive>
				</configuration>
				<executions>
					<execution>
						<phase>package</phase>
						<goals>
							<goal>single</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
			<plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>build-helper-maven-plugin</artifactId>
				<executions>
					<execution>
						<id>add-source</id>
						<phase>generate-sources</phase>
						<goals>
							<goal>add-source</goal>
						</goals>
						<configuration>
							<sources>
								<source>src/main/scala</source>
							</sources>
						</configuration>
					</execution>
					<execution>
						<id>add-test-source</id>
						<phase>generate-sources</phase>
						<goals>
							<goal>add-test-source</goal>
						</goals>
						<configuration>
							<sources>
								<source>src/test/scala</source>
							</sources>
						</configuration>
					</execution>
				</executions>
			</plugin>
			<plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>build-helper-maven-plugin</artifactId>
				<executions>
					<execution>
						<id>add-source</id>
						<phase>generate-sources</phase>
						<goals>
							<goal>add-source</goal>
						</goals>
						<configuration>
							<sources>
								<source>src/main/scala</source>
							</sources>
						</configuration>
					</execution>
					<execution>
						<id>add-test-source</id>
						<phase>generate-sources</phase>
						<goals>
							<goal>add-test-source</goal>
						</goals>
						<configuration>
							<sources>
								<source>src/test/scala</source>
							</sources>
						</configuration>
					</execution>
				</executions>
			</plugin>

		</plugins>
	</build>
```
- Fix Scala versions in pom.xml if a different version of Scala language was installed.
- Add Spark-ML code to the source folder.
- Run the project from ScalaIDE as a Scala Application.
