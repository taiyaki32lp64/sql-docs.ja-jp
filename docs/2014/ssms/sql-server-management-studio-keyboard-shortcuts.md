---
title: SQL Server Management Studio のキーボード ショートカット | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], shortcuts
- keyboard shortcuts [SQL Server Management Studio]
- menu shortcuts [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], keyboard shortcuts
- hot keys [SQL Server Management Studio]
- shortcuts [SQL Server Management Studio], keyboard shortcuts
- keyboard shortcuts [SQL Server Management Studio], list of shortcuts
- shortcuts [SQL Server Management Studio]
- accelerator keys
ms.assetid: 98baaac4-0727-4ce4-8bfe-c63793ae69b8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56c21fd7676e7ee20df37607752aa8076bd42096
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127054"
---
# <a name="sql-server-management-studio-keyboard-shortcuts"></a>SQL Server Management Studio のキーボード ショートカット
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] には、2 つのキーボード スキームが用意されています。 既定のスキームは [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] スキームであり、そのキーボード ショートカットの基になっているのは [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2010 です。 また、[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] では、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] の標準スキームに似たキーボード スキームも提供されています。 キーボード スキームの変更やキーボード ショートカットの追加を行うには、 **[ツール]** メニューの **[オプション]** をクリックします。 **[環境]** の **[キーボード]** ページで目的のキーボード スキームを選択できます。  
  
> [!NOTE]  
>  見出しだけを表示するには、このページの上部の **[すべて折りたたみ]** をクリックします。  
  
## <a name="menu-activation-keyboard-shortcuts"></a>メニューのアクティブ化のためのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] メニュー バーに移動する|Alt|Alt|  
|ツール コンポーネントのメニューをアクティブ化する|Alt + ハイフン|Alt + ハイフン|  
|コンテキスト メニューを表示する|Shift + F10|Shift + F10|  
|ファイルを作成するための **[新しいファイル]** ダイアログ ボックスを表示する|Ctrl + N|Ctrl + N|  
|新しいプロジェクトを作成するための **[新しいプロジェクト]** ダイアログ ボックスを表示する|Ctrl + Shift + N|Ctrl + Shift + N|  
|既存のファイルを開くための **[ファイルを開く]** ダイアログ ボックスを表示する|Ctrl + O<br /><br /> または<br /><br /> Ctrl + Shift + G|Ctrl + O|  
|既存のプロジェクトを開くための **[プロジェクトを開く]** ダイアログ ボックスを表示する|Ctrl + Shift + O|Ctrl + Shift + O|  
|現在のプロジェクトに新しいファイルを追加するための **[新しい項目の追加]** ダイアログ ボックスを表示する|Ctrl + Shift + A|Ctrl + Shift + A|  
|現在のプロジェクトに既存のファイルを追加するための **[既存項目の追加]** ダイアログ ボックスを表示する|Shift + Alt + A|Shift + Alt + A|  
|クエリ デザイナーを表示する|Ctrl + Shift + Q|Ctrl + Shift + Q|  
|メニューまたはダイアログ ボックスを閉じて操作を取り消す|Esc|Esc|  
  
