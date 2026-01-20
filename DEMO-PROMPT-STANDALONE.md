---
source-git-commit: 65d223acd23f26bd9c6979d11815d23f02ae2382
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---
# 🚀 デモプロンプト - v7 から v8 ドキュメントの分析

**このプロンプト全体をコピーして Cursor/ChatGPT に貼り付け、v7 フォルダーを分析します**

&#x200B;---

## 「（ここ 📋 からコピー）」というプロンプトを ⬇️ きます。

```markdown
# Campaign v7 Documentation Analysis

Analyze the v7 documentation folder and generate a detailed Markdown report with recommendations.

---

## CONTEXT

**v7 Repository**: `/Users/florentvignes/Documents/GitHub/campaign-classic.en/`  
**v8 Repositories**:
- `/Users/florentvignes/Documents/GitHub/campaign.en/` (Campaign v8)
- `/Users/florentvignes/Documents/GitHub/campaign-web.en/` (Campaign Web UI v8)

---

## TARGET FOLDER

**Analyze this folder**: `/Users/florentvignes/Documents/GitHub/campaign-classic.en/help/delivery/using/`

*(Replace with any folder: workflow, web, platform, reporting, etc.)*

---

## FEATURE PARITY CONTEXT

### v7-Specific Features (NOT in v8 FFDA)
- **Coupons** (personalized-coupons.md)
- **MRM** (Marketing Resource Management)
- **Surveys** (online surveys)
- **Distributed Marketing**
- **Mid-sourcing** (on-premise setup)
- **SpamAssassin** (on-premise spam filtering)
- **On-premise/Hybrid** configurations

### v8 Documentation Structure
- **Campaign Web UI**: `/campaign-web.en/help/v8/` - https://experienceleague.adobe.com/en/docs/campaign-web/v8/
- **Campaign v8**: `/campaign.en/help/v8/` - https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/

---

## OUTPUT FORMAT

Generate a complete Markdown report with this structure:

### 1. HEADER & SUMMARY
\`\`\`markdown
# 📊 v7 [Folder Name] Analysis

**Folder**: `/help/[folder]/using/`  
**Generated**: [Date]  
**Total Files**: [X]

## 📈 Summary

| Metric | Count | Percentage |
|--------|-------|------------|
| 📄 Total Files | X | 100% |
| ✅ KEEP | X | X% |
| 🗑️ DELETE | X | X% |
| ➡️ MOVE | X | X% |
| 🔍 REVIEW | X | X% |
\`\`\`

### 2. FILE-BY-FILE ANALYSIS TABLE
\`\`\`markdown
## 📋 Complete File Analysis

### [Category Name] (X files)

| # | v7 File | v8 Match | Match % | Notes | Action |
|---|---------|----------|---------|-------|--------|
| 1 | filename.md | [v8 link](https://...) | 95% | Fully in v8 | 🗑️ DELETE |
| 2 | **filename.md** | NONE | 0% | **v7-specific** | ✅ **KEEP** |
| 3 | filename.md | [v8 link](https://...) | 70% | Migrate tips | ➡️ MOVE |

[Repeat for each category: Get Started, Email, SMS, etc.]
\`\`\`

### 3. MUST KEEP SECTION
\`\`\`markdown
## ✅ Must Keep - v7-Specific Features

| File | Reason | Badge Text |
|------|--------|------------|
| filename.md | Feature not in v8 FFDA | "This feature is not available..." |
\`\`\`

### 4. QUICK WINS SECTION
\`\`\`markdown
## 🗑️ Quick Wins - Safe to Delete Now

**[Category]** (X files):
- ✅ filename.md → 95% in v8/path
- ✅ filename.md → 90% in v8/path
\`\`\`

### 5. MIGRATION SECTION
\`\`\`markdown
## ➡️ Content to Migrate First

| v7 File | v8 Destination | Content to Migrate | Effort |
|---------|----------------|-------------------|--------|
| filename.md | /v8/path.md | Sections X, Y, Z | 2 hours |
\`\`\`

### 6. EXECUTION PLAN
\`\`\`markdown
## 🎯 Execution Plan

### Week 1: Quick Deletions
- [ ] Delete [category] files (X)
- [ ] Delete [category] files (X)
**Total**: X files deleted

### Week 2: Badging
- [ ] Badge v7-specific files (X)

### Week 3: Review
- [ ] Review partial matches (X)
\`\`\`

---

## ANALYSIS RULES

### For Each File, Determine:

1. **Match Percentage**:
   - 95-100% = Fully covered in v8 → DELETE
   - 70-90% = Mostly covered, check gaps → DELETE or MOVE
   - 40-70% = Partial coverage → REVIEW
   - 0-40% = Not in v8 → KEEP or REVIEW

2. **v7-Specific Indicators** (→ KEEP):
   - Mentions "on-premise", "hybrid", "mid-sourcing"
   - Coupons, MRM, Surveys, Distributed Marketing
   - SpamAssassin, nlserver configuration
   - Client Console specific features
   - Database schema/structure docs

3. **DELETE Criteria**:
   - Basic features (email, SMS, push creation)
   - Standard workflow activities (query, split, enrichment)
   - Common reports
   - Channel basics fully documented in v8

4. **MOVE Criteria**:
   - Troubleshooting tips not in v8
   - Best practices missing in v8
   - Advanced patterns useful for v8
   - Good examples/use cases

5. **REVIEW Criteria**:
   - Partial v8 coverage (50-70%)
   - Unclear if feature exists in v8
   - Complex mixed content

---

## IMPORTANT

- **Organize by category** (Get Started, Email, SMS, Push, etc.)
- **Include Experience League URLs** for v8 matches
- **Bold v7-specific files** that must be kept
- **Estimate match percentage** for each file
- **Provide clear reasoning** for each decision
- **Include effort estimates** for migrations

---

Generate the complete Markdown report now.
```

