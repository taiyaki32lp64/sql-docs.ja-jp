---
title: クエリ エディターによる SQLCMD スクリプトの編集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], SQLCMD scripts
- SQLCMD scripts
- modifying scripts
- Query Editor [Database Engine], SQLCMD scripts
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: f77b866d-c330-47c9-9e74-0b8d8dff4b31
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7931e678db7e93dfea385b5ca905dd6968ec78eb
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263477"
---
# <a name="edit-sqlcmd-scripts-with-query-editor"></a>クエリ エディターによる SQLCMD スクリプトの編集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターを使用すると、クエリを SQLCMD スクリプトとして作成したり、編集したりできます。 Windows システムのコマンドと [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを同じスクリプトで処理する必要がある場合は、SQLCMD スクリプトを使用します。  
  
## <a name="sqlcmd-mode"></a>SQLCMD モード  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターで SQLCMD スクリプトの作成や編集を行うには、SQLCMD スクリプト モードを有効にする必要があります。 クエリ エディターの SQLCMD モードは、既定では有効ではありません。 スクリプト モードを有効にするには、ツール バーの **[SQLCMD モード]** アイコンをクリックするか、 **[クエリ]** メニューの **[SQLCMD モード]** をクリックします。  
  
> [!NOTE]  
>  SQLCMD モードを有効にすると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のクエリ エディターの IntelliSense および [!INCLUDE[ssDE](../../includes/ssde-md.md)] デバッガーが無効になります。  
  
 クエリ エディターで SQLCMD スクリプトを操作するときには、あらゆる [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトと同じ機能を使用できます。 使用できる機能には、次のようなものがあります。  
  
-   コードの色分け  
  
-   スクリプトの実行  
  
-   ソース管理  
  
-   スクリプトの解析  
  
-   Showplan  
  
## <a name="enable-sqlcmd-scripting-in-query-editor"></a>クエリ エディターで SQLCMD スクリプト操作を有効にする方法  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のアクティブなクエリ エディター ウィンドウで SQLCMD スクリプト操作を有効にするには、次の手順を実行します。  
  
#### <a name="to-switch-a-database-engine-query-editor-window-to-sqlcmd-mode"></a>データベース エンジンのクエリ エディター ウィンドウを SQLCMD モードに切り替えるには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックして **[新しいクエリ]** をクリックし、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディター ウィンドウを新しく開きます。  
  
2.  **[クエリ]** メニューの **[SQLCMD モード]** をクリックします。  
  
     クエリ エディター ウィンドウのコンテキストで **sqlcmd** ステートメントが実行されます。  
  
3.  **[SQL エディター]** ツール バーの **[使用できるデータベース]** の一覧で、[ [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]] データベースを選択します。  
  
4.  クエリ エディター ウィンドウに、次の 2 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと `!!DIR` **sqlcmd** ステートメントを入力します。  
  
    ```  
    SELECT DISTINCT Type FROM Sales.SpecialOffer;  
    GO  
    !!DIR  
    GO  
    SELECT ProductCategoryID, Name FROM Production.ProductCategory;  
    GO  
    ```  
  
5.  F5&lt;/localizedText&gt; キーを押して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと MS-DOS ステートメントが混在するセクション全体を実行します。  
  
     1 番目と 3 番目のステートメントにより、2 つの SQL 結果ペインが表示されます。  
  
6.  **結果** ペインの **[メッセージ]** タブをクリックし、3 つのステートメントすべてから取得されたメッセージを確認します。  
  
    -   (6 件処理されました)  
  
    -   \< ディレクトリ情報 >  
  
    -   (4 行処理されました)  
  
> [!IMPORTANT]  
>  コマンド ラインから実行すると、 **sqlcmd** ユーティリティではオペレーティング システムとの完全な対話が可能になります。 クエリ エディターを **SQLCMD モード**で使用する場合は、対話型のステートメントを実行しないように注意してください。 クエリ エディターは、オペレーティング システムのプロンプトに応答できません。  
  
 SQLCMD の実行方法の詳細については、「 [sqlcmd Utility](../../tools/sqlcmd-utility.md)」または SQLCMD のチュートリアルを参照してください。  
  
## <a name="enable-sqlcmd-scripting-by-default"></a>SQLCMD スクリプト操作を既定で有効にする方法  
 SQLCMD スクリプト操作を既定でオンにするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[クエリ実行]** 、 **[SQL Server]** の順に展開します。次に、 **[全般]** ページをクリックし、 **[既定で、新しいクエリを SQLCMD モードで開始する]** チェック ボックスをオンにします。  
  
## <a name="writing-and-editing-sqlcmd-scripts"></a>SQLCMD スクリプトの作成と編集  
 スクリプト モードを有効にしたら、SQLCMD コマンドと [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを作成できます。 この場合に当てはまる規則を以下に示します。  
  
-   SQLCMD コマンドは行の最初のステートメントでなければなりません。  
  
-   各行に 1 つの SQLCMD コマンドだけを記述できます。  
  
-   SQLCMD コマンドの前にコメントや空白文字を入れてもかまいません。  
  
-   コメント文字の間にはさまれた SQLCMD コマンドは実行されません。  
  
-   1 行のコメント文字は 2 つのハイフン (`--)` であり、行の先頭に置く必要があります。  
  
-   オペレーティング システム コマンドの前には 2 つの感嘆符 (`!!`) を置く必要があります。 2 つの感嘆符が付いたコマンドの場合は、感嘆符の後のステートメントが `cmd.exe` コマンド プロセッサによって実行されます。 `!!` の後のテキストは、 `cmd.exe`にパラメーターとして渡されるので、最終的に実行されるコマンド ラインは、 `"%SystemRoot%\system32\cmd.exe /c <text after !!>"`になります。  
  
-   SQLCMD コマンドと [!INCLUDE[tsql](../../includes/tsql-md.md)]の区別を明確にするために、すべての SQLCMD コマンドの先頭にはコロン (`:`) を付ける必要があります。  
  
-   `GO` コマンドは、先頭に文字を付けずに使用することも、 を付けて使用することもできます。 `!!:`  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターは、環境変数をサポートしており、また SQLCMD スクリプトの一部として定義されている変数もサポートしています。ただし、組み込みの SQLCMD 変数や **osql** 変数はサポートしていません。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で処理される SQLCMD では、変数の大文字と小文字が区別されます。 たとえば、PRINT '$(COMPUTERNAME)' では正しい結果になりますが、PRINT '$(ComputerName)' ではエラーが返されます。  
  
> [!CAUTION]
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、標準モードと SQLCMD モードの実行に [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SqlClient を使用します。 コマンド ラインから SQLCMD を実行する場合は、OLE DB プロバイダーを使用することになります。 同じクエリでも、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の SQLCMD モードで実行する場合と SQLCMD ユーティリティで実行する場合とでは、適用される既定のオプションが異なるので、動作も異なる可能性があります。  
  
## <a name="supported-sqlcmd-syntax"></a>サポートされている SQLCMD 構文  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターでは、以下の SQLCMD スクリプト キーワードをサポートしています。  
  
 `[!!:]GO[count]`  
  
 `!! <command>`  
  
 `:exit(statement)`  
  
 `:Quit`  
  
 `:r <filename>`  
  
 `:setvar <var> <value>`  
  
 `:connect server[\instance] [-l login_timeout] [-U user [-P password]]`  
  
 `:on error [ignore|exit]`  
  
 `:error <filename>|stderr|stdout`  
  
 `:out <filename>|stderr|stdout`  
  
> [!NOTE]  
>  `:error` と `:out`の場合、 `stderr` と `stdout` のどちらを指定しても、出力は [メッセージ] タブに送信されます。  
  
 クエリ エディターでは、上記以外の SQLCMD コマンドをサポートしていません。 サポートされていない SQLCMD キーワードが実行されると、サポートされていないキーワードごとに、"Ignoring command *\<ignored command*>" (<無視されたコマンド> コマンドを無視しています) メッセージがクエリ エディターから宛先に送信されます。 スクリプトは正常に実行されますが、サポートされていないコマンドは無視されます。  
  
> [!CAUTION]  
>  コマンド ラインから SQLCMD を実行する場合とは異なり、クエリ エディターの SQLCMD モードにはいくつかの制限事項があります。 まず、変数などのコマンド ライン パラメーターを受け渡すことができません。また、クエリ エディターはオペレーティング システムのプロンプトに応答できないため、対話型のステートメントを実行しないように注意してください。  
  
## <a name="color-coding-in-sqlcmd-scripts"></a>SQLCMD スクリプトのコードの色分け  
 SQLCMD スクリプト操作が有効になっていると、スクリプトのコードが色分けされます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] キーワードの色分けは変わりません。 SQLCMD コマンドは、背景が影付きになります。  
  
## <a name="example"></a>例  
 次の例では、現在のディレクトリを出力するために、 **sqlcmd** ステートメントを使用して testoutput.txt という出力ファイルを作成し、1 つのオペレーティング システム コマンドで 2 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] の SELECT ステートメントを実行しています。 結果ファイルには、 `DIR` ステートメントからのメッセージ出力に続いて、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントからの結果の出力が含まれます。  
  
```  
:out C:\testoutput.txt  
SELECT @@VERSION As 'Server Version'  
!!DIR  
!!:GO  
SELECT @@SERVERNAME AS 'Server Name'  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)  
  
  