## <a name="windows-management-and-toolbar-keyboard-shortcuts"></a>ウィンドウ管理とツール バーのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|現在の MDI 子ウィンドウを閉じる|Ctrl + F4|Ctrl + F4|  
|メニューまたはダイアログ ボックスを閉じるか、実行中の操作を取り消すか、または現在のドキュメント ウィンドウにフォーカスを設定する|Esc|Esc|  
|印刷|Ctrl + P|Ctrl + P|  
|終了する|Alt + F4|Alt + F4|  
|全画面モードを切り替える|Shift + Alt + Enter|Shift + Alt + Enter|  
|現在のツール ウィンドウを閉じる|Shift + Esc|Shift + Esc|  
|次の MDI 子ウィンドウを順番に表示する|Ctrl + F6|Ctrl + Tab|  
|最初のドキュメント ウィンドウが選択された状態で IDE ナビゲーターを表示する|Ctrl + Tab|同等の機能がありません|  
|前の MDI 子ウィンドウを順番に表示する|Ctrl + Shift + Tab|Ctrl + Shift + Tab|  
|エディターがコード ビューまたはサーバー コード ビューのとき、コード エディターの先頭にあるドロップダウン バーに挿入ポイントを移動する|Ctrl + F2|同等の機能がありません|  
|現在のツール ウィンドウのツール バーに移動する|Shift + Alt|Shift + Alt|  
|最初のツール ウィンドウが選択された状態で IDE ナビゲーターを表示する|Alt + F7|同等の機能がありません|  
|次のツール ウィンドウに移動する|Alt + F6<br /><br /> または<br /><br /> [!INCLUDE[ssDE](../includes/ssde-md.md)] クエリ エディターで F6|Alt + F6|  
|前のツール ウィンドウに移動する|Shift + Alt + F7|Shift + Alt + F7|  
|単一ドキュメントの分割ペイン ビューの次のペインに移動する|F6|F6|  
|前に選択していたウィンドウに移動する|Shift + Alt + F6<br /><br /> または<br /><br /> [!INCLUDE[ssDE](../includes/ssde-md.md)] クエリ エディターで Shift + F6|Shift + Alt + F6|  
|単一ドキュメントの分割ペイン ビューの前のペインに移動する|Shift + F6|F6|  
|ドック メニューを表示する|Ctrl + マイナス記号 (-)|同等の機能がありません|  
|開いているすべてのウィンドウの一覧が含まれるポップアップを表示する|Ctrl + Alt + ↓|同等の機能がありません|  
|新しいクエリ エディター ウィンドウを開く|Ctrl + O|Ctrl + O|  
|オブジェクト エクスプローラーを表示する|F8|F8|  
|登録済みサーバーを表示する|Ctrl + Alt + G|Ctrl + Alt + G|  
|テンプレート エクスプローラーを表示する|Ctrl + Alt + T|Ctrl + Alt + T|  
|ソリューション エクスプローラーを表示する|Ctrl + Alt + L|Ctrl + Alt + L|  
|概要ウィンドウを表示する|F7|F7|  
|[プロパティ] ウィンドウを表示する|F4|F4|  
|**[出力]** ウィンドウを表示する|Ctrl + Alt + O|同等の機能がありません|  
|**[タスク一覧]** ウィンドウを表示する|CTRL+\\、T<br /><br /> または<br /><br /> CTRL+\\、CTRL+T|Ctrl + Alt + K|  
|[オブジェクト エクスプローラーの詳細] リスト ビューと [オブジェクト エクスプローラーの詳細] プロパティ ペインとを切り替える|F6|F6|  
|[オブジェクト エクスプローラーの詳細] リスト ビューと [オブジェクト エクスプローラーの詳細] プロパティ ペインとを区切る分割バーを制御して、表示ペインのサイズを調整する|Tab + ↑ または ↓|Tab + ↑ または ↓|  
|ツールボックスを表示する|Ctrl + Alt + X|Ctrl + Alt + X|  
|[ブックマーク] ウィンドウを表示する|Ctrl + K、Ctrl + W|Ctrl + K、Ctrl + W|  
|ブラウザー ウィンドウを表示する|Ctrl + Alt + R|Ctrl + Alt + R|  
|HTML デザイナーの Web サーバー コントロールの共通コマンドのスマート タグ メニューを表示する|Shift + Alt + F10|同等の機能がありません|  
|[エラー一覧] ウィンドウを表示する ([!INCLUDE[tsql](../includes/tsql-md.md)] エディターのみ)|CRTL+\\、CTRL+E<br /><br /> または<br /><br /> CTRL+\\、E|CRTL+\\、CTRL+E|  
|[エラー一覧] ウィンドウの次のエントリに移動する ([!INCLUDE[tsql](../includes/tsql-md.md)] エディターのみ)|Ctrl + Shift + F12|Ctrl + Shift + F12|  
|表示履歴内の前のページを表示する。 Web ブラウザー ウィンドウのみで使用可能。|Alt + ←|同等の機能がありません|  
|表示履歴内の次のページを表示する。 Web ブラウザー ウィンドウのみで使用可能。|Alt + →|同等の機能がありません|  
  
## <a name="cursor-movement-keyboard-shortcuts"></a>カーソル移動のキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|カーソルを左に移動する|左方向キー|←|  
|カーソルを右に移動する|右矢印|→|  
|カーソルを上に移動する|上矢印|上矢印|  
|カーソルを下に移動する|下方向キー|下方向キー|  
|カーソルを行の先頭に移動する|Home|Home|  
|カーソルを行の末尾に移動する|END|END|  
|カーソルをドキュメントの先頭に移動する|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;Home|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;Home|  
|カーソルをドキュメントの末尾に移動する|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;End|Ctrl&lt;/localizedText&gt; + &lt;localizedText&gt;End|  
|カーソルを 1 画面上に移動する|PageUp|PageUp|  
|カーソルを 1 画面下に移動する|PageDown|PageDown|  
|カーソルを 1 ワード右に移動する|Ctrl + →|Ctrl + →|  
|カーソルを 1 ワード左に移動する|Ctrl + ←|Ctrl + ←|  
|カーソルを最後の項目に戻す|Shift + F8|同等の機能がありません|  
|カーソルをドキュメントの先頭に移動する|Ctrl + PageUp|同等の機能がありません|  
|ドキュメントの前のタブに移動する|Ctrl + PageUp||  
|カーソルをドキュメントの末尾に移動する|Ctrl + PageDown|同等の機能がありません|  
|ドキュメントの次のタブに移動する|Ctrl + PageDown|同等の機能がありません|  
  