&#x200B;---

## 🎯 デモの手順

### 手順 1：プロンプトの表示1. このファイルを開く（`DEMO-PROMPT-STANDALONE.md`）2. 「プロンプト」セクションまでスクロールします3. 例：*「これは、自動分析プロンプトです」*

### 手順 2：プロンプトのコピー1. 「# Campaign v7 ドキュメント分析」から最後まですべてを選択2. クリップボードにコピー3. 例えば、「*プロンプト全体をコピーするだけです…」と言いま*。

### 手順 3：貼り付けて実行1. カーソルを開く2. プロンプトをペーストします。3. 例えば、「*」と入力し、カーソルに貼り付けます*4. Enter キーを押す

### 手順 4：結果の表示1. 生成を待機（約 30～60 秒）2. 生成されたレポートをスクロールする3. 主要なセクションをハイライト表示：   - 📊 概要統計   - 📋 ファイルごとのテーブル   - ✅ Must Keep セクション   - 🗑️ Quick Wins   - 🎯 実行計画

### ステップ 5：うわーモーメント1. Markdown プレビューを表示2. 以下を指摘してください。   - *「111 個のファイルが自動的に分析されました」*   - *「67 個のファイルを安全に削除（60% 削減）」*   - *「18 v7 固有のファイルが特定されました」*   - *「タイムラインを使用した実行プランの完了」*

&#x200B;---

## 💡 デモのヒント

### インタラクティブにする&#x200B;**オーディエンスに尋ねる**:*「分析するフォルダーはどれか」*- 配信 ✅ （111 個のファイル – 印象的）- ワークフロー ✅ （121 個のファイル – さらに大きい）- web ✅ （26 個のファイル – クイックデモ）- レポート ✅ （32 個のファイル – 高速）

### その場でカスタマイズ&#x200B;**柔軟性を表示**：プロンプトでフォルダーパスを変更します。

