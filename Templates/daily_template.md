 1 <%*
    2 try {
    3     tR += "## ⚙️ 环境诊断报告\n\n";
    4     let ok = true;
    5 
    6     if (typeof moment !== 'function') {
    7         tR += "> ❌ **失败**: `moment` 功能不可用。\n";
    8         ok = false;
    9     }
   10 
   11     if (typeof tp !== 'object' || tp === null) {
   12         tR += "> ❌ **失败**: `tp` (Templater 核心) 
      不可用。\n";
   13         ok = false;
   14     }
   15 
   16     if (typeof app !== 'object' || app === null) {
   17         tR += "> ❌ **失败**: `app` (Obsidian 核心) 
      不可用。\n";
   18         ok = false;
   19     }
   20 
   21     if (ok) {
   22         tR += "> ✅ **成功**: 所有核心功能 (`moment`, `tp`
      `app`) 均正常。\n\n";
   23         tR += 
      "这说明你的环境没有问题，错误出在之前的文件处理逻辑中。";
   24     } else {
   25         tR += "\n请将以上失败信息截图给我，这说明你的 
      Obsidian 环境或插件配置存在问题。";
   26     }
   27 
   28 } catch (e) {
   29     tR += `## ‼️ 
      致命错误\n脚本在诊断时就崩溃了。\n**错误信息**: 
      ${e.message}`;
   30 }
   31 %>
   32 
   33 ---
   34 如果能看到这段文字，说明模板的基本结构是正常的。