## <a name="text-selection-keyboard-shortcuts"></a>テキスト選択のキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|カーソルからドキュメントの先頭までのテキストを選択する|Ctrl + Shift + Home|Ctrl + Shift + Home|  
|カーソルからドキュメントの末尾までのテキストを選択する|Ctrl</localizedText> + <localizedText>Shift</localizedText> + <localizedText>End|Ctrl</localizedText> + <localizedText>Shift</localizedText> + <localizedText>End|  
|カーソルから現在の行の先頭までのテキストを選択する|Shift</localizedText> + <localizedText>Home|Shift</localizedText> + <localizedText>Home|  
|カーソルを現在の行の先頭に移動し、列選択範囲を拡大する|Shift + Alt + Home|同等の機能がありません|  
|カーソルから現在の行の末尾までのテキストを選択する|Shift</localizedText> + <localizedText>End|Shift</localizedText> + <localizedText>End|  
|カーソルを行の末尾に移動し、列選択範囲を拡大する|Shift + Alt + End|同等の機能がありません|  
|カーソル位置から下へテキストを 1 行ずつ選択する|Shift + ↓|Shift + ↓|  
|カーソルを 1 行下に移動し、列選択範囲を拡大する|Shift + Ctrl + Shift + Del||  
|カーソルを 1 文字左に移動し、選択範囲を拡大する|Shift + ←|同等の機能がありません|  
|カーソルを 1 文字左に移動し、列選択範囲を拡大する|Shift + Alt + ←|同等の機能がありません|  
|カーソルを 1 文字右に移動し、選択範囲を拡大する|Shift + →|同等の機能がありません|  
|カーソルを 1 文字右に移動し、列選択範囲を拡大する|Shift + Alt + →|同等の機能がありません|  
||||  
|カーソル位置から上へテキストを 1 行ずつ選択する|Shift + ↑|Shift + ↑|  
|カーソルを 1 つ上の行に移動して選択範囲を拡大する|Shift + Alt + ↑|Shift + Alt + ↑|  
|1 ページ上に選択範囲を拡大する|Shift + PageUp|Shift + PageUp|  
|1 ページ下に選択範囲を拡大する|Shift + PageDown|Shift + PageDown|  
|現在のドキュメント全体を選択する|Ctrl + A|Ctrl + A|  
|カーソルが置かれているワードまたはカーソルから最も近いワードを選択する|Ctrl + W|Ctrl + W|  
|エディター内の現在の位置から直前の位置までの範囲を選択する|Ctrl + 等号 (=)|Ctrl + 等号 (=)|  
|選択範囲を現在のウィンドウの先頭まで拡大する|Ctrl + Shift + PageUp|Ctrl + Shift + PageUp|  
|カーソルをビュー内の最終行に移動して選択範囲を拡大する|Ctrl + Shift + PageDown|Ctrl + Shift + PageDown|  
|選択範囲を右に 1 ワード拡大する|Ctrl + Shift + →|Ctrl + Shift + →|  
|選択範囲を左に 1 ワード拡大する|Ctrl + Shift + ←|Ctrl + Shift + ←|  
|カーソルを 1 ワード右に移動し、選択範囲を拡大する|Ctrl + Shift + Alt + →|Ctrl + Shift + Alt + →|  
|カーソルを 1 ワード左に移動し、選択範囲を拡大する|Ctrl + Shift + Alt + ←|Ctrl + Shift + Alt + ←|  
|カーソルを次の中かっこに移動し、選択範囲を拡大する|Ctrl + Shift + ]|同等の機能がありません|  
|現在のカーソル位置から後方移動 (Ctrl + マイナス記号 (-)) 位置までのテキストを選択する|Ctrl + 等号 (=)|同等の機能がありません|  
|移動履歴で前のドキュメントまたはウィンドウに戻る|Ctrl + マイナス記号 (-)|同等の機能がありません|  
|移動履歴で次のドキュメントまたはウィンドウに進む|Ctrl + Shift + マイナス記号 (-)|同等の機能がありません|  
|現在の選択範囲のアンカーと終点を入れ替える|Ctrl + K、Ctrl + A|同等の機能がありません|  
|カーソルをビュー内の先頭行に移動して選択範囲を拡大する|Ctrl + Shift + PageUp|同等の機能がありません|  
|カーソルをビュー内の最終行に移動して選択範囲を拡大する|Ctrl + Shift + PageDown|同等の機能がありません|  
  
## <a name="bookmark-keyboard-shortcuts"></a>ブックマークのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|現在の行のブックマークを設定または解除する|Ctrl + K、Ctrl + K|Ctrl + K、Ctrl + K|  
|次のブックマークに移動する|Ctrl + K、Ctrl + N|Ctrl + K、Ctrl + N|  
|現在のブックマークがフォルダー内にある場合、フォルダーの次のブックマークに移動する。 フォルダー外のブックマークはスキップされます。<br /><br /> ブックマークがフォルダー内にない場合は、同レベルの次のブックマークに移動します。<br /><br /> ブックマーク ウィンドウにフォルダーが含まれる場合、フォルダー内のブックマークはスキップされます。|Ctrl + Shift + K、Ctrl + Shift + N|同等の機能がありません|  
|前のブックマークに移動する|Ctrl + K、Ctrl + P|Ctrl + K、Ctrl + P|  
|現在のブックマークがフォルダー内にある場合、フォルダーの次のブックマークに移動する。 フォルダー外のブックマークはスキップされます。<br /><br /> ブックマークがフォルダー内にない場合は、同レベルの次のブックマークに移動します。<br /><br /> ブックマーク ウィンドウにフォルダーが含まれる場合、フォルダー内のブックマークはスキップされます。|Ctrl + Shift + K、Ctrl + Shift + P|同等の機能がありません|  
|ブックマークをクリアする|Ctrl + K、Ctrl + L|Ctrl + K、Ctrl + L|  
  
