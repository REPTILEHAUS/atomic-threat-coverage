| Title                | Suspicious Program Location Process Starts                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects programs running in suspicious files system locations                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0005: Defense Evasion](https://attack.mitre.org/tactics/TA0005)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1036: Masquerading](https://attack.mitre.org/techniques/T1036)</li></ul>                             |
| Data Needed          | <ul><li>[DN_0002_4688_windows_process_creation_with_commandline](../Data_Needed/DN_0002_4688_windows_process_creation_with_commandline.md)</li><li>[DN_0001_4688_windows_process_creation](../Data_Needed/DN_0001_4688_windows_process_creation.md)</li><li>[DN_0003_1_windows_sysmon_process_creation](../Data_Needed/DN_0003_1_windows_sysmon_process_creation.md)</li></ul>                                                         |
| Trigger              | <ul><li>[T1036: Masquerading](../Triggers/T1036.md)</li></ul>  |
| Severity Level       | high                                                                                                                                                 |
| False Positives      | <ul><li>unknown</li></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul><li>[https://docs.google.com/spreadsheets/d/17pSTDNpa0sf6pHeRhusvWG6rThciE8CsXTSlDUAZDyo](https://docs.google.com/spreadsheets/d/17pSTDNpa0sf6pHeRhusvWG6rThciE8CsXTSlDUAZDyo)</li></ul>                                                          |
| Author               | Florian Roth                                                                                                                                                |


## Detection Rules

### Sigma rule

```
title: Suspicious Program Location Process Starts
status: experimental
description: Detects programs running in suspicious files system locations
references:
    - https://docs.google.com/spreadsheets/d/17pSTDNpa0sf6pHeRhusvWG6rThciE8CsXTSlDUAZDyo
tags:
    - attack.defense_evasion
    - attack.t1036
author: Florian Roth
date: 2019/01/15
logsource:
    category: process_creation
    product: windows
detection:
    selection:
        Image:
            - '*\$Recycle.bin'
            - '*\Users\Public\\*'
            - 'C:\Perflogs\\*'
            - '*\Windows\Fonts\\*'
            - '*\Windows\IME\\*'
            - '*\Windows\addins\\*'
            - '*\Windows\debug\\*'
    condition: selection
falsepositives:
    - unknown
level: high

```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
Image:("*\\\\$Recycle.bin" "*\\\\Users\\\\Public\\\\*" "C\\:\\\\Perflogs\\\\*" "*\\\\Windows\\\\Fonts\\\\*" "*\\\\Windows\\\\IME\\\\*" "*\\\\Windows\\\\addins\\\\*" "*\\\\Windows\\\\debug\\\\*")
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*.*\\\\$Recycle\\.bin|.*.*\\Users\\Public\\\\.*|.*C:\\Perflogs\\\\.*|.*.*\\Windows\\Fonts\\\\.*|.*.*\\Windows\\IME\\\\.*|.*.*\\Windows\\addins\\\\.*|.*.*\\Windows\\debug\\\\.*)'
```



