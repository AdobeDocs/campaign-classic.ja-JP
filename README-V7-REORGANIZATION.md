---
source-git-commit: 65d223acd23f26bd9c6979d11815d23f02ae2382
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---
# 📚 v7 ドキュメント再編成キット

**2 プロンプトは、アナライザーと主催者 la doc v7 → v8 を注ぐ**

&#x200B;---

## 📁 Fichiers

### 🔍 プロンプト （指示）

| フィッシャー | 説明 | 出力 |
|---------|-------------|--------|
| `PROMPT-1-OVERVIEW-ALL-FOLDERS.md` | Vue d&#39;ensemble de TOUS les folders v7 | `v7-reorganization-overview.md` |
| `PROMPT-2-DETAILED-FOLDER.md` | デテイラードゥン フォルダーの平均 % 一致の分析 | `[folder]-detailed-analysis.md` |

&#x200B;---

## 🚀 使用率

### 1️⃣ Vue d&#39;Ensemble （トゥーレ フォルダー）

```bash
# 1. Ouvrir le prompt
open PROMPT-1-OVERVIEW-ALL-FOLDERS.md

# 2. Copier tout le contenu du bloc "COPIER CE PROMPT"
# 3. Coller dans Cursor/ChatGPT
# 4. Obtenir : v7-reorganization-overview.md
```

**ジェネール** :
- 📊 エグゼクティブサマリー（統計グローバル）
- 📁 des 21 フォルダの分析
- 🎯 マトリス・デ・プリオライゼーション
- ✅ アクション アイテム
- ⚠️ リスク
- 📈 メトリックス

**Taille** : Markdown で 50～60 ページ

&#x200B;---

### 2️⃣ Analyze Détaillée d&#39;un フォルダー

```bash
# 1. Ouvrir le prompt
open PROMPT-2-DETAILED-FOLDER.md

# 2. Modifier la ligne :
📁 **Analyze**: /Users/.../help/delivery/using/

# 3. Remplacer par le folder souhaité :
# - /help/delivery/using/
# - /help/workflow/using/
# - /help/web/using/
# - etc.

# 4. Copier tout le contenu du bloc "COPIER CE PROMPT"
# 5. Coller dans Cursor/ChatGPT
# 6. Obtenir : [folder]-detailed-analysis.md
```

**ジェネール** :
- 📊 Stats du フォルダー
- 📋 Tableau détaillé organisé comme Experience League
- 🔗 Liens のクライアントライブラリ（v7 + Experience League）
- 📈 Juscu&#39;à 3 matchs v8 par fichier avec %
- 📄 ファイル par ファイルの概要
- 🎯 プラン ドゥ レオーガニゼーション
- 追跡に使用する ✅ チェックボックス

**Taille** : Markdown で 30～40 ページ

&#x200B;---

## 📊 d&#39;Output の例

### プロンプト 1 （概要）

```markdown
# 📊 v7 Documentation Reorganization Overview

**Total Files**: 1,500
**KEEP**: 400 (27%)
**DELETE**: 800 (53%)
**MOVE**: 200 (13%)
**REVIEW**: 100 (7%)

## 📁 Folder Analysis

### 🟢 100% KEEP - v7-Only Content
| Folder | Files | Reason |
|--------|-------|--------|
| /installation/ | 75 | On-premise setup |
| /mrm/ | 5 | Not in v8 FFDA |
...
```

### プロンプト 2 （詳細フォルダー）

```markdown
# 📊 v7 Folder Analysis: Delivery

**Total Files**: 111

| # | v7 File | v8 Match 1 | % | v8 Match 2 | % | Notes | Action |
|---|---------|------------|---|------------|---|-------|--------|
| 1 | about-email-channel.md | campaign-web/v8/email | 95% | - | - | Fully in v8 | 🗑️ DELETE |
| 9 | sms-set-up-mid.md | NONE | 0% | - | - | Mid-sourcing (on-prem) | ✅ KEEP |
...
```

&#x200B;---

## 🎯 ワークフローの推奨事項

### セメイン 1：ヴー・ダンサンブル1. Exécuter **Prompt 1** → Obtenir `v7-reorganization-overview.md`2. フォルダー優先順位付きの識別子3. パートナーの AVEC 関係者

### Semaine 2-4 : détaillée を分析1. チャックフォルダーのプリミティブの作成：   - Exécuter **プロンプト 2**   - オブテニール `[folder]-detailed-analysis.md`   - ヴァリデル レ デシシオン   - Commencer les actions

### Semaine 5+：エクセクション1. Supprimer les fichiers identifies （DELETE）2. バッジャーはフィッシャー v7 専用（KEEP）3. Migrer le contenu manquant （MOVE）4. レビュアー les cas ambigus （レビュー）

&#x200B;---

## 💡 ヒント

### プロンプトの入力- ✅ コピー/カラー l&#39;intégralité du prompt- ✅ Ne パス修飾子 le 形式- ✅ Adapter seulement le chemin du folder （プロンプト 2）

### 出力を出力する- マークダウン時の 📝 出力（pas HTML）- 🔗 Liens Cliquables 自動タスク- 追跡に使用する ✅ チェックボックス- 📊 Stats et pourcentages- 🎨 絵文字エ イコーヌ

### 分析する- 🎯 Commencer par les gros フォルダー（配信、ワークフロー）- ⚡ プライオリザー・レ・クイック勝利（95% 試合）- 🔍 Reviewer manuellement les cas ambigus （一致率 70% 未満）- ✅ Valider AVEC SME アバント抑制マッシブ

&#x200B;---

## ⚠️ 重要

### アバント ド サプリマー1. ✅ ベリフィール レキバルト v82. ✅ Vérifier qu&#39;il n&#39;y a pas de contenu v7 固有3. ✅ メトレ ア ジュール `redirects.csv`4. ✅ ヴァリダー avec un expert （先制者に注ぐ）

### Fichiers v7 のみの使用1. ✅ アジュアウン ウン バッジ オ デブ デュ フィジエ2. ✅ Expliquer pourquoi c&#39;est v7 のみ3. ✅ Lien vers les 制限 v8

&#x200B;---

## 🆘 サポート

**質問**?
- プロンプト新フォンチョンヌ パ → ヴェリファイア レ シュマン デ レポ
- 出力トロップ ロング → デマンドールの概要
- ベソイン デ→ーデ ピン レキペ ドク

&#x200B;---

**デリエール・ミゼ・ア・ジュール**:2026-01-13

