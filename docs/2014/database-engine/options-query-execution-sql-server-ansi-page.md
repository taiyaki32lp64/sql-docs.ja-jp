---
title: オプション (クエリ実行-SQL Server ANSI ページ) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAnsi
ms.assetid: 0f4c6887-0562-417e-806c-b5cffb1e7c5c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e075de106a66ffee63c02ead06a3fc68548111a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089378"
---
# <a name="options-query-execution-sql-server-ansi-page"></a>オプション (クエリ実行-SQL Server ANSI ページ)
  ユーザーのクエリや、トリガーやストアド プロシージャが実行されている間、これらの ANSI (ISO) 規格の SET オプションの組み合わせによってクエリ処理環境が定義されます。 ただし、これらの SET オプションに、ISO 規格に準拠するために必要なオプションがすべて含まれているとは限りません。 このページを使用すると、ISO 規格で指定されているすべての設定、または設定の一部が使用されたクエリを [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で実行するように指定できます。 このオプションに加えた変更は、新規の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリにのみ適用されます。 現在のクエリのオプションを変更するには、 **[クエリ]** メニューの **[クエリ オプション]** をクリックするか、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクエリ ウィンドウを右クリックして **[クエリ オプション]** をクリックします。 **[クエリ オプション]** ダイアログ ボックスで、 **[実行]** の下にある **[ANSI]** をクリックします。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **SET ANSI_DEFAULTS**  
 このチェック ボックスをオンにすると、既定の ISO 設定がすべて選択されます。 既定では、すべての ISO オプションが選択されるとは限りません。  
  
 **SET QUOTED_IDENTIFIER**  
 このチェック ボックスをオンにすると、識別子とリテラル文字列を区切る引用符に関する ISO 規則が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって遵守されます。 引用符で区切ることで、Transact-SQL の予約済みキーワードを識別子として指定することや、Transact-SQL の構文規則で通常は識別子として使用が認められていない文字を使用することができます。 既定では、このチェック ボックスはオンになっています。  
  
 **SET ANSI_NULL_DFLT_ON**  
 このチェック ボックスをオンにすると、CREATE TABLE ステートメントまたは ALTER TABLE ステートメントで明示的に NOT NULL に定義されなかったユーザー定義データ型または列が、すべて既定で NULL 値を許容するという設定になります。 既定では、このチェック ボックスはオンになっています。  
  
 **[SET IMPLICIT_TRANSACTIONS]**  
 このチェック ボックスをオンにすると、接続が暗黙のトランザクション モードに設定されます。 このチェック ボックスをオフにすると、接続は自動コミット トランザクション モードに戻ります。 暗黙のトランザクション モードが選択されているときに、暗黙のトランザクションを開始するステートメントについては、「[SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-implicit-transactions-transact-sql)」を参照してください。 既定では、このチェック ボックスはオフになっています。  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 このチェック ボックスをオンにすると、トランザクションがコミットされたときに、オープンしているカーソルが ISO に準拠して自動的にクローズします。 このチェック ボックスをオフにすると、トランザクションが変わってもカーソルはオープンしたままです。接続が終了するか、カーソルが明示的にクローズされたときだけカーソルがクローズします。 既定では、このチェック ボックスはオフになっています。  
  
 **SET ANSI_PADDING**  
 列に定義されているサイズよりも短い値の名前を列に格納する方法と、値の後に **char**、**varchar**、**binary**、**varbinary** データ型で空白が続いている値を列に格納する方法を指定します。 この設定は新しい列の定義にだけ影響します。 列が作成された後は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では列の作成時の設定に基づいて値が格納されます。 この設定を後で変更しても、既存の列には影響がありません。 既定では、このチェック ボックスはオンになっています。  
  
 **SET ANSI_WARNINGS**  
 複数のエラー条件に対して ISO 標準の動作をすることを指定します。  
  
-   このチェック ボックスをオンにすると、NULL 値が集計関数 (SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP、COUNT など) で使用されている場合に、警告メッセージが生成されます。 オフの場合は、警告メッセージは生成されません。  
  
-   このチェック ボックスをオフにすると、0 除算や演算オーバーフロー エラーが発生したときにステートメントがロールバックされ、エラー メッセージが生成されます。 オフの場合は、0 除算や演算オーバーフロー エラーが発生したときに NULL 値が返されます。 INSERT 処理または UPDATE 処理が **character**、**Unicode**、**binary** 型の列に対して実行され、新しい値が列の最大サイズより長くなると、0 除算や演算オーバーフロー エラーが原因となって NULL 値が返されます。 [SET ANSI_WARNINGS] がオンの場合は、INSERT 処理または UPDATE 処理は ISO 規格の指定に従って取り消されます。 文字型の列の末尾の空白文字とバイナリ列の末尾の NULL 値は無視されます。 OFF の場合、データは列のサイズに切り捨てられ、ステートメントは成功します。  
  
 既定では、このチェック ボックスはオンになっています。  
  
 **SET ANSI_NULLS**  
 -   等号 (=) 比較演算子と不等号 (<>) 比較演算子を NULL 値に対して使用した場合に ISO に準拠した動作をすることを指定します。 [SET ANSI_NULLS] がオンの場合、NULL 値に対する比較はすべて UNKNOWN として評価されます。これは ISO 準拠した動作です。 [SET ANSI_NULLS] がオフの場合、NULL 値に対するデータの比較はすべて TRUE に評価されます。 既定では、このチェック ボックスはオンになっています。  
  
 **既定値にリセット**  
 このページ上のすべての値を元の既定値にリセットします。  
  
  
