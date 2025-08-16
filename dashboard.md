```dataviewjs
/* ========================= CONFIG ========================= */
const CONFIG = {
  filters: {
    tags: ["journal"], // تگ یادداشت روزانه
    paths: []          // مسیر یادداشت روزانه
  },
  dateSource: {
    from: "filename", // "filename" یا "frontmatter"
    frontmatterField: "date", // نام فیلد تاریخ در frontmatter
    dateFormat: "YYYY/MM/DD" // فرمت تاریخ برای
  },
  habits: [
    {
      id: "exercise",
      title: "🏋️ ورزش",
      field: "🏋️exercise",
      type: "boolean",
      unit: null,
      progressMax: null,
      completeCondition: { kind: "eq", value: true },
      chain: { graceDays: 1, cupEvery: 15 },
      achievement: null
    },
    {
      id: "reading",
      title: "📚 مطالعه",
      field: "📚reading",
      type: "numeric",
      unit: "پومودورو",
      progressMax: 16,
      completeCondition: { kind: "gte", value: 1 },
      chain: { graceDays: 1, cupEvery: 15 },
      achievement: [
        { range: [10, 12], label: "🏅 سوپراستار" },
        { range: [7, 9],   label: "🥇 طلا" },
        { range: [4, 6],   label: "🥈 نقره" },
        { range: [1, 3],   label: "🥉 برنز" },
        { range: [0, 0],   label: "⚪" }
      ]
    },
    {
      id: "english",
      title: "🌎 یادگیری زبان",
      field: "🌎en",
      type: "numeric",
      unit: "پومودورو",
      progressMax: 8,
      completeCondition: { kind: "gte", value: 1 },
      chain: { graceDays: 1, cupEvery: 15 },
      achievement: [
        { range: [7, 8], label: "🏅 سوپراستار" },
        { range: [5, 6],   label: "🥇 طلا" },
        { range: [3, 4],   label: "🥈 نقره" },
        { range: [1, 2],   label: "🥉 برنز" },
        { range: [0, 0],   label: "⚪" }
      ]
    },
    {
      id: "social",
      title: "📱 سوشال مدیا",
      field: "📱social",
      type: "numeric",
      unit: "ساعت",
      progressMax: 12,
      completeCondition: { kind: "lte", value: 3 },
      chain: null,
      achievement: [
        { range: [0, 0],        label: "🏅 سوپراستار" },
        { range: [0, 1],        label: "🥇 طلا"   },
        { range: [0, 2],        label: "🥈 نقره"  },
        { range: [0, 3],        label: "🥉 برنز"  },
        { range: [4, Infinity], label: "⚪" }
      ],
      lowerIsBetter: true
    }
  ]
};
/* ======================= END CONFIG ======================= */

/* =================== STYLES (inject once) =================== */
(function injectStyles(){
  const ID = "habit-tracker-style-rtl-2col";
  if (document.getElementById(ID)) return;
  const s = document.createElement("style");
  s.id = ID;
  s.textContent = `
  .habit-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1.5rem;
    margin-top: 1rem;
    direction: rtl;
    text-align: right;
  }
  @media (max-width: 900px) {
    .habit-grid { grid-template-columns: 1fr; }
  }
  .h-card {
    border: 1px solid var(--background-modifier-border);
    border-radius: 14px;
    padding: 14px;
    background: var(--background-primary);
    box-shadow: 0 1px 6px rgba(0,0,0,0.06);
    display: flex;
    flex-direction: column;
    gap: 10px;
    transition: transform 0.15s ease, box-shadow 0.15s ease;
  }
  .h-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  }
  .h-title {
    font-weight: 700;
    font-size: 1.05rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .subtle { opacity: 0.75; font-size: 0.92rem; }
  .progress-wrap {
    width: 100%;
    height: 12px;
    border-radius: 999px;
    background: var(--background-modifier-form-field);
    overflow: hidden;
    border: 1px solid var(--background-modifier-border);
  }
  .progress-bar {
    height: 100%;
    transition: width 200ms ease;
  }
  .kpis {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 8px;
  }
  .kpi {
    padding: 8px;
    border-radius: 12px;
    background: var(--background-secondary);
    text-align: center;
    font-size: 0.9rem;
  }
  .kpi b { font-variant-numeric: tabular-nums; }
  .warning-message {
    background: rgba(237, 190, 11, 0.15);
    padding: 10px;
    border-radius: 8px;
    margin-bottom: 1rem;
    margin-top: 1rem;
    font-size: 0.95rem;
    display: flex;
    align-items: center;
    gap: 8px;
    direction: rtl;
  }
  `;
  document.head.appendChild(s);
})();

/* ====================== HELPERS ====================== */
const today = window.moment().startOf("day");
const todayISO = today.format("YYYY-MM-DD");

function parseDateFromFileName(name, page) {
  if (CONFIG.dateSource.from === "filename") {
    const m = String(name).match(/(\d{4}-\d{2}-\d{2})/);
    if (!m) {
      console.warn(`Invalid date in filename: ${name}`);
      return null;
    }
    const parsedDate = window.moment(m[1], CONFIG.dateSource.dateFormat);
    if (!parsedDate.isValid()) {
      console.warn(`Invalid date format in filename: ${name}, value: ${m[1]}`);
      return null;
    }
    return parsedDate.startOf("day");
  } else if (CONFIG.dateSource.from === "frontmatter") {
    const fmDate = getFieldValue(page, CONFIG.dateSource.frontmatterField);
    if (!fmDate) {
      console.warn(`No date found in frontmatter field '${CONFIG.dateSource.frontmatterField}' for page: ${page.file.path}`);
      return null;
    }
    const trimmedDate = String(fmDate).trim();
    const parsedDate = window.moment(trimmedDate, CONFIG.dateSource.dateFormat);
    if (!parsedDate.isValid()) {
      console.warn(`Invalid date format in frontmatter field '${CONFIG.dateSource.frontmatterField}' for page: ${page.file.path}, value: ${fmDate}`);
      return null;
    }
    return parsedDate.startOf("day");
  }
  console.warn(`Invalid dateSource.from: ${CONFIG.dateSource.from}`);
  return null;
}

function getFieldValue(page, key) {
  if (page?.[key] !== undefined) return page[key];
  if (page?.file?.frontmatter && key in page.file.frontmatter) return page.file.frontmatter[key];
  return undefined;
}

function isSuccessful(value, completeCondition) {
  if (value === undefined || value === null) return false;
  if (completeCondition.kind === "eq")  return value === completeCondition.value;
  const num = Number(value) || 0;
  if (completeCondition.kind === "gte") return num >= completeCondition.value;
  if (completeCondition.kind === "lte") return num <= completeCondition.value;
  return false;
}

function barColor(percent, lowerIsBetter=false) {
  const p = Math.max(0, Math.min(1, percent));
  if (lowerIsBetter) {
    const hue = 120 * (1 - p);
    return `hsl(${hue}, 70%, 48%)`;
  } else {
    return `hsl(120, 70%, ${85 - p * 40}%)`;
  }
}

function pickAchievement(value, achList) {
  if (!achList) return "—";
  for (const a of achList) {
    const [min, max] = a.range;
    if (value >= min && value <= max) return a.label;
  }
  return "—";
}

function toJalali(date) {
  return new Intl.DateTimeFormat("fa-IR", { year: "numeric", month: "2-digit", day: "2-digit" }).format(date.toDate());
}

function computeChainsWithDates(successDates, graceDays, cupEvery) {
  if (!successDates.length) return { current: 0, currentRange: null, longest: 0, longestRange: null, total: 0, cups: [] };
  successDates = successDates.filter(d => d.isSameOrBefore(today, "day")).sort((a,b)=>a - b);
  const maxGap = graceDays + 1;

  // longest
  let longest = 1, run = 1, longestStart = successDates[0], longestEnd = successDates[0], tempStart = successDates[0];
  for (let i = 1; i < successDates.length; i++) {
    const gap = successDates[i].diff(successDates[i-1], "days");
    if (gap <= maxGap) {
      run++;
      longestEnd = successDates[i];
    } else {
      if (run > longest) {
        longest = run;
        longestStart = tempStart;
        longestEnd = successDates[i-1];
      }
      run = 1;
      tempStart = successDates[i];
    }
  }
  if (run > longest) {
    longest = run;
    longestStart = tempStart;
    longestEnd = successDates[successDates.length-1];
  }

  // current
  let current = 1;
  let currentStart = successDates[successDates.length-1];
  for (let i = successDates.length-1; i > 0; i--) {
    const gap = successDates[i].diff(successDates[i-1], "days");
    if (gap <= maxGap) {
      current++;
      currentStart = successDates[i-1];
    } else break;
  }
  const lastGapToToday = today.diff(successDates[successDates.length-1], "days");
  if (lastGapToToday > maxGap) current = 0;

  // cups list
  let cups = [];
  if (cupEvery > 0) {
    let count = 0, start = successDates[0];
    for (let i = 0; i < successDates.length; i++) {
      count++;
      if (count === cupEvery) {
        cups.push({ num: cups.length + 1, start, end: successDates[i] });
        count = 0;
        start = successDates[i+1];
      }
    }
  }

  return { current, currentRange: current ? { start: currentStart, end: successDates[successDates.length-1] } : null,
           longest, longestRange: { start: longestStart, end: longestEnd }, total: successDates.length, cups };
}

/* =============== QUERY PAGES WITH FILTERS =============== */
let q = dv.pages();
if (CONFIG.filters.tags.length || CONFIG.filters.paths.length) {
  q = q.where(p => {
    const hasTags = CONFIG.filters.tags.length
      ? CONFIG.filters.tags.every(tag => p.file.tags.includes(`#${tag}`))
      : true;
    const hasPaths = CONFIG.filters.paths.length
      ? CONFIG.filters.paths.some(path => p.file.path.includes(path))
      : true;
    return hasTags && hasPaths;
  });
}
const allPages = q.array();