## <a name="tree-control-keyboard-shortcuts"></a>ツリー コントロールのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|ツリー ノードを折りたたむ|- (テンキー)|- (テンキー)|  
|すべてのツリー ノードを展開する|* (テンキー)|* (テンキー)|  
|ウィンドウ内でツリー コントロールを上にスクロールする|Ctrl + ↑|Ctrl + ↑|  
|ウィンドウ内でツリー コントロールを下にスクロールする|Ctrl + ↓|Ctrl + ↓|  
  
## <a name="code-editor-keyboard-shortcuts"></a>コード エディターのキーボード ショートカット  
 すべての種類のコード エディターにすべてのショートカットが実装されているわけではありません。  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|全画面表示を切り替える|Shift + Alt + Enter|Shift + Alt + Enter|  
|テキストを 1 つ上の行にスクロールする|Ctrl + ↑|Ctrl + ↑|  
|テキストを 1 つ下の行にスクロールする|Ctrl + ↓|Ctrl + ↓|  
|最後の編集操作を元に戻す|Ctrl + Z<br /><br /> または<br /><br /> Alt + BackSpace|Ctrl + Z|  
|最後に元に戻した編集を復元する|Ctrl + Shift + Z<br /><br /> または<br /><br /> Ctrl + Y<br /><br /> または<br /><br /> Alt + Shift + BackSpace|Ctrl + Shift + Z<br /><br /> または<br /><br /> Ctrl + Y<br /><br /> または<br /><br /> Alt + Shift + BackSpace|  
|選択した項目を保存する|Ctrl + S|Ctrl + S|  
|すべて保存する|Ctrl + Shift + S|Ctrl + Shift + S|  
|閉じる|Ctrl + F4|Ctrl + F4|  
|印刷|Ctrl + P|Ctrl + P|  
|終了する|Alt + F4|Alt + F4|  
|現在のファイルをブラウザーで開く|Ctrl + Shift + W|同等の機能がありません|  
|現在のファイルのすべてのテキストを削除する|Ctrl + Shift + Del|Ctrl + Shift + Del|  
|**[指定行へのジャンプ]** ダイアログ ボックスを表示する|Ctrl + G|Ctrl + G|  
|**[移動]** ダイアログ ボックスを表示する|Ctrl + プラス記号 (+)|同等の機能がありません|  
|行のインデントを増やす|Tab|Tab|  
|行のインデントを減らす|Shift + Tab|Shift + Tab|  
|選択したテキストを大文字にする|Ctrl + Shift + U|Ctrl + Shift + U|  
|選択したテキストを小文字にする|Ctrl + U|Ctrl + Shift + L|  
|選択したテキストをコメント化する|Ctrl + K、Ctrl + C|Ctrl + K、Ctrl + C|  
|選択したテキストのコメント化を解除する|Ctrl + K、Ctrl + U|Ctrl + K、Ctrl + U|  
|現在の接続で新しいクエリを開く|Ctrl + N|Ctrl + N|  
|オブジェクト エクスプローラーでデータベースを開く|Alt + F8|Alt + F8|  
|テンプレート パラメーターの値を指定する|Ctrl + Shift + M|Ctrl + Shift + M|  
|クエリ エディターの選択部分、または選択部分がない場合はクエリ エディター全体を実行する|F5<br /><br /> または<br /><br /> Ctrl + Shift + E|F5<br /><br /> または<br /><br /> Ctrl + E<br /><br /> または<br /><br /> Alt + X|  
|クエリ エディターの選択部分、または選択部分がない場合はクエリ エディター全体を解析する|Ctrl + F5|Ctrl + F5|  
|推定実行プランを表示する|Ctrl + Shift + Atl + L|Ctrl + L|  
|クエリの実行を取り消す|Alt + Break|Alt + Break|  
|実際の実行プランをクエリ出力に含める|Ctrl + Shift + Atl + M|Ctrl + M|  
|結果をグリッドに出力する|Ctrl + Shift + D|Ctrl + D|  
|結果をテキスト形式で出力する|Ctrl + T|Ctrl + T|  
|結果をファイルに出力する|Ctrl + Shift + T|Ctrl + Shift + F|  
|クエリの結果ペインの表示/非表示を切り替える|Ctrl + R|Ctrl + R|  
|クエリ結果ペインを表示する|Ctrl + Shift + Alt + R||  
|クエリと結果ペインを切り替える|F6|F6|  
|結果グリッドとヘッダーをクリップボードにコピーする|Ctrl + Shift + C|同等の機能がありません|  
|[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] で次のアクティブ ウィンドウに移動する|Alt + F6|Alt + F6|  
|開く [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|Ctrl + Alt + P|Ctrl + Alt + P|  
|クエリ エディター ウィンドウからクエリ デザイナー ダイアログ ボックスを表示する|Ctrl + Shift + Q|同等の機能がありません|  
|`sp_help` システム ストアド プロシージャを実行する|Alt + F1|Alt + F1|  
|`sp_who` システム ストアド プロシージャを実行する|Ctrl + 1|Ctrl + 1|  
|`sp_lock` システム ストアド プロシージャを実行する|Ctrl + 2|Ctrl + 2|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 3|Ctrl + 3|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 4|Ctrl + 4|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 5|Ctrl + 5|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 6|Ctrl + 6|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 7|Ctrl + 7|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 7|Ctrl + 7|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 8|Ctrl + 8|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 9|Ctrl + 9|  
|**[ツール]**、 **[オプション]**、 **[キーボード]**、 **[クエリ ショートカット]** ダイアログ ボックスでこのショートカットに対して構成されているストアド プロシージャを実行する|Ctrl + 0|Ctrl + 0|  
  
## <a name="text-manipulation-in-code-editor-keyboard-shortcuts"></a>コード エディターのテキスト操作のキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|新しい行を挿入する|Enter または Shift + Enter|Enter または Shift + Enter|  
|カーソルの両側の文字を入れ替える (SQL エディターは適用外)|Ctrl + T|Ctrl + T|  
|カーソルの右側の 1 文字を削除する|Del|Del|  
|カーソルの左側の 1 文字を削除する|BackSpace<br /><br /> または<br /><br /> Shift +<br /><br /> BackSpace|BackSpace<br /><br /> または<br /><br /> Shift +<br /><br /> BackSpace|  
|選択範囲内の空白文字を削除する。選択範囲がない場合は、カーソルの隣の空白文字を削除する。|Ctrl + K、C|同等の機能がありません|  
|エディターで指定されている数のスペースを挿入する|Tab|Tab|  
|カーソルの上に空の 1 行を挿入する|Ctrl + Enter|Ctrl + Enter|  
|カーソルの下に空の 1 行を挿入する|Ctrl + Shift + Enter|Ctrl + Shift + Enter|  
|選択したテキストを小文字に変更する|Ctrl + Shift + L|Ctrl + Shift + L|  
|選択したテキストを大文字に変更する|Ctrl + Shift + U|Ctrl + Shift + U|  
|挿入モードと上書きモードを切り替える|INSERT|INSERT|  
|選択した行を 1 タブ ストップ分左に移動する|Shift + Tab|Shift + Tab|  
|カーソルの右側の 1 ワードを削除する|Ctrl + Del|Ctrl + Del|  
|カーソルの左側の 1 ワードを削除する|Ctrl + BackSpace|Ctrl + BackSpace|  
|カーソルの両側のワードを入れ替える (SQL エディターは適用外)|Ctrl + Shift + T|Ctrl + Shift + T|  
|カーソルが含まれる行を次の行の下に移動する|Shift + Alt + T|同等の機能がありません|  
|**[オプション]** ダイアログ ボックスの **[テキスト エディター]** セクションの言語の **[書式設定]** ペインで指定されている言語のインデントおよび空白書式設定を適用する。 テキスト エディターでのみ使用できます。|Ctrl + K、Ctrl + D|同等の機能がありません|  
|周囲のコード行に基づいて、選択されているコード行を正しくインデントする|Ctrl + K、Ctrl + F|同等の機能がありません|  
|現在の行のショートカットを設定または解除する|Ctrl + K、Ctrl + H|同等の機能がありません|  
|現在の行からコメント構文を削除する|Ctrl + K、Ctrl + U|同等の機能がありません|  
|空白文字およびタブの表示と非表示を切り替える|Ctrl + R、Ctrl + W|同等の機能がありません|  
|エディターの右端で折り返す機能を有効または無効にする|Alt + F、Ctrl + W|同等の機能がありません|  
|すべてのアウトライン領域を折りたたみ、階層の最も外側のグループだけを表示する|Ctrl + M、Ctrl + A|同等の機能がありません|  
|現在選択されているアウトライン領域を折りたたむ|Ctrl + M、Ctrl + S|同等の機能がありません|  
|ページ上のすべてのアウトライン領域を展開する|Ctrl + M、Ctrl + X|同等の機能がありません|  
|現在選択されているアウトライン領域を展開する|Ctrl + M、Ctrl + E|同等の機能がありません|  
|既存のアウトライン領域を折りたたむ|Ctrl + M、Ctrl + O||  
|選択したテキストを非表示にする。 シグナル アイコンによって非表示テキストの位置が示されます。|Ctrl + M、Ctrl + H|同等の機能がありません|  
|非表示として以前にマークされているすべてのテキスト セクションの非表示状態と表示状態を切り替える|Ctrl + M、Ctrl + L|同等の機能がありません|  
|現在選択されている非表示テキスト セクションの非表示状態と表示状態を切り替える|Ctrl + M、Ctrl + M|同等の機能がありません|  
|文書内のすべてのアウトライン情報を削除する|Ctrl + M、Ctrl + P|同等の機能がありません|  
|現在選択されている領域のアウトライン情報を削除する|Ctrl + M、Ctrl + U|同等の機能がありません|  
  
## <a name="transact-sql-debugger-keyboard-shortcuts"></a>Transact-SQL デバッガーのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|デバッグを開始または続行する|Alt + F5|Alt + F5|  
|デバッグを停止する|Shift + F5|Shift + F5|  
|ステップ イン|F11|F11|  
|ステップ オーバー|F10|F10|  
|ステップ アウト|Shift + F11|Shift + F11|  
|特定のステートメントにステップ インする|Shift + Alt + F11|同等の機能がありません|  
|次のステートメントを設定する|Ctrl + 3 0|同等の機能がありません|  
|次のステートメントを表示する|Alt + Num|同等の機能がありません|  
|**[カーソルまで実行]** コマンドを実装する|Ctrl + F10|Ctrl + F10|  
|**[クイック ウォッチ]** ダイアログ ボックスを表示する|Ctrl + Alt + Q<br /><br /> または<br /><br /> Shift + F9|Ctrl + Alt + Q|  
|ブレークポイントを設定/解除する|F9|F9|  
|ブレークポイントを有効にする|Ctrl + F9|同等の機能がありません|  
|ブレークポイントを削除する。 **[ブレークポイント]** ウィンドウでのみ使用可能。|Alt + F9、D|同等の機能がありません|  
|**[ブレークポイント ラベルの編集]** ダイアログ ボックスを開く。 **[ブレークポイント]** ウィンドウでのみ使用可能。|Alt + F9、L|同等の機能がありません|  
|すべてのブレークポイントを削除する|Ctrl + Shift + F9|Ctrl + Shift + F9|  
|**[ブレークポイント]** ウィンドウを表示する|Ctrl + Alt + B|Ctrl + Alt + B|  
|すべて中断する|Ctrl + Alt + Break|Ctrl + Alt + Break|  
|関数でブレークする|Ctrl + B|同等の機能がありません|  
|**[ウォッチ 1]** ウィンドウを表示する|Ctrl + Alt + W、1|同等の機能がありません|  
|**[ウォッチ 2]** ウィンドウを表示する|Ctrl</localizedText> + <localizedText>Alt</localizedText> + <localizedText>W</localizedText>、<localizedText>2|Ctrl + Alt + W、1|  
|**[ウォッチ 3]** ウィンドウを表示する|Ctrl</localizedText> + <localizedText>Alt</localizedText> + <localizedText>W</localizedText>、<localizedText>3|Ctrl</localizedText> + <localizedText>Alt</localizedText> + <localizedText>W</localizedText>、<localizedText>3|  
|**[ウォッチ 4]** ウィンドウを表示する|Ctrl + Alt + W、4|Ctrl + Alt + W、4|  
|**[自動変数]** ウィンドウを表示する|Ctrl + Alt + V、A|Ctrl + Alt + V、A|  
|**[ローカル]** ウィンドウを表示する|Ctrl + Alt + V、L|Ctrl + Alt + V、L|  
|**[イミディエイト]** ウィンドウを表示する|Ctrl + Alt + I|Ctrl + Alt + I|  
|**[呼び出し履歴]** ウィンドウを表示する|Ctrl + Alt + C|Ctrl + Alt + C|  
|**[スレッド]** ウィンドウを表示する|Ctrl + Alt + H|Ctrl + Alt + H|  
|**[並列スタック]** ウィンドウを表示する|Ctrl + Shift + D、S|同等の機能がありません|  
|**[並列タスク]** ウィンドウを表示する|Ctrl + Shift + D、K|同等の機能がありません|  
  
## <a name="microsoft-intellisense-keyboard-shortcuts"></a>Microsoft IntelliSense のキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|メンバーの一覧を表示する|Ctrl + J|Ctrl + Space<br /><br /> または<br /><br /> Ctrl + J|  
|ワードを完成する|Ctrl + Space<br /><br /> または<br /><br /> Alt + →|Alt + →|  
|クイック情報を表示する|Ctrl + K、Ctrl + I|同等の機能がありません|  
|パラメーター情報を表示する|Ctrl + Shift + Space|Ctrl + Shift + Space|  
|パラメーター ヒントをコピーする|Ctrl + Shift + Alt + C|同等の機能がありません|  
|パラメーター ヒントを貼り付ける|Ctrl + Shift + Alt + P|同等の機能がありません|  
|構文のペア間を移動する|Ctrl + ]|Ctrl + ]|  
|コード スニペット ピッカーを起動する|Ctrl + K、Ctrl + X|Ctrl + K、Ctrl + Z|  
|ローカル キャッシュを更新する|Ctrl + Shift + R|Ctrl + Shift + R|  
|ブロックの挿入スニペット ピッカーを起動する|Ctrl + K、Ctrl + S|Ctrl + K、Ctrl + S|  
|コード スニペット マネージャーを表示する|Ctrl + K、Ctrl + B|同等の機能がありません|  
|IntelliSense フィルターのレベルを **[共通]** タブから **[すべて]** タブに変更する。|Alt + プラス記号 (+)|同等の機能がありません|  
|IntelliSense フィルターのレベルを **[すべて]** タブから **[共通]** タブに変更する|Alt + ピリオド (.)|同等の機能がありません|  
  
