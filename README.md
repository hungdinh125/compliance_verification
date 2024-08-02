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
