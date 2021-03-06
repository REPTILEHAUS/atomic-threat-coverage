| Title                | Taskmgr as Parent                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects the creation of a process from Windows task manager                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0005: Defense Evasion](https://attack.mitre.org/tactics/TA0005)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1036: Masquerading](https://attack.mitre.org/techniques/T1036)</li></ul>                             |
| Data Needed          | <ul><li>[DN_0002_4688_windows_process_creation_with_commandline](../Data_Needed/DN_0002_4688_windows_process_creation_with_commandline.md)</li><li>[DN_0003_1_windows_sysmon_process_creation](../Data_Needed/DN_0003_1_windows_sysmon_process_creation.md)</li></ul>                                                         |
| Trigger              | <ul><li>[T1036: Masquerading](../Triggers/T1036.md)</li></ul>  |
| Severity Level       | low                                                                                                                                                 |
| False Positives      | <ul><li>Administrative activity</li></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul></ul>                                                          |
| Author               | Florian Roth                                                                                                                                                |


## Detection Rules

### Sigma rule

```
title: Taskmgr as Parent
status: experimental
description: Detects the creation of a process from Windows task manager
tags:
    - attack.defense_evasion
    - attack.t1036
author: Florian Roth
date: 2018/03/13
logsource:
    category: process_creation
    product: windows
detection:
    selection:
        ParentImage: '*\taskmgr.exe'
    filter:
        Image:
            - resmon.exe
            - mmc.exe
    condition: selection and not filter
fields:
    - Image
    - CommandLine
    - ParentCommandLine
falsepositives:
    - Administrative activity
level: low

```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
(ParentImage:"*\\\\taskmgr.exe" AND NOT (Image:("resmon.exe" "mmc.exe")))
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*(?=.*.*\\taskmgr\\.exe)(?=.*(?!.*(?:.*(?=.*(?:.*resmon\\.exe|.*mmc\\.exe))))))'
```



