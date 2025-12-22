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
// 获取当前文件日期
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) date = moment();

// 1. 确保星期简写是英文 (Mon, Tue...) 以匹配周计划格式
let dayAbbr = date.locale('en').format("ddd");

// 2. 重新计算周文件名 (以周一所在月份为准)
let weekStr = date.clone().isoWeekday(1).format("YYYY-MM-[W]WW");
let weeklyPlanPath = `weekly_plan/${weekStr}`;
let tFile = tp.file.find_tfile(weeklyPlanPath);
let planContent = "";

if (tFile) {
    const fileContent = await app.vault.read(tFile);
    // 匹配: - **Mon:** 任意内容
    // 使用 multiline 模式，确保只匹配对应行
    const regex = new RegExp(`-\\s*\\*\\*${dayAbbr}:\\*\\*\\s*(.*)`, "i");
    const match = fileContent.match(regex);
    if (match && match[1].trim()) {
        planContent = match[1].trim();
    }
} else {
    // 调试信息：如果找不到文件，提示用户 (可选，正式版可去掉)
    // planContent = `(未找到周计划文件: ${weeklyPlanPath})`; 
}
%>
<% planContent ? `> 📌 **周计划**: ${planContent}` : "> ℹ️ *今日暂无周计划内容或未找到关联文件*" %>

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
