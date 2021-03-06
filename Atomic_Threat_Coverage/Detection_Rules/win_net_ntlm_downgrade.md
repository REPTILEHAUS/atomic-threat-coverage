| Title                | NetNTLM Downgrade Attack                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects post exploitation using NetNTLM downgrade attacks                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0006: Credential Access](https://attack.mitre.org/tactics/TA0006)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1212: Exploitation for Credential Access](https://attack.mitre.org/techniques/T1212)</li></ul>                             |
| Data Needed          | <ul><li>[DN_0017_13_windows_sysmon_RegistryEvent](../Data_Needed/DN_0017_13_windows_sysmon_RegistryEvent.md)</li><li>[DN_0059_4657_registry_value_was_modified](../Data_Needed/DN_0059_4657_registry_value_was_modified.md)</li></ul>                                                         |
| Trigger              | <ul><li>[T1212: Exploitation for Credential Access](../Triggers/T1212.md)</li></ul>  |
| Severity Level       | critical                                                                                                                                                 |
| False Positives      | <ul><li>Unknown</li></ul>                                                                  |
| Development Status   |                                                                                                                                                 |
| References           | <ul><li>[https://www.optiv.com/blog/post-exploitation-using-netntlm-downgrade-attacks](https://www.optiv.com/blog/post-exploitation-using-netntlm-downgrade-attacks)</li></ul>                                                          |
| Author               | Florian Roth                                                                                                                                                |


## Detection Rules

### Sigma rule

```
--- 
action: global
title: NetNTLM Downgrade Attack
description: Detects post exploitation using NetNTLM downgrade attacks
references: 
    - https://www.optiv.com/blog/post-exploitation-using-netntlm-downgrade-attacks
author: Florian Roth
date: 2018/03/20
tags:
    - attack.credential_access
    - attack.t1212
detection:
    condition: 1 of them
falsepositives:
    - Unknown
level: critical
--- 
logsource:
    product: windows
    service: sysmon
detection:
    selection1:
        EventID: 13
        TargetObject: 
            - '*SYSTEM\\*ControlSet*\Control\Lsa\lmcompatibilitylevel'
            - '*SYSTEM\\*ControlSet*\Control\Lsa\NtlmMinClientSec'
            - '*SYSTEM\\*ControlSet*\Control\Lsa\RestrictSendingNTLMTraffic'
---
# Windows Security Eventlog: Process Creation with Full Command Line
logsource:
    product: windows
    service: security
    definition: 'Requirements: Audit Policy : Object Access > Audit Registry (Success)'
detection:
    selection2:
        EventID: 4657
        ObjectName: '\REGISTRY\MACHINE\SYSTEM\\*ControlSet*\Control\Lsa'
        ObjectValueName: 
            - 'LmCompatibilityLevel'
            - 'NtlmMinClientSec'
            - 'RestrictSendingNTLMTraffic'

```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
(EventID:"13" AND TargetObject:("*SYSTEM\\\\*ControlSet*\\\\Control\\\\Lsa\\\\lmcompatibilitylevel" "*SYSTEM\\\\*ControlSet*\\\\Control\\\\Lsa\\\\NtlmMinClientSec" "*SYSTEM\\\\*ControlSet*\\\\Control\\\\Lsa\\\\RestrictSendingNTLMTraffic"))\n(EventID:"4657" AND ObjectName:"\\\\REGISTRY\\\\MACHINE\\\\SYSTEM\\\\*ControlSet*\\\\Control\\\\Lsa" AND ObjectValueName:("LmCompatibilityLevel" "NtlmMinClientSec" "RestrictSendingNTLMTraffic"))
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*(?=.*13)(?=.*(?:.*.*SYSTEM\\\\.*ControlSet.*\\Control\\Lsa\\lmcompatibilitylevel|.*.*SYSTEM\\\\.*ControlSet.*\\Control\\Lsa\\NtlmMinClientSec|.*.*SYSTEM\\\\.*ControlSet.*\\Control\\Lsa\\RestrictSendingNTLMTraffic)))'\ngrep -P '^(?:.*(?=.*4657)(?=.*\\REGISTRY\\MACHINE\\SYSTEM\\\\.*ControlSet.*\\Control\\Lsa)(?=.*(?:.*LmCompatibilityLevel|.*NtlmMinClientSec|.*RestrictSendingNTLMTraffic)))'
```



