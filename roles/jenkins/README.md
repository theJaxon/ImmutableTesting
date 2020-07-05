### Bypassing the initial setup wizard:
1- Modify /etc/default/jenkins to include the following line 
```
JAVA_ARGS="-Djenkins.install.runSetupWizard=false"
```

2- Create the directory /var/lib/jenkins/init.groovy.d and place basic-security.groovy inside it 
This defines a default username and password of "admin"
[Credentials setup is from here](https://github.com/geerlingguy/ansible-role-jenkins/issues/50)

3- Downloading jenkins-cli from the current jenkins installation 
```
wget http://localhost:8080/jnlpJars/jenkins-cli.jar
```

4- Installing a specific plugin using the CLI
```bash
java -jar jenkins-cli.jar -auth admin:admin -s http://localhost:8080/ install-plugin blueocean

# Same but for a list of plugins 
#!/bin/bash
declare -a PluginList=(
    "blueocean"
    "gitea" 
    "kubernetes" 
)

# Iterate the string array using for loop
for plugin in ${PluginList[@]}; do
   java -jar jenkins-cli.jar -auth admin:admin -s http://localhost:8080/ install-plugin $plugin
done
```

5- Restarting jenkins after plugin installation
```
java -jar jenkins-cli.jar -auth admin:admin -s http://localhost:8080/ restart 
```