## <a name="document-window-and-browser-keyboard-shortcuts"></a>ドキュメント ウィンドウとブラウザーのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|全画面モードを切り替える|Shift + Alt + Enter|Shift + Alt + Enter|  
|ドキュメントの分割ペイン ビューの次のペインに移動する|F6|F6|  
|エディター内またはデザイナー内の前のドキュメントに移動する|Ctrl + Shift + F6<br /><br /> Ctrl + Shift + Tab|Ctrl + Shift + F6<br /><br /> Ctrl + Shift + Tab|  
|ドキュメントの分割ペイン ビューの前のペインに移動する|Shift + F6|Shift + F6|  
|表示履歴内の前のページを表示する|Alt + ←|Alt + ←|  
|表示履歴内の次のページを表示する|Alt + →|Alt + →|  
|メニューまたはダイアログ ボックスを閉じるか、実行中の操作を取り消すか、または現在のウィンドウにフォーカスを設定する|Esc|同等の機能がありません|  
  
## <a name="solution-explorer-keyboard-shortcuts"></a>ソリューション エクスプローラーのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|ソリューション エクスプローラーを表示する|Ctrl + Alt + L|Ctrl + Alt + L|  
|新しいファイルを作成するための **[新しいファイル]** ダイアログ ボックスを表示する|Ctrl + N|Ctrl + N|  
|新しいプロジェクトを作成するための **[新しいプロジェクト]** ダイアログ ボックスを表示する|Ctrl + Shift + N|Ctrl + Shift + N|  
|既存のファイルを開くための **[ファイルを開く]** ダイアログ ボックスを表示する|Ctrl + O|Ctrl + O|  
|選択したオブジェクトの名前を変更する|F2|同等の機能がありません|  
  