const dated = allPages.map(p => {
  const d = parseDateFromFileName(p.file.name, p);
  if (!d) return null;
  return { page: p, date: d, dateStr: d.format("YYYY-MM-DD") };
}).filter(Boolean);

// تعریف allDaysSorted قبل از استفاده
const allDaysSorted = dated.sort((a,b) => a.date - b.date);

const todayEntry = dated.find(x => x.dateStr === todayISO);
const todayPage = todayEntry?.page;

const root = dv.container.createDiv({ cls: "habit-grid" });
root.setAttr("dir", "rtl");

// اگر یادداشت امروز پیدا نشد، پیام هشدار را بالای کارت‌ها نمایش بده
if (!todayPage) {
  const warn = dv.container.createDiv({ cls: "warning-message" });
  warn.createSpan({ text: "⚠ یادداشت امروز پیدا نشد" });
  warn.createSpan({ cls: "subtle", text: `فایلی با تاریخ ${todayISO} و فیلترهای مشخص‌شده پیدا نشد.` });
}

// نمایش کارت‌های عادت‌ها
for (const habit of CONFIG.habits) {
  const card = root.createDiv({ cls: "h-card" });

  const rawToday = todayPage ? getFieldValue(todayPage, habit.field) : null;
  const todayVal = habit.type === "boolean" ? !!rawToday : Number(rawToday ?? 0);

  const medal = habit.type === "boolean"
    ? (todayVal ? "✅" : (todayPage ? "❌" : "—"))
    : (todayPage ? pickAchievement(todayVal, habit.achievement) : "—");

  const header = card.createDiv({ cls: "h-title" });
  header.createSpan({ text: habit.title });
  header.createSpan({ text: medal || "—", cls: "subtle" });

  if (habit.type === "boolean") {
    const wrap = card.createDiv({ cls: "progress-wrap" });
    const bar = wrap.createDiv({ cls: "progress-bar" });
    if (todayPage && todayVal) {
      bar.style.width = "100%";
      bar.style.background = "#22c55e";
    } else {
      bar.style.width = "0%";
    }
    card.createDiv({ cls: "subtle", text: todayPage
      ? `وضعیت امروز: ${todayVal ? "انجام شد ✅" : "انجام نشد ❌"}`
      : "امروز بدون داده" });
  } else {
    const max = Math.max(1, Number(habit.progressMax || 1));
    const pct = Math.max(0, Math.min(1, todayVal / max));
    const wrap = card.createDiv({ cls: "progress-wrap" });
    const bar = wrap.createDiv({ cls: "progress-bar" });
    bar.style.width = (todayPage && todayVal > 0) ? `${(pct*100).toFixed(0)}%` : "0%";
    if (todayPage && todayVal > 0) bar.style.background = barColor(pct, !!habit.lowerIsBetter);
    const unitLabel = habit.unit ? ` ${habit.unit}` : "";
    card.createDiv({ cls: "subtle", text: todayPage
      ? `وضعیت امروز: ${todayVal}${unitLabel}`
      : "امروز بدون داده" });
  }

  if (habit.chain) {
    const successDates = [];
    for (const {page, date} of allDaysSorted) {
      const v = getFieldValue(page, habit.field);
      const val = habit.type === "boolean" ? !!v : Number(v ?? 0);
      if (isSuccessful(val, habit.completeCondition)) successDates.push(date.clone());
    }

    const chainData = computeChainsWithDates(successDates, habit.chain.graceDays, habit.chain.cupEvery);
    const kpis = card.createDiv({ cls: "kpis" });

    const currentKPI = kpis.createDiv({ cls: "kpi" });
    currentKPI.innerHTML = `زنجیره فعلی<br><b>${chainData.current}</b> روز`;
    if (chainData.currentRange) {
      currentKPI.setAttr("title", `شروع: ${toJalali(chainData.currentRange.start)}\nپایان: ${toJalali(chainData.currentRange.end)}`);
    }

    const longestKPI = kpis.createDiv({ cls: "kpi" });
    longestKPI.innerHTML = `طولانی‌ترین<br><b>${chainData.longest}</b> روز`;
    if (chainData.longestRange) {
      longestKPI.setAttr("title", `شروع: ${toJalali(chainData.longestRange.start)}\nپایان: ${toJalali(chainData.longestRange.end)}`);
    }

    const cupsKPI = kpis.createDiv({ cls: "kpi" });
    cupsKPI.innerHTML = `مجموع کاپ‌ها<br><b>${chainData.cups.length}</b> 🏆`;
    if (chainData.cups.length) {
      cupsKPI.setAttr("title", chainData.cups.map(c => `${c.num}. ${toJalali(c.start)} تا ${toJalali(c.end)}`).join("\n"));
    }
  }
}
```
