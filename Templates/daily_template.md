<%* try { // --- 1. 初始化 --- let currentDate = moment(tp.file.title, "YYYY-MM-DD", true); if (!currentDate.isValid()) { currentDate = moment(); } let titleDate = currentDate.format("dddd"); // --- 2. 计算周计划路径 --- // 获取本周一的日期 (ISO周: 1=周一, 7=周日) let mondayDate = currentDate.clone().isoWeekday(1); let weekFileName = mondayDate.format("YYYY-MM-[W]WW"); // 显式加上 .md 后缀，提高查找成功率 let weeklyPlanPath = `weekly_plan/${weekFileName}.md`; // --- 3. 尝试读取内容 --- let dayAbbr = currentDate.clone().locale('en').format("ddd"); let planContent = ""; // 查找文件 let tFile = tp.file.find_tfile(weeklyPlanPath); // 如果找不到，尝试不带后缀再找一次 (兼容性) if (!tFile) { tFile = tp.file.find_tfile(`weekly_plan/${weekFileName}`); } if (tFile) { const fileContent = await app.vault.read(tFile); const regex = new RegExp(`-\s*\*\*${dayAbbr}:\*\*\s*(.*)`, "i"); const match = fileContent.match(regex); if (match && match[1].trim()) { planContent = match[1].trim(); } } // --- 4. 输出内容到笔记 --- tR += `# ${titleDate}\n\n`; tR += `🔗 **关联**: [[weekly_plan/${weekFileName}|📅 本周计划 (${weekFileName})]]\n\n`; tR += `# 今日计划\n`; if (planContent) { tR += `> 📌 **周计划**: ${planContent}\n`; } else { tR += `> ℹ️ *今日暂无周计划内容 (关联文件: ${weekFileName})*\n`; if (!tFile) { tR += `> ⚠️ *Debug: 未找到文件 ${weeklyPlanPath}*\n`; } } } catch (e) { // 捕获错误并显示，不再弹窗报错 tR += `\n> ❌ **Templater 脚本错误**: ${e.message}\n`; tR += `> ${e.stack}\n`; } 
%>

## 💻 CS 学习与开发
-
## ✅ 待办事项
- [ ] 跑步打卡
- [ ] 背单词打卡
- 作业
	- [ ] 作业1
	- [ ] 作业2
	- [ ] --
- [ ] 
## 📝 笔记与想法
### 