## <a name="help-and-books-online-keyboard-shortcuts"></a>ヘルプとオンライン ブックのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|ヘルプ|F1<br /><br /> または<br /><br /> Shift + F1|F1|  
|SQL Server オンライン ブックを表示する|Ctrl + F1|同等の機能がありません|  
|ヘルプ ライブラリ マネージャーを開く|Ctrl + Alt + F1|該当するショートカットはありません|  
|SQL Server リソース センター Web ページを表示する|Ctrl + Alt + F2|同等の機能がありません|  
|現在のエディター ウィンドウのヘルプを表示する|Shift + F1|同等の機能がありません|  
|[操作方法] のヘルプを表示する|同等の機能がありません|Ctrl + F1|  
|オンライン ブックの目次を表示する|同等の機能がありません|Ctrl + Alt + F1|  
|オンライン ブックの索引を表示する|同等の機能がありません|Ctrl + Alt + F2|  
|ヘルプの [検索] を表示する|同等の機能がありません|Ctrl + Alt + F3|  
|ダイナミック ヘルプを表示する|同等の機能がありません|Ctrl + Alt + F4|  
|ヘルプの [お気に入り] を表示する|同等の機能がありません|Ctrl + Alt + F|  
  
## <a name="search-keyboard-shortcuts"></a>検索のキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|**[検索]** ダイアログ ボックスを表示する|Ctrl + F|CTRL + F|  
|**[検索]** ダイアログ ボックスの **[ファイル内]** タブを表示する|||  
|選択した記号の定義を表示する|F12|同等の機能がありません|  
|選択した記号の参照の一覧を表示する|Shift + F12|同等の機能がありません|  
|**[置換]** ダイアログ ボックスを表示する|Ctrl + H|Ctrl + H|  
|インクリメンタル検索を開始する (検索する文字列を入力するか、Ctrl + I キーを押して前の検索で抽出された文字列を検索する)|Ctrl + I|Ctrl + I|  
|前の検索テキストの次の出現箇所を検索する|F3|F3|  
|検索テキストの前の出現箇所を検索する|Shift + F3|Shift + F3|  
|現在選択しているテキストの次の出現箇所を検索する|Ctrl + F3|Ctrl + F3|  
|現在選択しているテキストの前の出現箇所を検索する|Ctrl + Shift + F3|Ctrl + Shift + F3|  
|**[フォルダーを指定して置換]** ダイアログ ボックスを表示する|Ctrl + Shift + H|Ctrl + Shift + H|  
|インクリメンタル検索を反転して、ファイルの末尾から上に向かって検索する|Ctrl + Shift + I|Ctrl + Shift + I|  
|**[検索と置換]** の **[上へ検索]** オプションをオンまたはオフにする|Alt + F3、B|Alt + F3、B|  
|**[フォルダーを指定して検索]** による検索を停止する|Alt + F3、S|Alt + F3、S|  
|**[検索と置換]** の **[単語単位]** オプションをオンまたはオフにする|Alt + F3、W|Alt + F3、W|  
|**[検索と置換]** の **[ワイルドカード]** オプションをオンまたはオフにする|Alt + F3、P|Alt + F3、P|  
|[標準] ツール バーの [検索/コマンド] ボックスにキャレットを配置する|Ctrl + /|同等の機能がありません|  
  
