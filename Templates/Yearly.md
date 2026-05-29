---
cssclasses:
  - cards
  - rtl-dataview
---

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
    "🏋️ " + length(filter(rows, (r) => r.🏋️exercise = true)) + " روز ورزش کــــردم" as true,
    "🛌 " + length(filter(rows, (r) => r.🏋️exercise = false)) + " روز استراحت کردم" as false
FROM #journal
WHERE file.name >= ("{{اول سال}}") AND file.name <= ("{{آخر سال}}")
GROUP BY ""
```


‌
## 📚 مطالعه

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
fillTheScreen: true
enableMainContainerShadow: false
fromDate: {{اول سال}}
toDate: {{آخر سال}}
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
    max: "999"
cellStyle:
  minWidth: 12px
  minHeight: 12px
mainContainerStyle:
  backgroundColor: "#ffffff00"

```

---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.📚reading)) + " پومودورو" as Total,
"🔺 بیشترین: " + round(max(rows.📚reading)) + " پومودورو" as Maximum,
"🔻 کمترین: " + round(min(rows.📚reading)) + " پومودورو" as Minimum,
"📈 میانگین: " + round(sum(rows.📚reading) / length(rows), 1) + " پومودورو" as Average
from #journal
where file.name >= ("{{اول سال}}") AND file.name <= ("{{آخر سال}}")
GROUP BY ""
```

---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: 📚reading
startDate: {{اول سال}}
endDate: {{آخر سال}}
folder: #journal
aspectRatio: 18:9
bar:
    title: " "
    xAxisLabel: " "
    yAxisLabel: " "
	yMin: 20
	yMax: 0
	barColor: "#ffa43d"
```
````


## 🌎 یادگیری زبان

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
    value: 🌎english
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
  minWidth: 12px
  minHeight: 12px
mainContainerStyle:
  backgroundColor: "#ffffff00"
```
---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.🌎english)) + " مورد" as Total,
"🔺 بیشترین: " + round(max(rows.🌎english)) + " مورد" as Maximum,
"🔻 کمترین: " + round(min(rows.🌎english)) + " مورد" as Minimum,
"📈 میانگین: " + round(sum(rows.🌎english) / length(rows), 1) + " مورد" as Average
from #journal
where file.name >= ("{{اول سال}}") AND file.name <= ("{{آخر سال}}")
GROUP BY ""
```
---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: 🌎english
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



‌‌ ‌
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
  minWidth: 12px
  minHeight: 12px
mainContainerStyle:
  backgroundColor: "#ffffff00"
```

---tab 🧮 آمار
```dataview
table without id
"🔘 جمع کل: " + round(sum(rows.📱social)) + " ساعت" as Total,
"🔺 بیشترین: " + round(max(rows.📱social)) + " ساعت" as Maximum,
"🔻 کمترین: " + round(min(rows.📱social)) + " ساعت" as Minimum,
"📈 میانگین: " + round(sum(rows.📱social) / length(rows), 1) + " ساعت" as Average
from #journal
where file.name >= ("{{اول سال}}") AND file.name <= ("{{آخر سال}}")
GROUP BY ""
```

---tab 📊 نمودار
``` tracker
searchType: frontmatter
searchTarget: 📱social
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
