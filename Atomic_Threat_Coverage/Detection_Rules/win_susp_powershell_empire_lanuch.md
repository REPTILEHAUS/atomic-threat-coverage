| Title                | Empire PowerShell Launch Parameters                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects suspicious powershell command line parameters used in Empire                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0002: Execution](https://attack.mitre.org/tactics/TA0002)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1086: PowerShell](https://attack.mitre.org/techniques/T1086)</li></ul>                             |
| Data Needed          | <ul><li>[DN_0002_4688_windows_process_creation_with_commandline](../Data_Needed/DN_0002_4688_windows_process_creation_with_commandline.md)</li><li>[DN_0003_1_windows_sysmon_process_creation](../Data_Needed/DN_0003_1_windows_sysmon_process_creation.md)</li></ul>                                                         |
| Trigger              | <ul><li>[T1086: PowerShell](../Triggers/T1086.md)</li></ul>  |
| Severity Level       | critical                                                                                                                                                 |
| False Positives      | <ul></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul><li>[https://github.com/EmpireProject/Empire/blob/c2ba61ca8d2031dad0cfc1d5770ba723e8b710db/lib/common/helpers.py#L165](https://github.com/EmpireProject/Empire/blob/c2ba61ca8d2031dad0cfc1d5770ba723e8b710db/lib/common/helpers.py#L165)</li><li>[https://github.com/EmpireProject/Empire/blob/e37fb2eef8ff8f5a0a689f1589f424906fe13055/lib/modules/powershell/persistence/powerbreach/deaduser.py#L191](https://github.com/EmpireProject/Empire/blob/e37fb2eef8ff8f5a0a689f1589f424906fe13055/lib/modules/powershell/persistence/powerbreach/deaduser.py#L191)</li><li>[https://github.com/EmpireProject/Empire/blob/e37fb2eef8ff8f5a0a689f1589f424906fe13055/lib/modules/powershell/persistence/powerbreach/resolver.py#L178](https://github.com/EmpireProject/Empire/blob/e37fb2eef8ff8f5a0a689f1589f424906fe13055/lib/modules/powershell/persistence/powerbreach/resolver.py#L178)</li></ul>                                                          |
| Author               | Florian Roth                                                                                                                                                |


## Detection Rules

### Sigma rule

```
title: Empire PowerShell Launch Parameters
description: Detects suspicious powershell command line parameters used in Empire
status: experimental
references:
    - https://github.com/EmpireProject/Empire/blob/c2ba61ca8d2031dad0cfc1d5770ba723e8b710db/lib/common/helpers.py#L165
    - https://github.com/EmpireProject/Empire/blob/e37fb2eef8ff8f5a0a689f1589f424906fe13055/lib/modules/powershell/persistence/powerbreach/deaduser.py#L191
    - https://github.com/EmpireProject/Empire/blob/e37fb2eef8ff8f5a0a689f1589f424906fe13055/lib/modules/powershell/persistence/powerbreach/resolver.py#L178
author: Florian Roth
date: 2019/04/20
tags:
  - attack.execution
  - attack.t1086
logsource:
    category: process_creation
    product: windows
detection:
    selection:
        CommandLine:
            - '* -NoP -sta -NonI -W Hidden -Enc *'
            - '* -noP -sta -w 1 -enc *'
    condition: selection
level: critical

```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
CommandLine:("* \\-NoP \\-sta \\-NonI \\-W Hidden \\-Enc *" "* \\-noP \\-sta \\-w 1 \\-enc *")
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*.* -NoP -sta -NonI -W Hidden -Enc .*|.*.* -noP -sta -w 1 -enc .*)'
```