## <a name="cut-and-paste-keyboard-shortcuts"></a>切り取りと貼り付けのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|切り取る (現在選択している項目を削除してクリップボードに配置する)|Ctrl + X<br /><br /> または<br /><br /> Shift + Delete|Ctrl + X<br /><br /> または<br /><br /> Shift + Del|  
|選択された行をすべて切り取る。何も選択されていない場合は現在の行を切り取る。|CTRL + L<br /><br /> または<br /><br /> Ctrl + Shift + L|同等の機能がありません|  
|クリップボードにコピーする|Ctrl + C<br /><br /> または<br /><br /> Ctrl + Ins|CTRL キーを押しながら C<br /><br /> または<br /><br /> Ctrl + Ins|  
|クリップボードから挿入ポイントに貼り付ける|Ctrl + V<br /><br /> または<br /><br /> Shift + Ins|Ctrl + V<br /><br /> または<br /><br /> Shift + Ins|  
|挿入ポイントにクリップボード リングから項目を貼り付け、貼り付けた項目を自動的に選択する|Ctrl + Shift + V<br /><br /> または<br /><br /> Ctrl + Shift + Insert|同等の機能がありません|  
  
## <a name="log-viewer-keyboard-shortcuts"></a>ログ ビューアーのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|更新|同等の機能がありません|F5|  
|**[ログの選択]** ペインと **[ログ ファイルの概要]** ペインの間を移動する|同等の機能がありません|F6|  
|**[ログ ファイルの概要]** ペインに移動する|同等の機能がありません|Alt + S|  
|新しいログを読み込む|同等の機能がありません|Ctrl + Shift + L|  
|ログをエクスポートする|同等の機能がありません|Ctrl + Shift + E|  
|ログにフィルターを適用する|同等の機能がありません|Ctrl + Shift + F|  
|ログの中を検索する|同等の機能がありません|Ctrl + Shift + S|  
  
