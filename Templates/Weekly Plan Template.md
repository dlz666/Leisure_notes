<%*
  // 自动计算本周的起始和结束日期
  let startOfWeek = tp.date.weekday("YYYY-MM-DD", 0);
  let endOfWeek = tp.date.weekday("YYYY-MM-DD", 6);
  let weekNum = tp.date.now("WW");
%>
# 🗓️ Weekly Plan: W<% weekNum %> (<% startOfWeek %> ~ <% endOfWeek %>)

> "The key is not to prioritize what's on your schedule, but to schedule your priorities." — Stephen Covey

## 1. 🧭 指南针：以终为始

- **🔗 我的使命宣言：** [[My_Mission_Statement]] 
- **🎯 本周核心意图 (One Word)：** <% tp.file.cursor() %>

---

## 2. 磨刀：不断更新)

| 维度         | 目标              | 具体安排             |
| :--------- | :-------------- | :--------------- |
| **💪 身体**  | (e.g. 睡眠充足, 运动) | 每天 23:30 睡, 每天打卡 |
| **🧘 精神 ** | (e.g. 冥想, 独处)   | 每天 NSDR 20分钟     |
| **🧠 心智**  | (e.g. 课外阅读)     | 读《黑客与画家》, 写周复盘   |


---

## 3. 🎭 Roles & Big Rocks 

### 🎓 角色 A: 浙大CS学生 (绩点/基础)
- [ ] 🪨 Big Rock: 
- [ ] 🪨 Big Rock: 

### ⚔️ 角色 B: 算法竞赛选手
- [ ] 🪨 Big Rock: 

### 🛠️ 角色 C: 项目工程师
- [ ] 🪨 Big Rock: 

### 👤 角色 D: 系统管理员 
*(包括整理 Obsidian, 财务, 杂务)*
- [ ] 🪨 Big Rock: 

---

## 4. 📅 The Week Ahead 

- **Mon:** 
- **Tue:**
- **Wed:**
- **Thu:** 
- **Fri:**  
- **Sat:** 
- **Sun:** 
---

## 5. 🔄 Review 
- 🌹 **高光时刻 (Highlights):** 
- 🚧 **未完成/障碍 (Blockers):** 
- 💡 **下周改进 (Action Items):** 
- 📉 **身心状态指数 (1-10):** 

---
