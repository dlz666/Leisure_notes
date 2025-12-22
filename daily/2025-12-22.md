<%*
// ==========================================
// 🛡️ 最终稳定版：无正则匹配，纯字符串处理
// ==========================================

// 1. 初始化
let date = moment(tp.file.title, "YYYY-MM-DD", true);
if (!date.isValid()) date = moment();

let titleText = date.format("dddd");
let dayKey = date.clone().locale('en').format("ddd"); // e.g. "Mon"
let searchKey = `- **${dayKey}:**`; // 目标字符串: "- **Mon:**"

// 2. 计算周计划文件名
let monday = date.clone().isoWeekday(1);
let weekFileName = monday.format("YYYY-MM-[W]WW"); 
let linkText = `[[weekly_plan/${weekFileName}|📅 本周计划 (${weekFileName})]]`;

// 3. 读取内容
let planOutput = "";
let targetPath = `weekly_plan/${weekFileName}.md`;

try {
    let tFile = tp.file.find_tfile(targetPath);
    if (!tFile) tFile = tp.file.find_tfile(`weekly_plan/${weekFileName}`);

    if (tFile) {
        let fileBody = await app.vault.read(tFile);
        let lines = fileBody.split("\n");
        let foundLine = lines.find(line => line.toLowerCase().includes(searchKey.toLowerCase()));

        if (foundLine) {
            // 截取冒号后面的内容
            // 格式: - **Mon:** 内容
            let parts = foundLine.split(":**");
            if (parts.length > 1) {
                let content = parts[1].trim();
                if (content) {
                    planOutput = `> 📌 **周计划**: ${content}`;
                } else {
                    planOutput = `> ℹ️ *(${dayKey} 暂无内容)*`;
                }
            }
        } else {
            planOutput = `> ℹ️ *(${weekFileName} 中未找到 ${dayKey} 条目)*`;
        }
    } else {
        planOutput = `> ⚠️ **未找到文件**: 
${weekFileName}
``;
    }
} catch (err) {
    planOutput = `> ❌ **读取出错**: ${err.message}`;
}

// 4. 输出
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
