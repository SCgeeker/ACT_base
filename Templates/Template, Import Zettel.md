<%*
// Template, Import Zettel.md
// 觸發 import_wrapper.js 匯入 Zettelkasten，完成後開啟新建的 Annotation Note
const importZettel = tp.user.import_wrapper;
const notePath = await importZettel(tp);

// 刪除 QuickAdd 建立的暫時筆記
tp.hooks.on_all_templates_executed(async () => {
    const tmpFile = app.vault.getAbstractFileByPath(tp.file.path(true));
    if (tmpFile) await app.vault.delete(tmpFile);
});

if (notePath) {
    // 等待檔案系統寫入
    await new Promise(r => setTimeout(r, 800));

    const file = app.vault.getAbstractFileByPath(notePath);
    if (file) {
        await app.workspace.getLeaf().openFile(file);
    } else {
        new Notice(`找不到筆記: ${notePath}`);
    }
}

// 此模板不產生任何筆記內容
tR = '';
%>
