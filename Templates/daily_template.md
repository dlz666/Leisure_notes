<%*
// 1. 【日期计算】
// 如果文件名是日期则使用文件名，否则默认为今天
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) date = moment();

// 获取显示用的日期字符串
let titleDate = date.format("dddd"); // 标题: Monday
let dayAbbr = date.clone().locale('en').format("ddd"); // 搜索用: Mon

// 获取本周一的日期，用于确定周计划文件名 (解决跨月问题)
let monday = date.clone().isoWeekday(1);
let weekName = monday.format("YYYY-MM-[W]WW"); // 例如: 2025-12-W52

// 2. 【读取周计划】
let planResult = `> ℹ️ *(${weekName} 无 ${dayAbbr} 安排)*`; // 默认提示
try {
    // 尝试查找文件 (Obsidian 会自动处理 md 后缀)
    let tFile = tp.file.find_tfile(`weekly_plan/${weekName}`);
    
    if (tFile) {
        let content = await app.vault.read(tFile);
        
        // 正则匹配: - **Mon:** 任意内容
        // 注意: 在 JS 字符串中写正则，反斜杠需要双写 (\\)
        let regex = new RegExp(`-\s*\*\*${dayAbbr}:\*\*\s*(.*)`, "i");
        let match = content.match(regex);
        
        if (match && match[1].trim()) {
            planResult = `> 📌 **周计划**: ${match[1].trim()}`;
        }
    } else {
        planResult = `> ⚠️ *未找到关联文件: weekly_plan/${weekName}*`;
    }
} catch (error) {
    planResult = `> ❌ *读取出错: ${error.message}*`;
}

// 3. 【输出内容】
// 使用 tR 变量将内容输出到笔记中
tR += `# ${titleDate}\n\n`;
tR += `🔗 **关联**: [[weekly_plan/${weekName}|📅 本周计划 (${weekName})]]\n\n`;
tR += `# 今日计划\n`;
tR += `${planResult}\n\n`;
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