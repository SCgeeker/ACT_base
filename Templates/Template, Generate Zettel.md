<%*
// Template, Generate Zettel.md
// 觸發 zettel_wrapper.js 從知識庫生成 Zettel 原子卡片
const generateZettel = tp.user.zettel_wrapper;

// 執行完畢後刪除 Templater 自動建立的暫時筆記
tp.hooks.on_all_templates_executed(async () => {
    const file = app.vault.getAbstractFileByPath(tp.file.path(true));
    if (file) await app.vault.delete(file);
});

await generateZettel(tp);
tR = '';
%>
