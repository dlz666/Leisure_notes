<%*
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) {
    date = moment();
}
// 格式化周数，例如 2025-W52
let weekStr = date.format("YYYY-MM-[W]WW");
// 格式化显示的日期标题
let titleDate = date.format("dddd");
%> 
# <% titleDate %>

🔗 **关联**: [[weekly_plan/<% weekStr %>|📅 本周计划 (<% weekStr %>)]]

# 今日计划

## 💻 CS 学习与开发
- 
## ✅ 待办事项
- [ ] 跑步打卡
- [ ] 背单词打卡
- 作业
	- [ ] 作业1
	- [ ] 作业2
	- [ ] ---

## 📝 笔记与想法
### 
