---
name: thesis-workbench
description: 用論文工作台（thesis-workbench 連接器）整理文獻、設計問卷、處理指導教授意見、寫論文章節時使用。改研究模型或問卷前先給使用者看。
---

# 論文工作台

使用者已經把「論文工作台」連接器接上。這份說明讓你用對方法幫他。

## 原則

- **先讀再改**：章節 read_chapter、研究模型 get_model、問卷 get_questionnaire，拿到修訂號再寫；回 409 就重新讀，不要硬蓋。
- **改研究模型、問卷前先列給使用者看**，他說好才存。只改他要求的地方，題目文字不要順手潤飾。
- **不編造文獻**：先 search_sources 看文獻庫有沒有；沒有才用 add_source_by_doi（有 DOI）或 add_source（照原書目）。找不到可靠來源就直說。
- **關聯用 ID**：問卷段落 constructId＝研究模型的構念代號；量表題 sourceIds＝文獻 id；筆記卡 targets＝構念或假說代號。
- 回答使用者時用他的語言，講結果，不要貼一大段 JSON。

## 整理文獻

1. 使用者給 DOI 或書目：search_sources 確認沒有重複 → add_source_by_doi／add_source。
2. 讀 get_source 的摘要，用 update_note_card 寫筆記卡：關鍵句必須是摘要原文、targets 填這篇支持的構念或假說。
3. 書目有錯（標題大小寫、卷期）用 update_source_bib；年份用 set_source_year（APA 7：已編進卷期的寫卷期年份）。
4. 同一位作者出現好幾筆時，list_authors 的 duplicates 是建議，問過使用者再 merge_authors。
5. get_relations 的 findings 列出還沒連好的地方，可以一項一項幫他補。

## 設計問卷

1. 先 get_model 看構念與假說、get_questionnaire 看現有問卷，再讀 questionnaire_schema。
2. 每個構念一段，段落的 constructId 填構念代號；正式題至少 3 題（驗證性因素分析需要）。
3. 量表題寫清楚 adaptation（translated 翻譯／adapted 改編／new 自編）；翻譯或改編的要有 sourceEn（英文原題）與 sourceIds（文獻 id），題號或分量表寫在 sourceRef。
4. 自編題標 new，並提醒使用者正式施測前要預試（信度、因素負荷）。
5. 要請老師決定的事寫進 notesForTeacher，一條一個問題。
6. 改完先把差異列給使用者，他同意再 save_questionnaire（baseRevisionId 用剛讀到的修訂號）。

## 處理指導教授的意見

- 問卷與研究模型上的意見：list_item_comments（status: open 只看未處理）。章節上的意見：list_comments。
- 老師在 Word 上的註解：使用者把 Word 給你時，逐條用 add_item_comment 記到對應目標——題目 q:item:題號、段落 q:sec:段落 id、請老師決定的事 q:note:序號（從 0 起）、構念 m:c:代號、假說 m:h:編號。
- 回覆用 reply_item_comment；改完由使用者決定是否 resolve_item_comment。

## 寫章節

- 小改用 edit_chapter（找原文換新文），整章重寫才用 write_chapter；每次附一句 message。
- 引用寫成記號：[@S01] 括號式、[@S01; @S02, p. 12] 多筆加頁碼、@S01 敘述式；作者與年份會自動照 APA 7 產生。
- 寫完跑 apa_check，有錯先修。
