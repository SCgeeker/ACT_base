<%*
// Template, Generate Slides.md
// 觸發 slides_wrapper.js 從 +/pdf/ 選擇 PDF 並生成投影片
const generateSlides = tp.user.slides_wrapper;

// 執行完畢後刪除 Templater 自動建立的暫時筆記
tp.hooks.on_all_templates_executed(async () => {
    const file = app.vault.getAbstractFileByPath(tp.file.path(true));
    if (file) await app.vault.delete(file);
});

await generateSlides(tp);
tR = '';
%>
