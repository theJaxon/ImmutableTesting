### Bypassing the initial setup wizard:
1- Modify /etc/default/jenkins to include the following line 
```
JAVA_ARGS="-Djenkins.install.runSetupWizard=false"
```

2- Create tge directory /var/lib/jenkins/init.groovy.d and place basic-security.groovy inside it 
This defines a default username and password of "admin"
[Credentials setup is from here](https://github.com/geerlingguy/ansible-role-jenkins/issues/50)