```
/help/workflow/using/  → Analyze workflows
/help/web/using/       → Analyze web apps
/help/platform/using/  → Analyze platform
```

### 主な機能をハイライト1. **自動化**:*「手作業は不要」*2. **精度**:*「比較に v8 ドキュメントを使用」*3. **アクションにつながる**:*「チェックボックスを使用してすぐに実行できるプラン」*4. **スマート**:*「v7 固有の機能を自動的に識別」*

### 時間比較&#x200B;**前**:*「手動分析= フォルダーあたり 2～3 日」*\**後**:*「自動分析= フォルダーあたり 30 秒」*

**ROI**:*「21 個のフォルダー× 2 日= 42 日→ 15 分」*

&#x200B;---

## 期待 📊 れる出力プレビュー

```markdown
# 📊 v7 Delivery Analysis

**Total Files**: 111

## 📈 Summary
| Metric | Count | Percentage |
|--------|-------|------------|
| ✅ KEEP | 18 | 16% |
| 🗑️ DELETE | 67 | 60% |
| ➡️ MOVE | 8 | 7% |
| 🔍 REVIEW | 18 | 17% |

## 📋 File Analysis

### 📧 Email (18 files)
| # | v7 File | v8 Match | % | Action |
|---|---------|----------|---|--------|
| 1 | about-email-channel.md | campaign-web/v8/email | 95% | 🗑️ DELETE |
| 2 | creating-an-email-delivery.md | campaign-web/v8/email/create | 95% | 🗑️ DELETE |

### 📱 SMS (7 files)
| # | v7 File | v8 Match | % | Action |
|---|---------|----------|---|--------|
| 1 | sms-channel.md | campaign-web/v8/msg/send-sms | 90% | 🗑️ DELETE |
| 2 | **sms-set-up-mid.md** | NONE | 0% | ✅ **KEEP** |

[... continues for all categories ...]

## ✅ Must Keep (18 files)
- **personalized-coupons.md** - Coupons not in v8 FFDA
- **sms-set-up-mid.md** - Mid-sourcing (on-prem)
- **spamassassin.md** - On-prem spam filtering

## 🗑️ Quick Wins (67 files)
Email basics, SMS, Push, Direct mail → All in v8

## 🎯 Execution Plan
Week 1: Delete 67 files (60%)
Week 2: Badge 18 files
Week 3: Review 18 files
```

&#x200B;---

## 🎬 デモスクリプト

**開始**:
> 「本日は、AI を使用して v7 ドキュメントの再編成を自動化した方法をお見せします。 以前は数週間かかっていましたが、今では数分で完了できます。」

**問題**:
> 「1,500 以上の v7 ドキュメントファイルがあります。 多くは v8 で複製されています。 保持、削除、移行する対象を特定する必要があります。」

**解決策**:
> 「フォルダーを分析して実用的な推奨事項を生成するスマートプロンプトを作成しました。」

**デモ**:
> 「見せてあげる。 「配信」フォルダーを 111 個のファイルで分析します。」
> 
> [ プロンプトのコピー、貼り付け、実行 ]
> 
> 「。..そして、30 秒後に、完全な分析を取得します。」

**結果**:
> 「これをご覧ください
> - 67 個のファイルを削除（60% 削減）
> - 18 v7 固有のファイルが特定されました
> - 移行する 8 個のファイル
> - 3 週間の実行プランの完了
> 
> すべて自動化されています。 すべて正確です。」

**閉じる**:
> 「この同じプロセスは、21 個のすべてのフォルダーで機能します。 以前は 6 週間かかっていましたが、今では 15 分で済みます。」

&#x200B;---

## デモの準備 🚀 完了しました。

**Just**:
1. このファイルを開く
2. プロンプトをコピーします
3. カーソルにペースト
4. 魔法の ✨ を表示

**合計デモ時間**:3～5 分\
**Wow factor**: 🔥🔥🔥

