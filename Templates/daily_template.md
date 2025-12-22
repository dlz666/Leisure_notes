<%*
// ==========================================
// 🛡️ 整合版脚本：一次性计算所有内容，确保稳定
// ==========================================

// 1. 初始化日期
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) date = moment();

// 2. 准备基础信息
let titleText = date.format("dddd"); // 标题 (e.g. Monday)
let dayKey = date.clone().locale('en').format("ddd"); // 搜索关键字 (e.g. Mon)

// 3. 计算周计划路径 (以周一所在月份为准)
let monday = date.clone().isoWeekday(1);
let weekFileName = monday.format("YYYY-MM-[W]WW"); // e.g. 2025-12-W52
let linkText = `[[weekly_plan/${weekFileName}|📅 本周计划 (${weekFileName})]]`;

// 4. 读取周计划内容
let planOutput = "";
let targetPath = `weekly_plan/${weekFileName}.md`;

try {
    // 查找文件 (先找带后缀的)
    let tFile = tp.file.find_tfile(targetPath);
    if (!tFile) {
        // 没找到再找不带后缀的
        tFile = tp.file.find_tfile(`weekly_plan/${weekFileName}`);
    }

    if (tFile) {
        // 读取文件
        let fileBody = await app.vault.read(tFile);
        
        // 正则匹配: "- **Mon:** 内容"
        let re = new RegExp(`-\s*\*\*${dayKey}:\*\*\s*(.*)`, "i");
        let found = fileBody.match(re);
        
        if (found && found[1] && found[1].trim()) {
            planOutput = `> 📌 **周计划**: ${found[1].trim()}`;
        } else {
            planOutput = `> ℹ️ *(${weekFileName} 中无 ${dayKey} 安排)*`;
        }
    } else {
        planOutput = `> ⚠️ **未找到文件**: \\`weekly_plan/${weekFileName}.md\\` `;
    }
} catch (err) {
    planOutput = `> ❌ **读取出错**: ${err.message}`;
}

// ==========================================
// 📝 输出最终 Markdown 内容
// ==========================================
tR += `# ${titleText}\n\n`;
tR += `🔗 **关联**: ${linkText}\n\n`;
tR += `# 今日计划\n`;
tR += `${planOutput}\n\n`;
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