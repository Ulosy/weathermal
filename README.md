## Set-up
1. Install Java Development Kit 8: <https://www.oracle.com/java/technologies/javase-jdk8-downloads.html>
2. Download/install Eclipse IDE for Java: <https://www.eclipse.org/downloads>
	* IMPORTANT: When installing the Eclipse IDE, when given the option of "Java 1.8+ VM" be sure to choose from the drop-down the JDK instead of the JRE. By default the installer will pick the JRE, which will not work with Maven.
3. Install Google Chrome: <https://www.google.com/chrome/>
4. Open Eclipse IDE. 
5. Go to File -> Import, Git -> Projects from Git, Clone URI:
	* For URI: Copy the link from the green "Clone or download" button.
	* For Authentication section fill in your GitHub username/password
	* For the remaining options in the wizard you can just click "Next" and "Finish", the default settings are correct.
6. Install MySQL Workbench. <https://dev.mysql.com/downloads/workbench/> 
7. Set up 2 connections at localhost:3306 with username: root and password: root.
8. Run the 2 JunitTest.sql and WeatherPlanning.sql files on those two files


## Usage
### To run JUnit tests:
Go to src/main/java/weatherplanning/DatabaseConnector.java, replace line 17 with

```
private static final String DBTestPwd = "root"; // <== TODO: change to "root" for JUnit tests, otherwise you will get sql error
```
Right click project -> Run As -> "Maven test".

### To host your web app: 
Expand src/main/java/weatherplanning, right click setup.java file -> Run As -> "Java Application"
Go to "Run Configurations", run the "run" configuration.
Open Google Chrome and navigate to https://localhost:8443 to access the application via ssl.
You can stop the web server by clicking the red "stop" button in the console window.

If you get "Variable references non-existent resource : ${workspace_loc:/project2}" error, or just cannot run,
Change the ${workspace_loc:/project2} to {workspace_loc:/sp2020-project2-sp2020_project2_groupc} or vice versa in run.launch


### To run Cucumber tests:
Go to src/main/java/weatherplanning/DatabaseConnector.java, replace line 17 with
```java
private static final String DBTestPwd = "root"; // <== TODO: change to "root" for JUnit tests,
```
Make sure the webserver is running when you run the Cucumber tests (using the steps for hosting the web app above).
Go to Run->"Run Configurations", run the "cucumber" configuration.
Before running the cucumber tests, make sure that your WeatherPlanning database is empty by running the WeatherPlanning.sql again.

If you get "Variable references non-existent resource : ${workspace_loc:/project2}" error, or just cannot run cucumber,
Change the ${workspace_loc:/project2} to {workspace_loc:/sp2020-project2-sp2020_project2_groupc} or vice versa in cucumber.launch


### To access the web app:
Go to <https://localhost:8443>.
the https certificate is a self-signed certificate for testing purpose.
Click on advanced -> ignore warning.

if you want to access this app via http, try uncommenting this line at pom.xml at line 197 and go to localhost 8080.

```xml
<!-- uncomment this line if you want to access this webapp via port 8080 (no ssl)
    <connector implementation="org.eclipse.jetty.server.nio.SelectChannelConnector">
        <port>8080</port>
    </connector>
    -->
```

### Database Troubleshooting:
Make sure that the MySQL server is running on the background! (For Mac, go to system pref->MySQL)
.sql files are at at the project2/schema. Run .sql files again to reset the database when running cucumber tests to make sure they pass.

Make sure to change the DatabaseConnector.java lines to

	private static final String DBTestConnection = "jdbc:mysql://localhost:3306/JUnitTest";
	private static final String DBTestUser = "root";
	private static final String DBTestPwd = "root"; 
	
	private static final String DBConnection = "jdbc:mysql://localhost:3306/WeatherPlanning";
	private static final String DBUser = "root";
	private static final String DBPwd = "root"; 
