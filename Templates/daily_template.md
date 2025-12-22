<%*
// [全局配置] 获取当前笔记的日期对象
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) date = moment();
%>
# <% date.format("dddd") %>

<%*
// [区块1] 生成周计划关联链接
// 逻辑：找到本周一 -> 获取其月份和周号 -> 拼接文件名
let monday = date.clone().isoWeekday(1);
let weekName = monday.format("YYYY-MM-[W]WW");
let linkText = `[[weekly_plan/${weekName}|📅 本周计划 (${weekName})]]`;
tR += `🔗 **关联**: ${linkText}`;
%>

# 今日计划
<%*
// [区块2] 读取并显示今日安排
try {
    // 1. 再次计算路径 (确保独立性，防止变量冲突)
    let m = date.clone().isoWeekday(1);
    let targetFileName = m.format("YYYY-MM-[W]WW");
    let targetPath = `weekly_plan/${targetFileName}.md`;
    
    // 2. 准备匹配信息
    let dayKey = date.locale('en').format("ddd"); // "Mon", "Tue"...
    let content = "";
    
    // 3. 查找并读取文件
    // 优先尝试带 .md 后缀
    let tFile = tp.file.find_tfile(targetPath);
    // 备用：尝试不带后缀
    if (!tFile) tFile = tp.file.find_tfile(`weekly_plan/${targetFileName}`);
    
    if (tFile) {
        let fileBody = await app.vault.read(tFile);
        // 正则匹配: "- **Mon:** 内容"
        // 解释: 
        // - \s* 允许前面有空格
        // \*\* 匹配加粗标记
        // (.*) 捕获后面的内容
        let re = new RegExp(`-\s*\*\*${dayKey}:\*\*\s*(.*)`, "i");
        let found = fileBody.match(re);
        if (found && found[1]) {
            content = found[1].trim();
        }
    }
    
    // 4. 输出结果
    if (content) {
        tR += `> 📌 **周计划**: ${content}`;
    } else {
        // 如果没找到内容，显示一行灰色的小字提示，方便确认脚本运行正常
        tR += `> ℹ️ *(${targetFileName} 中无 ${dayKey} 安排)*`;
    }
} catch (err) {
    tR += `> ⚠️ 读取周计划出错`;
}
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