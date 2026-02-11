---
cssclasses:
  - border-tab
  - cards
  - rtl-dataview
---
عادت: {{name}}




## [[Weekly|Weekly(هفتگی)]]

```contributionGraph
title: ""
graphType: default
dateRangeValue: 180
dateRangeType: FIXED_DATE_RANGE
startOfWeek: "6"
showCellRuleIndicators: true
titleStyle:
  textAlign: left
  fontSize: 15px
  fontWeight: normal
dataSource:
  type: PAGE
  value: "#journal"
  dateField:
    type: FILE_NAME
    value: date
  countField:
    type: PAGE_PROPERTY
    value: {{name}}
fillTheScreen: false
enableMainContainerShadow: false
fromDate: {{اول هفته}}
toDate: {{آخر هفته}}
cellStyleRules:
  - id: Ocean_a
    color: "#c0e1ffff"
    min: 1
    max: "2"
  - id: Ocean_b
    color: "#5fbfffff"
    min: "2"
    max: "3"
  - id: Ocean_c
    color: "#0784e4ff"
    min: "3"
    max: "4"
  - id: Ocean_d
    color: "#0760a9ff"
    min: "4"
    max: "5"
  - id: 1713257815258
    min: "5"
    max: "24"
    color: "#083864ff"
    text: ""
mainContainerStyle:
  backgroundColor: "#ffffff00"
cellStyle:
  minWidth: 20px
  minHeight: 20px

```

```dataview
TABLE 
    "✅ " + length(filter(rows, (r) => r.{{name}} = true)) + " روز انجام شد" as true,
    "❌ " + length(filter(rows, (r) => r.{{name}} = false)) + " روز انجام نشد" as false
FROM #journal
WHERE file.name >= ("{{اول هفته}}") AND file.name <= ("{{آخر هفته}}")
GROUP BY ""
```



## [[Monthly|Monthly (ماهانه)]]



```contributionGraph
title: " "
graphType: default
dateRangeValue: 180
dateRangeType: FIXED_DATE_RANGE
startOfWeek: "6"
showCellRuleIndicators: true
titleStyle:
  textAlign: center
  fontSize: 15px
  fontWeight: normal
dataSource:
  type: PAGE
  value: "#journal"
  dateField:
    type: FILE_NAME
    value: date
  countField:
    type: PAGE_PROPERTY
    value: {{name}}
fillTheScreen: false
enableMainContainerShadow: false
fromDate: {{اول ماه}}
toDate: {{آخر ماه}}
cellStyleRules:
  - id: default_b
    color: "#64da7aff"
    min: 1
    max: 2
cellStyle:
  minWidth: 20px
  minHeight: 20px
mainContainerStyle:
  backgroundColor: "#ffffff00"
```

```dataview
TABLE 
    "✅ " + length(filter(rows, (r) => r.{{name}} = true)) + " روز انجام شد" as true,
    "❌ " + length(filter(rows, (r) => r.{{name}} = false)) + " روز انجام نشد" as false
FROM #journal
WHERE file.name >= ("{{اول ماه}}") AND file.name <= ("{{آخر ماه}}")
GROUP BY ""
```




## [[Quarterly|Quarterly(سه‌ماهه)]]



```contributionGraph
title: " "
graphType: default
dateRangeValue: 180
dateRangeType: FIXED_DATE_RANGE
startOfWeek: "6"
showCellRuleIndicators: true
titleStyle:
  textAlign: center
  fontSize: 15px
  fontWeight: normal
dataSource:
  type: PAGE
  value: "#journal"
  dateField:
    type: FILE_NAME
    value: date
  countField:
    type: PAGE_PROPERTY
    value: {{name}}
fillTheScreen: false
enableMainContainerShadow: false
fromDate: {{اول فصل}}
toDate: {{آخر فصل}}
cellStyleRules:
  - id: default_b
    color: "#64da7aff"
    min: 1
    max: 2
cellStyle:
  minWidth: 20px
  minHeight: 20px
mainContainerStyle:
  backgroundColor: "#ffffff00"
```

```dataview
TABLE 
    "✅ " + length(filter(rows, (r) => r.{{name}} = true)) + " روز انجام شد" as true,
    "❌ " + length(filter(rows, (r) => r.{{name}} = false)) + " روز انجام نشد" as false
FROM #journal
WHERE file.name >= ("{{اول فصل}}") AND file.name <= ("{{آخر فصل}}")
GROUP BY ""
```



## [[Yearly|Yearly(سالانه)]]





```contributionGraph
title: " "
graphType: default
dateRangeValue: 180
dateRangeType: FIXED_DATE_RANGE
startOfWeek: "6"
showCellRuleIndicators: true
titleStyle:
  textAlign: center
  fontSize: 15px
  fontWeight: normal
dataSource:
  type: PAGE
  value: "#journal"
  dateField:
    type: FILE_NAME
    value: date
  countField:
    type: PAGE_PROPERTY
    value: {{name}}
fillTheScreen: true
enableMainContainerShadow: false
fromDate: {{اول سال}}
toDate: {{آخر سال}}
cellStyleRules:
  - id: default_b
    color: "#64da7aff"
    min: 1
    max: 2
cellStyle:
  borderRadius: ""
  minWidth: 12px
  minHeight: 12px
mainContainerStyle:
  backgroundColor: "#00000000"
```

```dataview
TABLE 
    "✅ " + length(filter(rows, (r) => r.{{name}} = true)) + " روز انجام شد" as true,
    "❌ " + length(filter(rows, (r) => r.{{name}} = false)) + " روز انجام نشد" as false
FROM #journal
WHERE file.name >= ("{{اول سال}}") AND file.name <= ("{{آخر سال}}")
GROUP BY ""
```






