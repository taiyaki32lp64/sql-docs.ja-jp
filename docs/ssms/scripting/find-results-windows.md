---
title: 検索結果ウィンドウ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vs.findresults2
helpviewer_keywords:
- Find Results Windows dialog box
ms.assetid: 3b68dbb7-26d6-4bc9-bd2c-c27e5dc385c3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1162aed479c7c895b21138e882c6fbdce51eec3
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265444"
---
# <a name="find-results-windows"></a>検索結果ウィンドウ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  2 つの検索結果ウィンドウには、 **[検索と置換]** ダイアログの **[フォルダーを指定して検索]** タブまたは **[フォルダーを指定して置換]** タブを使用して検出された項目が表示されます。 **[フォルダーを指定して検索]** または **[フォルダーを指定して置換]** の **[検索結果]** コマンドを使用すると、検出された項目が表示される検索結果ウィンドウを選択できます。  
  
 条件に一致する項目が検出されると、選択された検索結果ウィンドウが自動的に開きます。 検索結果ウィンドウを手動で表示するには、 **[表示]** メニューの **[その他のウィンドウ]** をクリックし、 **[検索結果 1]** または **[検索結果 2]** をクリックします。  
  
 コード ファイルを表示し、一致する項目が検出された行にジャンプするには、結果一覧内の任意の行をダブルクリックします。 コード エディターにソース ファイルが表示され、条件に一致するテキストの先頭にカーソルが置かれます。 エディターのインジケーター マージンには、条件に一致する項目がその行に含まれることを示す記号が表示され、ステータス バーにフルテキストが表示されます。  
  
## <a name="toolbar-buttons"></a>ツール バー ボタン  
 ツール バーには、結果一覧内を移動したり、一致項目が検出されたコード行にジャンプしたりするために、次のボタンが用意されています。  
  
 **ページ + 上方向キー**  
 選択されている一致項目が検出された行に移動します。  
  
 **ページ + 左方向キー**  
 前の一致項目が含まれる行に移動します。  
  
 **ページ + 右方向キー**  
 次の一致項目が含まれる行に移動します。  
  
 **[すべてクリア]**  
 **結果** の一覧からすべての一致項目を削除します。  
  
## <a name="shortcut-keys"></a>ショートカット キー  
 検出された項目間をすばやく移動するために、次のショートカット キーが用意されています。  
  
 Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;Home  
 検索結果ウィンドウの最上部までスクロールします。  
  
 Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;End  
 検索結果ウィンドウの最下部までスクロールします。  
  
 PageUp  
 次の一致項目のグループまで上にスクロールします。  
  
 PageDown  
 次の一致項目のグループまで下にスクロールします。  
  
 ↑  
 前の一致項目を選択します。  
  
 下方向キー  
 次の一致項目を選択します。  
  
## <a name="search-result-entries"></a>検索結果のエントリ  
 結果一覧の各エントリについて、次の情報が表示されます。  
  
-   完全なパス  
  
-   [ファイル名]  
  
-   行番号  
  
-   一致項目が含まれている行のフルテキスト  
  
> [!TIP]  
>  **[クイック検索]** を使用すると、長い結果一覧内をすばやくスキャンできます。 検索結果ウィンドウを開いてドッキングします。次に、 **検索** タブにある三角形の **表示** ボタンをクリックして **[クイック検索]** に切り替えます。 **[検索対象]** フィールドを **[現在のウィンドウ]** に設定します。 **[検索する文字列]** に文字列を入力し、 **[次を検索]** をクリックします。 これにより、結果一覧をスキャンして、特定のフォルダーまたはファイル内で検出された一致項目や、他の重要な用語も一緒に現れるコード行で検出された一致項目を表示できます。  
  
## <a name="summary-lines"></a>概要行  
 検索結果の各セットは、検索パラメーターが示された行で開始され、統計情報が示された行で終了します。 たとえば、すべての開いているドキュメントを対象に、正規表現 " **" を検索文字列として指定した** [フォルダーを指定して検索]`var[1-3]&par`検索の結果一覧は、次の検索パラメーターが示される行で始まります。  
  
 `Find all "var[1-3]&par" Regular Expression, All Open Documents`  
  
 最後の行には、次のような統計情報が含まれます。  
  
 `Total found: 57  Matching files: 23  Total files searched: 59`  
  
 すべての開いているドキュメントを対象に、正規表現 " **" に一致するすべての文字列を、文字列 "** " で置換する`var[1-3]&par`[フォルダーを指定して置換]`sample`検索の結果一覧は、次の検索パラメーターが示される行で始まります。  
  
 `Replace "var[1-3]&par", "sample", Regular Expression, All Open Documents`  
  
 最後の行には、次のような統計情報が含まれます。  
  
 `Total replaced: 57  Matching files: 23  Total files searched: 59`  
