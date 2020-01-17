---
title: クエリおよびビュー デザイナーでの移動 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, navigating
- shortcuts [SQL Server]
- Query Designer [SQL Server], navigating
- keyboard shortcuts [Visual Database Tools]
ms.assetid: 1c65acef-6dfa-463a-bf37-5a5335fe3865
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f9581eca3d6abbefcd897ccc4ce627ca180649b3
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262300"
---
# <a name="navigate-in-the-query-and-view-designer-visual-database-tools"></a>クエリおよびビュー デザイナーでの移動 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
クエリおよびビュー デザイナー内では、キーボードまたはマウスを使用して作業できます。 具体的な方法については、次の表を参照してください。  
  
## <a name="any-pane"></a>すべてのペイン  
  
|**変換先**|**ショートカット キー**|**クリックする場所**|  
|----------|-------------|-------------|  
|クエリおよびビュー デザイナーのペイン間で移動する|F6&lt;/localizedText&gt;、&lt;localizedText&gt;Shift&lt;/localizedText&gt; + &lt;localizedText&gt;F6|移動先のペイン内の任意の箇所|  
  
> [!TIP]  
> Ctrl キーを押しながら Tab キーを押すと、クエリおよびビュー デザイナーのペインだけでなく、その他のペインにフォーカスを移すことができます。  
  
## <a name="diagram-pane"></a>ダイアグラム ペイン  
  
|**変換先**|**ショートカット キー**|**クリックする場所**|  
|----------|-------------|-------------|  
|テーブルやその他のテーブル構造オブジェクト間で移動する (または、結合線に移動する)|Tab または Shift + Tab|移動先のテーブル、テーブル構造オブジェクト、または結合線|  
|テーブルまたはテーブル構造オブジェクト内の列間で移動する|方向キー|移動先の列|  
|出力するデータ列を選択する|Space または +|列の名前の横にあるチェック ボックス|  
|選択したデータ列をクエリ出力から削除する|Space または -|列の名前の横にあるチェック ボックス|  
|選択したテーブル、テーブル構造オブジェクト、または結合線をクエリから削除する|DELETE|右クリックしてから **[削除]** をクリック|  
  
> [!NOTE]  
> 複数の項目を選択している場合は、このキーを押すと、選択されているすべての項目が影響を受けます。 複数の項目を選択するには、Ctrl キーを押しながら各項目をクリックします。  
  
詳細については、「[ダイアグラム ペイン (Visual Database Tools)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)」を参照してください。  
  
## <a name="criteria-pane"></a>抽出条件ペイン  
  
|変換先|ショートカット キー|クリックする場所|  
|------|---------|---------|  
|セル間で移動する|方向キーまたは Tab または Shift + Tab|移動先のセル|  
|選択した列の最後の行に移動する|Ctrl + ↓||  
|選択した列の最初の行に移動する|Ctrl + ↑||  
|グリッド内の見えている範囲の左上隅にあるセルに移動する|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;Home||  
|右下隅にあるセルに移動する|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;End||  
|ドロップダウン リスト内で移動する|↑または↓|セル内のボタン|  
|グリッド内の 1 つの列全体を選択する|Ctrl + SPACE キー|列ヘッダー|  
|編集モードとセル選択モードを切り替える|F2||  
|セル内の選択された文字列をクリップボードにコピーする (編集モードの場合)|Ctrl + C||  
|セル内で選択したテキストを切り取ってクリップボードに送る (編集モードの場合)|Ctrl + X||  
|クリップボードからテキストを貼り付ける (編集モードの場合)|Ctrl + V||  
|セルでの編集中に挿入モードと上書きモードを切り替える|Ins||  
|[出力] 列のチェック ボックスのオンとオフを切り替える|Space キー|チェック ボックス|  
|セルの選択した内容を削除する|DELETE||  
|選択したグリッド列の値をすべて削除する|DELETE||  
|既存の行の間に行を挿入する|グリッド線を選択した後で Ins||  
|[または...] 列を追加する|いずれかの [または...] 列を選択した後で Ins||  
  
> [!NOTE]  
> 複数の項目を選択している場合は、このキーを押すと、選択されているすべての項目が影響を受けます。  
  
詳細については、「[抽出条件ペイン (Visual Database Tools)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)」を参照してください。  
  
## <a name="sql-pane"></a>SQL ペイン  
SQL ペインでの作業時には、標準の Windows 編集キーを使用できます。たとえば、Ctrl + 方向キーで単語間を移動したり、 **[編集]** メニューの **[切り取り]** 、 **[コピー]** 、および **[貼り付け]** コマンドを使用したりできます。  
  
> [!NOTE]  
> テキストの挿入だけができます。上書きモードはありません。  
  
詳細については、「[SQL ペイン (Visual Database Tools)](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)」を参照してください。  
  
## <a name="results-pane"></a>結果ペイン  
  
|**変換先**|**ショートカット キー**|**クリックする場所**|  
|----------|-------------|-------------|  
|セル間を移動する|方向キーまたは Tab または Shift + Tab|移動先のセル|  
|現在の行の最初または最後のセルに移動する|ホームまたは End||  
|現在の列の最初の行に移動する|Ctrl + ↑||  
|左上隅のセルに移動する|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;Home||  
|最初の列の一番下のセルに移動する|Ctrl + ↓||  
|セル内の最初の文字を選択する|Shift</localizedText> + <localizedText>Home||  
|セル内の最後の文字を選択する|Shift</localizedText> + <localizedText>End||  
|編集モードとセル選択モードを切り替える|F2||  
|セルでの編集中に挿入モードと上書きモードを切り替える|Ins||  
|テーブルから行を削除する|DELETE||  
|現在のセルに対する変更を元に戻す|変更したセル内で Esc||  
|現在の行に対する変更を元に戻す|変更していないいずれかのセル内で Esc||  
|セルに NULL を入力する|Ctrl + 0||  
|選択した列または行をクリップボードにコピーする|Ctrl + C||  
|セル内の選択された文字列をクリップボードにコピーする (編集モードの場合)|Ctrl + C||  
|セル内の選択された文字列を切り取ってクリップボードに送る (編集モードの場合)|Ctrl + X||  
|クリップボードからテキストを貼り付ける (編集モードの場合)|Ctrl + V||  
  
> [!NOTE]  
> 複数の項目を選択している場合は、このキーを押すと、選択されているすべての項目が影響を受けます。  
  
詳細については、「[SQL ペイン (Visual Database Tools)](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
