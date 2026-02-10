---
cssclasses:
  - border-tab
  - cards
  - rtl-dataview
---
➕new


## هفتگی

````tabs

---tab 📅 تقویم
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
    value: ➕new
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
---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.➕new)) + " مورد" as Total,
"🔺 بیشترین: " + round(max(rows.➕new)) + " مورد" as Maximum,
"🔻 کمترین: " + round(min(rows.➕new)) + " مورد" as Minimum,
"📈 میانگین: " + round(sum(rows.➕new) / length(rows), 1) + " مورد" as Average
from #journal
where date >= date("{{اول هفته}}") AND date <= date("{{آخر هفته}}")
GROUP BY ""
```
---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: ➕new
startDate: {{اول هفته}}
endDate: {{آخر هفته}}
folder: #journal
aspectRatio: 16:9
bar:
    title: " "
    xAxisLabel: " "
    yAxisLabel: " "
	yMin: 8
	yMax: 0
	barColor: "#63b2f5"
```
````



## ماهانه

````tabs

---tab 📅 تقویم
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
    value: ➕new
fillTheScreen: false
enableMainContainerShadow: false
fromDate: {{اول ماه}}
toDate: {{آخر ماه}}
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
---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.➕new)) + " مورد" as Total,
"🔺 بیشترین: " + round(max(rows.➕new)) + " مورد" as Maximum,
"🔻 کمترین: " + round(min(rows.➕new)) + " مورد" as Minimum,
"📈 میانگین: " + round(sum(rows.➕new) / length(rows), 1) + " مورد" as Average
from #journal
where file.name >= ("{{اول ماه}}") AND file.name <= ("{{آخر ماه}}")
GROUP BY ""
```
---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: ➕new
startDate: {{اول ماه}}
endDate: {{آخر ماه}}
folder: #journal
aspectRatio: 16:9
bar:
    title: " "
    xAxisLabel: " "
    yAxisLabel: " "
	yMin: 8
	yMax: 0
	barColor: "#63b2f5"
```
````

## فصل

````tabs

---tab 📅 تقویم
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
    value: ➕new
fillTheScreen: false
enableMainContainerShadow: false
fromDate: {{اول فصل}}
toDate: {{آخر فصل}}
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
---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.➕new)) + " مورد" as Total,
"🔺 بیشترین: " + round(max(rows.➕new)) + " مورد" as Maximum,
"🔻 کمترین: " + round(min(rows.➕new)) + " مورد" as Minimum,
"📈 میانگین: " + round(sum(rows.➕new) / length(rows), 1) + " مورد" as Average
from #journal
where file.name >= ("{{اول فصل}}") AND file.name <= ("{{آخر فصل}}")
GROUP BY ""
```
---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: ➕new
startDate: {{اول فصل}}
endDate: {{آخر فصل}}
folder: #journal
aspectRatio: 16:9
bar:
    title: " "
    xAxisLabel: " "
    yAxisLabel: " "
	yMin: 8
	yMax: 0
	barColor: "#63b2f5"
```
````




## سالانه

````tabs

---tab 📅 تقویم
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
    value: ➕new
fillTheScreen: true
enableMainContainerShadow: false
fromDate: {{اول سال}}
toDate: {{آخر سال}}
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
cellStyle:
mainContainerStyle:
  backgroundColor: "#ffffff00"
```
---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.➕new)) + " مورد" as Total,
"🔺 بیشترین: " + round(max(rows.➕new)) + " مورد" as Maximum,
"🔻 کمترین: " + round(min(rows.➕new)) + " مورد" as Minimum,
"📈 میانگین: " + round(sum(rows.➕new) / length(rows), 1) + " مورد" as Average
from #journal
where file.name >= ("{{اول سال}}") AND file.name <= ("{{آخر سال}}")
GROUP BY ""
```
---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: ➕new
startDate: {{اول سال}}
endDate: {{آخر سال}}
folder: #journal
aspectRatio: 18:9
bar:
    title: " "
    xAxisLabel: " "
    yAxisLabel: " "
	yMin: 8
	yMax: 0
	barColor: "#63b2f5"
```
````








