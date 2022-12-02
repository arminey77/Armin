TRANSLATED:

Support (almost any version):
JIRA Software
JIRA Core
JIRA Service Desk
JIRA plugin: Capture
JIRA plugin: Training
JIRA plugin: Portfolio
Confluence
Confluence plugin: Questions
Confluence plugin: Team Calendars
Bamboo
Bitbucket
FishEye
Crowd
Crucible
Third party plugins

Automatically compile
Clone this project source code, pom.xml siblings, execute mvn package and then compile it.
Use atlassian-agent-jar-with-dependencies.jar produced using the target directory instead of atlassian-agent.jar!
If you don't know what I'm talking about, it's better to download my compiled package directly.

Configure Agent
1. Place atlassian-agent.jar in a location that you will not delete at will (all Atlassian services on your server can share the same atlassian-agent.jar).
2. Set the environment variable JAVA_OPTS (this is actually an environment variable for Java, used to specify the parameters that are included when starting the java program), and attach the -javaagent parameter. Specifically this
What to do:
You can put: export JAVA_OPTS = "-javaagent: /path/to/atlassian-agent.jar $ {JAVA_OPTS}" into .bashrcOr .bash_profile.
You can put: export JAVA_OPTS = "-javaagent: /path/to/atlassian-agent.jar $ {JAVA_OPTS}" to the service installation site
In setenv.sh or setenv.bat (for windows) in the bin directory.
You can also directly command and execute: JAVA_OPTS = "-javaagent: /path/to/atlassian-agent.jar" /path/to/start-confluence.sh
To start your service.
Or other methods you know to modify the environment variables, but if you have irrelevant services on your machine, it is not recommended to modify the global JAVA_OPTS environment variable.
In short you find a way to attach the -javaagent parameter to the java process to be started.
3. After configuration, please restart your Confluence service.
4. If you want to verify that the configuration is successful, you can do this:
Run a similar command: ps aux | grep java Find the corresponding process and see if the -javaagent parameter is correctly attached.
The software installation directory is similar to: /path/to/confluence/logs/catalina.out Tomcat. The log should look for
To: =========== output of agent working ==========.

Use KeyGen
You have to confirm that the agent has been configured, please refer to the above description.
When you try to execute java -jar /path/to/atlassian-agent.jar, you should see the output of the KeyGen parameter help.
Please take a closer look at the role of each parameter, especially the value range of the -p parameter.
The third party plug-in takes its application key as the -p parameter. For example: -p com.gliffy.integration.confluence
You should see something like: AAAA-BBBB-CCCC-DDDD server id during Atlassian service installation, please pay attention.
Provided the correct parameter operation, KeyGen will output the calculated activation code in the terminal.
Copy the activation code you generated to activate the service you want to use.
For example
Bitch: java -jar atlassian-agent.jar -p conf -m aaa@bbb.com -n my_name -o https://zhile.io -s ABCD-1234-EFGH-5678
