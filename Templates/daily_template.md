<%*
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) {
    date = moment();
}
// 格式化周数，以周一所在月份为准，避免跨月文件名不一致
let weekStr = date.clone().isoWeekday(1).format("YYYY-MM-[W]WW");
// 格式化显示的日期标题
let titleDate = date.format("dddd");
%> 
# <% titleDate %>

🔗 **关联**: [[weekly_plan/<% weekStr %>|📅 本周计划 (<% weekStr %>)]]

# 今日计划
<%*
// 尝试从周计划中获取今日安排
let dayAbbr = date.format("ddd");
let weeklyPlanPath = `weekly_plan/${weekStr}`;
let tFile = tp.file.find_tfile(weeklyPlanPath);
let planContent = "";

if (tFile) {
    const fileContent = await app.vault.read(tFile);
    // 匹配格式: - **Mon:** 计划内容
    const regex = new RegExp(`-\\s*\\*\\*${dayAbbr}:\\*\\*\\s*(.*)`, "i");
    const match = fileContent.match(regex);
    if (match && match[1].trim()) {
        planContent = match[1].trim();
    }
}
%>
<% planContent ? `> 📌 **周计划安排**: ${planContent}` : "" %>

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
