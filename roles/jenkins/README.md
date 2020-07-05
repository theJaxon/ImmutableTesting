### Bypassing the initial setup wizard:
1- Modify /etc/default/jenkins to include the following line 
```
JAVA_ARGS="-Djenkins.install.runSetupWizard=false"
```

2- Create tge directory /var/lib/jenkins/init.groovy.d and place basic-security.groovy inside it 
This defines a default username and password of "admin"
[Credentials setup is from here](https://github.com/geerlingguy/ansible-role-jenkins/issues/50)

3- Downloading jenkins-cli from the current jenkins installation 
```
wget http://localhost:8080//jnlpJars/jenkins-cli.jar
```

4- Installing a specific plugin using the CLI
```
java -jar jenkins-cli.jar -s http://localhost:8080/ -auth admin:admin install-plugin blueocean
```

5- Restarting jenkins after plugin installation
```
java -jar jenkins-cli.jar -auth admin:admin -s http://localhost:8080/ restart 
```