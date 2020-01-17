---
title: Transact-SQL デバッガーの実行
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, sysadmin requirement
- Transact-SQL debugger, supported versions
- Query Editor [Database Engine], right-click menu
- Transact-SQL debugger, Query Editor shortcut menu
- Transact-SQL debugger, stopping
- Transact-SQL debugger, Debug menu
- Transact-SQL debugger, Debug toolbar
- Transact-SQL debugger, keyboard shortcuts
- Transact-SQL debugger, starting
ms.assetid: 386f6d09-dbec-4dc7-9e8a-cd9a4a50168c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 843bd1c4213b6cb50c843b846cd9f5d95529b4b1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243703"
---
# <a name="run-the-transact-sql-debugger"></a>Transact-SQL デバッガーの実行
  
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウを開いた後に起動できます。 次に、デバッガーを停止するまで、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コードをデバッグ モードで実行できます。 オプションを設定して、デバッガーの実行方法をカスタマイズできます。  
  
## <a name="starting-and-stopping-the-debugger"></a>デバッガーの起動と停止  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーを起動するための要件は次のとおりです。  
  
-   
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターが別のコンピューターの [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続されている場合、デバッガーはリモート デバッグ用に構成されています。 詳細については、「 [Transact-sql デバッガーの構成](configure-firewall-rules-before-running-the-tsql-debugger.md)」を参照してください。  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] が、sysadmin 固定サーバー ロールのメンバーである Windows アカウントで実行されている必要があります。  
  
-   
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが、sysadmin 固定サーバー ロールのメンバーである Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインを使用して接続されている必要があります。  
  
-   
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディター ウィンドウが、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 2 (SP2) 以降の [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のインスタンスに接続されている必要があります。 クエリ エディター ウィンドウがシングル ユーザー モードのインスタンスに接続されているときは、デバッガーを実行できません。  
  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] コードのデバッグは、次の理由により、実稼働サーバーではなくテスト サーバーで行うことをお勧めします。  
  
-   デバッグは高度な権限を必要とする操作です。 このため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でデバッグを行うことができるのは、sysadmin 固定サーバー ロールのメンバーのみです。  
  
-   いくつかの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの処理を調査するときに、デバッグ セッションが長時間に及ぶことがあります。 セッションによって取得されたロック (たとえば更新ロック) が、セッションが終了するかトランザクションがコミットまたはロールバックされるまで、長時間保持される場合があります。  
  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーを起動すると、クエリ エディター ウィンドウがデバッグ モードになります。 クエリ エディター ウィンドウがデバッグ モードになると、デバッガーは最初のコード行で一時停止します。 この段階で、コードをステップ実行することも、特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで実行を一時停止することもできます。デバッガー ウィンドウを使用して現在の実行状態を表示することもできます。 デバッガーは、 **[クエリ]** ツール バーの **[デバッグ]** ボタンをクリックするか、または **[デバッグ]** メニューの **[デバッグ開始]** をクリックすることで開始できます。  
  
 クエリ エディター ウィンドウは、クエリ エディター ウィンドウ内の最後のステートメントが完了するか、またはデバッグ モードを自分で終了するまで、デバッグ モードに保たれます。 デバッグ モードとステートメントの実行を停止するには、次のいずれかの操作を行います。  
  
-   
  **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
-   
  **[デバッグ]** ツール バーの **[デバッグの停止]** ボタンをクリックする。  
  
-   
  **[クエリ]** メニューの **[クエリ実行のキャンセル]** をクリックする。  
  
-   
  **[クエリ]** ツール バーの **[クエリ実行のキャンセル]** ボタンをクリックする。  
  
 また、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [デバッグ] **メニューの** [すべてデタッチ] **をクリックすると、デバッグ モードを停止し、残りの** ステートメントを実行できます。  
  
## <a name="controlling-the-debugger"></a>デバッガーの制御  
 次のメニュー コマンド、ツール バー、およびショートカットを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーの動作を制御できます。  
  
-   
  **[デバッグ]** メニューおよび **[デバッグ]** ツール バー。 
  **[デバッグ]** メニューと **[デバッグ]** ツール バーは、開いているクエリ エディター ウィンドウにフォーカスが設定されるまで、どちらも非アクティブ状態です。 現在のプロジェクトが閉じられるまで、アクティブ状態に保たれます。  
  
-   デバッガーのキーボード ショートカット。  
  
-   クエリ エディターのショートカット メニュー。 ショートカット メニューは、クエリ エディター ウィンドウ内の行を右クリックすると表示されます。 クエリ エディター ウィンドウがデバッグ モードのとき、ショートカット メニューには、選択された行または文字列に適用できるデバッガー コマンドが表示されます。  
  
-   デバッガーによって開かれたウィンドウ (たとえば **[ウォッチ]** ウィンドウや **[ブレークポイント]** ウィンドウ) のメニュー項目およびコンテキスト コマンド。  
  
 デバッガーのメニュー コマンド、ツール バー ボタン、およびキーボード ショートカットを次の表に示します。  
  
|[デバッグ] メニューのコマンド|エディターのショートカット コマンド|ツール バー ボタン|キーボード ショートカット|操作|  
|------------------------|-----------------------------|--------------------|-----------------------|------------|  
|**Windows/ブレークポイント**|不可|**区切り**|Ctrl + Alt + B|
  **[ブレークポイント]** ウィンドウを表示します。このウィンドウでは、ブレークポイントの表示と管理を行うことができます。|  
