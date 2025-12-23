<%*
// 1. 【日期计算】
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) date = moment();

let titleDate = date.format("dddd"); // 标题: Monday
let dayAbbr = date.clone().locale('en').format("ddd"); // Mon
let targetKey = `- **${dayAbbr}:**`; // 目标字符串: "- **Mon:**"

// 2. 【计算文件名】
let monday = date.clone().isoWeekday(1);
let weekName = monday.format("YYYY-MM-[W]WW"); 

// 3. 【读取周计划】
let planResult = `> ℹ️ *(${weekName} 无 ${dayAbbr} 安排)*`;

try {
    let tFile = tp.file.find_tfile(`weekly_plan/${weekName}`);
    
    if (tFile) {
        let content = await app.vault.read(tFile);
        
        // --- 核心修改：使用 split 行处理，完全避开正则转义问题 ---
        let lines = content.split("\n");
        let foundLine = lines.find(line => line.includes(targetKey));
        
        if (foundLine) {
            // 截取目标字符串之后的部分
            // 例如 foundLine 是 "- **Mon:** 跑步"
            // 分割后 parts[1] 就是 " 跑步"
            let parts = foundLine.split(targetKey);
            
            if (parts.length > 1 && parts[1].trim()) {
                planResult = `> 📌 **周计划**: ${parts[1].trim()}`;
            }
        }
    } else {
        planResult = `> ⚠️ *未找到关联文件: weekly_plan/${weekName}*`;
    }
} catch (error) {
    planResult = `> ❌ *读取出错: ${error.message}*`;
}

// 4. 【输出】
tR += `# ${titleDate}\n\n`;
tR += '今天状态打几分?\n'
tR += `🔗 **关联**: [[weekly_plan/${weekName}|📅 本周计划 (${weekName})]]\n\n`;
tR += `# 今日计划\n`;
tR += `${planResult}\n\n`;
%> 
## 💻 CS 学习与开发
- 
## ✅ 待办事项
- [ ] 跑步打卡
- [ ] 背单词打卡
- 任务
	- [ ] 
- 琐事
	- [ ] 
## 📝 笔记与想法
### 
