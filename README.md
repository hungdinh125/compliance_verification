#### Error message
 - The authenticity of host '10.148.253.1' can't be established due to 'Host is unknown: 64:15:f2:da:95:8c:b9:f9:80:b4:d2:9b:04:50:fe:80:14:d6:6a:22'.\nThe ssh-rsa key fingerprint is SHA1:ZBXy2pWMufmAtNKbBFD+gBTWaiI."}}, "msg": "The following modules failed to execute: ansible.legacy.ios_facts\n"}


#### Remediation
 ```bash
$ ssh-keyscan -H 10.148.253.1 >> ~/.ssh/known_hosts
# 10.148.253.1:22 SSH-2.0-Cisco-1.25
# 10.148.253.1:22 SSH-2.0-Cisco-1.25
# 10.148.253.1:22 SSH-2.0-Cisco-1.25
# 10.148.253.1:22 SSH-2.0-Cisco-1.25
# 10.148.253.1:22 SSH-2.0-Cisco-1.25
```

#### Error message
 + ansible-playbook compliance_verification/compliance.yml -i compliance_verification/inventory --check
ERROR! the playbook: compliance_verification/compliance.yml could not be found

#### Remediation
- Add a stage to verify the directory structure after clone the repo

```Groovy
stage('Verify directory is cloned') {
    steps {
        sh 'ls -la'
    }
}
```

- Result
```bash
total 20
drwxr-xr-x. 3 jenkins jenkins 112 Aug  2 19:41 .
drwxr-xr-x. 6 jenkins jenkins 170 Aug  2 19:17 ..
-rw-r--r--. 1 jenkins jenkins 835 Aug  2 19:41 compliance.yml
drwxr-xr-x. 8 jenkins jenkins 162 Aug  2 19:41 .git
-rw-r--r--. 1 jenkins jenkins 219 Aug  2 19:41 inventory
-rw-r--r--. 1 jenkins jenkins 899 Aug  2 19:41 Jenkinsfile
-rw-r--r--. 1 jenkins jenkins 699 Aug  2 19:41 Jenskinfile
-rw-r--r--. 1 jenkins jenkins 588 Aug  2 19:41 README.md
```

- Correct the bash cli in the ansible-playbook

```bash
ansible-playbook compliance.yml -i inventory --check
```

### Reachability_check pipeline
- The type of this pipeline is __Free style project__, and Build Steps is __Execute shell__
- Then, add the ping command

```bash
ping -c 1 10.148.253.1
```

- Next is to add the __reachability_check__ to the main pipeline
  
```python
stage('Verify reachability') {
  steps {
    build(job: 'reachability_check')
    }
}
```