|**Windows/Watch/ウォッチポイント**|不可|**[ブレークポイント]/[ウォッチ]/[ウォッチ式]**|Ctrl + Alt + W、1|
  **[ウォッチ 1]** ウィンドウを表示します。|  
|**Windows/Watch/Watch2**|不可|**[ブレークポイント]/[ウォッチ]/[Watch2]**|Ctrl</localizedText> + <localizedText>Alt</localizedText> + <localizedText>W</localizedText>、<localizedText>2|
  **[ウォッチ 2]** ウィンドウを表示します。|  
|**Windows/Watch/Watch3**|不可|**[ブレークポイント]/[ウォッチ]/[Watch3]**|Ctrl</localizedText> + <localizedText>Alt</localizedText> + <localizedText>W</localizedText>、<localizedText>3|
  **[ウォッチ 3]** ウィンドウを表示します。|  
|**Windows/Watch/[ウォッチ4**|不可|**[ブレークポイント]/[ウォッチ]/[[ウォッチ 4]**|Ctrl + Alt + W、4|
  **[ウォッチ 4]** ウィンドウを表示します。|  
|**Windows/ローカル**|不可|**[ブレークポイント]/[ローカル]**|Ctrl + Alt + V、L|[**ローカル**] ウィンドウを表示します。|  
|**Windows/呼び出し履歴**|不可|**[ブレークポイント]/[呼び出し履歴]**|Ctrl + Alt + C|[**呼び出し履歴**] ウィンドウを表示します。|  
|**Windows/スレッド**|不可|**ブレークポイント/スレッド**|Ctrl + Alt + H|[**スレッド**] ウィンドウを表示します。|  
|**まま**|不可|**まま**|Alt + F5|次のブレークポイントまで実行する。 [**続行**] は、デバッグモードのクエリエディターウィンドウにフォーカスがあるまではアクティブになりません。|  
|**デバッグの開始**|不可|**デバッグの開始**|Alt + F5|クエリ エディター ウィンドウをデバッグ モードにし、最初のブレークポイントまで実行します。 デバッグ モードのクエリ エディター ウィンドウにフォーカスを移した場合、 **[デバッグ開始]** は **[続行]** に切り替わります。|  
|**すべて中断**|不可|**すべて中断**|Ctrl + Alt + Break|この機能は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは使用できません。|  
|**デバッグの停止**|不可|**デバッグの停止**|SHIFT + F5|クエリ エディター ウィンドウをデバッグ モードから通常モードに切り替えます。|  
|**すべてデタッチ**|不可|不可|不可|デバッグ モードを終了しますが、クエリ エディター ウィンドウ内の残りのステートメントを実行します。|  
|**ステップイン**|不可|**ステップイン**|F11|次のステートメントを実行します。次のステートメントがストアド プロシージャ、トリガー、または関数を実行する場合は、新しいクエリ エディター ウィンドウをデバッグ モードで開きます。|  
|**ステップオーバー**|不可|**ステップオーバー**|F10|関数、ストアド プロシージャ、またはトリガーがデバッグされない点を除き、 **[ステップ イン]** と同じです。|  
|**ステップアウト**|不可|**ステップアウト**|SHIFT + F11|ブレークポイントで一時停止することなく、トリガー、関数、またはストアド プロシージャ内の残りのコードを実行します。 モジュールを呼び出したコードに制御が返されると、通常のデバッグ モードが再開されます。|  
|不可|**実行先**G|不可|Ctrl + F10|ブレークポイントで停止することなく、前回の停止位置から現在のカーソル位置までのすべてのコードを実行します。|  
|**[クイックウォッチ**|**[クイックウォッチ**|不可|Ctrl + Alt + Q|
  **[クイック ウォッチ]** ウィンドウを表示します。|  
|**ブレークポイントの設定/解除**|**[ブレークポイント]/[ブレークポイントの挿入]**|不可|F9|現在の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントまたは選択されているステートメントにブレークポイントを配置します。|  
|不可|**ブレークポイント/ブレークポイントの削除**|不可|不可|選択されている行からブレークポイントを削除します。|  
|不可|**ブレークポイント/ブレークポイントの無効化**|不可|不可|選択されている行のブレークポイントを無効にします。 ブレークポイントはコード行に設定されたままですが、再び有効にするまで実行は停止されません。|  
|不可|**ブレークポイント/ブレークポイントの有効化**|不可|不可|選択されている行のブレークポイントを有効にします。|  
|**すべてのブレークポイントの削除**|不可|不可|CTRL + SHIFT + F9|すべてのブレークポイントを削除します。|  
|**すべてのブレークポイントの無効化**|不可|不可|不可|すべてのブレークポイントを無効にします。|  
|不可|**ウォッチ式の追加**|不可|不可|選択されている式を **[ウォッチ]** ウィンドウに追加します。|  
  
## <a name="see-also"></a>参照  
 [Transact-sql デバッガー](transact-sql-debugger.md)   
 [Transact-sql コードのステップ実行](step-through-transact-sql-code.md)   
 [Transact-sql デバッガー情報](transact-sql-debugger-information.md)   
 [データベースエンジンクエリエディター &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)  
  
  
