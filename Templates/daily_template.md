<%*
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) {
    date = moment();
}
// 格式化周数，例如 2025-W52
let weekStr = date.format("YYYY-[W]WW");
// 格式化显示的日期标题
let titleDate = date.format("YYYY-MM-DD dddd");
%>
# <% titleDate %>

🔗 **关联**: [[weekly_plan/<% weekStr %>|📅 本周计划 (<% weekStr %>)]]

## ✅ 待办事项
- [ ] jlKDJ

## 💻 CS 学习与开发
- 

## 📝 笔记与想法
- 
