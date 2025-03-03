# Branch 規範

- 採用 feature branch 進行開發
- Branch merge後要定期清除
- $type/$project-$ticket-id/$branch-name
    - $type 是遵循 [Conventional Commits](https://www.conventionalcommits.org/zh-hant/v1.0.0-beta.4/) 的 type 。
    - $project-$ticket-id 要對應專案中開的票號，如果沒有票，則省略。
    - $branch-name 的每個字是用 hyphen(-) 隔開。
    - 全小寫。
    - Examples:
        - feat/xx-1/backstage-header
        - fix/xx-2/button-is-missing
        - chore/xx-3/adjust-gitlab-ci

# Pull Request (PR)

- 發PR後的Merge須依照規範命名標題及填寫內容
- PR標題規則：`[PR 類型 ticke_id] PR 標題`
- ex: [Feature XX-90] 新增某個新功能

  PR 類型包括如下

  | 類型 | 範例 |
  | --- | --- |
  | BugFix | [BugFix] 修正某個壞掉的功能 |
  | HotFix | [HotFix] 緊急修正某個奇怪的東西 |
  | CS | [CS] 修正 Coding Style |
  | Feature | [Feature] 寫了某個新功能 |
  | Update | [Update] 改了某個文字檔 |
  | Refactor | [Refactor] 重構了某個功能 |
- PR內容：依範本內容填寫
- PR標題規則：[PR 類型 ticket id] PR 標題
- 如何預設新專案的PR範本：新專案建立後，在專案根目錄底下新增 `.github` 資料夾，裡面加入 `pull_request_template.md` 檔案(不可改檔名)，並加入預設範本，發 PR 並 merge 到 base(main / master)
- 詳細教學參考：[連結](https://riverye.com/2020/07/11/%E5%A6%82%E4%BD%95%E8%AE%93-GitHub-%E6%AF%8F%E5%80%8B-pull-request-PR-%E6%9C%89%E9%A0%90%E8%A8%AD%E6%A8%A1%E6%9D%BF/)

# Commit 規範

- https://chris.beams.io/posts/git-commit/
- 每個 commit 做一件事
- 如果 commit 內有包含跟這個 commit 無關的修正，應該要切出去
- 可用中文，如為英文則全小寫
- 使用祈使句，例如“add feature”而不是“added feature”或“adding feature”。
- 我們採用 [Conventional Commits](https://www.conventionalcommits.org/zh-hant/v1.0.0-beta.4/)
  - （自行決定是否加 scope）提交的類型可以在括號內給予作用範圍，以提供額外的脈絡資訊。
  - Examples:
    - feat: 購物車
    - fix: 修正登入錯誤
    - 新增功能 => feat(auth): add login functionality
    - 修復 bug => fix(button): correct misaligned text
    - 更新文檔 => docs(readme): update installation instructions
    - 性能改進 => perf(image): improve image loading time
    - 重構代碼 => refactor(api): simplify request handling
  - 前綴 build, chore, ci, docs, feat, fix, perf, refactor, revert, style, test, infra(可參考下方類型說明)

## 常用類型參考

- build：影響構建系統或外部依賴項的變更（例如：gulp、broccoli、npm）
- chore：套件變動，例如，更新依賴庫、調整構建流程、增加或更新文檔生成邏輯等。
- ci：持續整合相關的變更（例如：Travis, Circle, BrowserStack, SauceLabs）
- docs：描述與文檔相關的變更，例如，更新文件內容、改進文檔結構、翻譯文檔、補充說明等。
- feat：新增功能，描述新增的功能或功能性的改進，添加一個新的功能、引入新的功能模組、或增強現有功能等。
- fix：修復 bug，添修正程式碼中的錯誤、修復應用程式的漏洞或問題等。
- perf：改進性能的變更，描述針對程式碼性能的改進，例如：優化算法、減少運算時間、減少記憶體使用等。
- refactor：既不修復 bug 也不新增功能的代碼更改，描述重構程式碼的提交，不包含新增功能或修復錯誤。重構是改進程式碼設計， 但不改變其外部行為。
- revert：恢復先前的提交
- style：不影響代碼含義的變更，描述對程式碼格式的調整，如空格、縮排、拼寫錯誤等。通常不會對程式碼的功能進行更改，僅專注於代碼的格式化和視覺風格。
- test：新增或修正測試，描述與測試相關的變更，包括新增測試、修改測試、測試用例的重構等。測試用例的增加和維護有助於確保程式碼的品質和穩定性。
- infra：基礎設施相關變更

## 使用方向舉例

目前有master (正式)/ develop(測試)/ feature(功能)/ fix(bug）
- 當你有新需求：會從develop拉一條分支出來例如feature/abc，處理完畢後將feature/abc推至remote並發起PR到develop
- 當feature/abc有問題需要修正: 不用從其他develop再次拉分支，可由原feature/abc分支繼續處理，因為commit可以一直下，所以改完後下commit後在push上去就可以
- 由feature/abc衍生的新需求：如果github尚未merge到develop，這時候可由feature/abc拉分支出去例如feature/123處理，處理完後推至remote並發起PR到develop，後續流程都跟前面一樣
- 測試完後推正式：這時候直接develop發PR置master
- 有bug要處理：如果今天bug不是很嚴重，可由develop拉分支處理例如fix/bug，處理完後推至remote並發起PR到develop
- 非常緊急bug：嚴重bug，由master拉分支出來處理例如hotfix/bug，完成後發PR到master以及develop（確保一致）

# 強制同步遠端

先取回遠端數據庫的最新歷史紀錄
git fetch --all

然後放棄目前所有檔案與 commit，還原成遠端版本
git reset --hard origin/xxx

最後重新拉回來
git pull origin master