## <a name="activity-monitor-keyboard-shortcuts"></a>利用状況モニターのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|利用状況モニターの起動|Ctrl + Alt + A|Ctrl + Alt + A|  
|利用状況モニターを閉じる|Ctrl + F4|Ctrl + F4|  
|Refresh|F5|F5|  
|モニター表示にフィルターを適用する|Ctrl + Shift + F|Ctrl + Shift + F|  
|パネルを順番に表示する|F6|F6|  
|選択したペインの展開または折りたたみ|Ctrl を押しながら + または -|Ctrl を押しながら + または -|  
|すべてのペインの展開または折りたたみ|+ または -|+ または -|  
|グリッド内の選択した行全体をコピー|CTRL キーを押しながら C|CTRL キーを押しながら C|  
|セルをコピー|Ctrl + Shift + C|Ctrl + Shift + C|  
|グリッド内でのフィルター処理のためのドロップダウン|Alt + 下方向キー|Alt + 下方向キー|  
|利用状況モニターを上下にスクロール|Ctrl + Alt + 上方向/下方向キー|Ctrl + Alt + 上方向/下方向キー|  
  
## <a name="replication-monitor-keyboard-shortcuts"></a>レプリケーション モニターのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|Refresh|F5|F5|  
|グリッドから詳細ウィンドウを開く|Enter|Enter|  
  
## <a name="replication-conflict-viewer-keyboard-shortcuts"></a>レプリケーション競合表示モジュールのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|フィルターを定義する|F6|F6|  
|フィルターを適用する|F7|F7|  
|すべての列を表示|F8|F8|  
  
## <a name="query-designer-keyboard-shortcuts"></a>クエリ デザイナーのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|現在実行中のクエリを取り消すか停止する|Ctrl + T|Ctrl + T|  
|**クエリ デザイナー**のダイアグラム ペインを表示する|Ctrl + 1|Ctrl + 1|  
|**クエリ デザイナー**の条件ペインを表示する|Ctrl + 2|Ctrl + 2|  
|**クエリ デザイナー**の SQL ペインを表示する|Ctrl + 3|Ctrl + 3|  
|**クエリ デザイナー**の結果ペインを表示する|Ctrl + 4|Ctrl + 4|  
|**クエリ デザイナー**で指定されているクエリを実行する|Ctrl + R|Ctrl + R|  
|結果ペインで、デザイナーの下部にドッキングされているツール ストリップにフォーカスを移動する|Ctrl + G|Ctrl + G|  
|**クエリ デザイナー**で JOIN モードを有効にする|Ctrl + Shift + J|Ctrl + Shift + J|  
  
## <a name="designer-keyboard-shortcuts"></a>デザイナーのキーボード ショートカット  
  
|操作|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|------------|-----------------------------|---------------------------------|  
|デザイン画面で選択したコントロールを 8 単位ずつ下に移動する|下方向キー|同等の機能がありません|  
|デザイン画面で選択したコントロールを 8 単位ずつ左に移動する|左方向キー|同等の機能がありません|  
|デザイン画面で選択したコントロールを 8 単位ずつ右に移動する|右矢印|同等の機能がありません|  
|デザイン画面で選択したコントロールを 8 単位ずつ上に移動する|↑|同等の機能がありません|  
|選択したコントロールの高さを 8 単位ずつ高くする|Shift + ↓|同等の機能がありません|  
|選択したコントロールの幅を 8 単位ずつ狭くする|Shift + ←|同等の機能がありません|  
|選択したコントロールの幅を 8 単位ずつ広くする|Shift + →|同等の機能がありません|  
|選択したコントロールの高さを 8 単位ずつ低くする|Shift + ↑|同等の機能がありません|  
|ページ上の次のコントロールに移動する|Tab|同等の機能がありません|  
|ページ上の前のコントロールに移動する|Shift + Tab|同等の機能がありません|  
|デザイン画面にグリッドを表示する|Enter|同等の機能がありません|  
  
## <a name="see-also"></a>関連項目  
 [メニューとショートカット キーのカスタマイズ](customize-menus-and-shortcut-keys.md)  
  
  
