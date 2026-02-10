---
cssclasses:
  - cards
  - rtl-dataview
  - border-tab
---

# {{نام فصل یادداشت}}

## 🏋️ ورزش


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
    value: 🏋️exercise
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
table without id
"✅ این فصل: " + length(rows) + " روز ورزش کردم" as Exercise
from #journal
where file.name >= ("{{اول فصل}}") AND file.name <= ("{{آخر فصل}}") And 🏋️exercise
GROUP BY ""
```


‌
## 📚 مطالعه

````tabs

---tab 📅 تقویم
```contributionGraph
title: ""
graphType: default
dateRangeValue: 30
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
    value: 📚reading
fillTheScreen: false
enableMainContainerShadow: false
fromDate: {{اول فصل}}
toDate: {{آخر فصل}}
cellStyleRules:
  - id: Halloween_a
    color: "#fdd577"
    min: 1
    max: "5"
  - id: Halloween_b
    color: "#faaa53"
    min: "5"
    max: "10"
  - id: Halloween_c
    color: "#f07c44"
    min: "10"
    max: "15"
  - id: Halloween_d
    color: "#d94e49"
    min: "15"
    max: 9999
cellStyle:
  minWidth: 20px
  minHeight: 20px
  borderRadius: ""
mainContainerStyle:
  backgroundColor: "#ffffff00"

```

---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.📚reading)) + " پ" as Total,
"🔺 بیشترین: " + round(max(rows.📚reading)) + " پ" as Maximum,
"🔻 کمترین: " + round(min(rows.📚reading)) + " پ" as Minimum,
"📈 میانگین: " + round(sum(rows.📚reading) / length(rows), 1) + " پ" as Average
from #journal
where file.name >= ("{{اول فصل}}") AND file.name <= ("{{آخر فصل}}")
GROUP BY ""
```

---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: 📚reading
startDate: {{اول فصل}}
endDate: {{آخر فصل}}
folder: #journal
aspectRatio: 16:9
bar:
    title: " "
    xAxisLabel: " "
    yAxisLabel: " "
	yMin: 18
	yMax: 0
	barColor: "#ffa43d"
```
````

‌
## 📱 سوشال مدیا

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
    value: 📱social
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
"🔘 جمع کل: " + round(sum(rows.📱social)) + " ساعت" as Total,
"🔺 بیشترین: " + round(max(rows.📱social)) + " ساعت" as Maximum,
"🔻 کمترین: " + round(min(rows.📱social)) + " ساعت" as Minimum,
"📈 میانگین: " + round(sum(rows.📱social) / length(rows), 1) + " ساعت" as Average
from #journal
where file.name >= ("{{اول فصل}}") AND file.name <= ("{{آخر فصل}}")
GROUP BY ""
```

---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: 📱social
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





