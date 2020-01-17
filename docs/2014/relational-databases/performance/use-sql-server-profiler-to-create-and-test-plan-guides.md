---
title: SQL Server Profiler を使用したプラン ガイドの作成とテスト | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- checking plan guides
- plan guides [SQL Server], testing
- plan guides [SQL Server], SQL Server Profiler
- matching queries to plan guides [SQL Server]
- testing plan guides
- SQL Server Profiler, plan guides
- plan guides [SQL Server], creating
- capturing query text [SQL Server]
- verifying plan guides
- Profiler [SQL Server Profiler], plan guides
- query-to-plan guide matching [SQL Server]
ms.assetid: 7018dbf0-1a1a-411a-88af-327bedf9cfbd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fcdbfe9f9289ab9cc529d4d37eb27d877dfff3ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150489"
---
# <a name="use-sql-server-profiler-to-create-and-test-plan-guides"></a>SQL Server Profiler を使用したプラン ガイドの作成とテスト
  プラン ガイドを作成するとき、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] sp_create_plan_guide *ストアド プロシージャの* statement_text **引数に使用するために、** を使用して正確なクエリ テキストをキャプチャできます。 これにより、コンパイル時にプラン ガイドをクエリに一致させることができます。 プラン ガイドを作成した後、プラン ガイドが実際にクエリに一致することをテストするためにも [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用できます。 通常、クエリがプラン ガイドに一致することを確認するには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用してプラン ガイドをテストする必要があります。  
  
## <a name="capturing-query-text-by-using-sql-server-profiler"></a>SQL Server Profiler を使用したクエリ テキストのキャプチャ  
 クエリを実行し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]に送信されたテキストを正確にキャプチャすると、そのクエリ テキストに正確に一致する SQL 型または TEMPLATE 型のプラン ガイドを作成できます。 これにより、このプラン ガイドをクエリ オプティマイザーに使用させることができます。  
  
 スタンドアロン バッチとしてアプリケーションから送信される次のクエリについて考えてみます。  
  
```  
SELECT COUNT(*) AS c  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d  
  ON h.SalesOrderID = d.SalesOrderID  
WHERE h.OrderDate BETWEEN '20000101' and '20050101';  
```  
  
 マージ結合操作を使用してこのクエリを実行する必要がありますが、クエリでマージ結合を使用しないことを SHOWPLAN が示しているとします。 アプリケーションでクエリを直接変更することはできませんが、代わりにプラン ガイドを作成して、コンパイル時に MERGE JOIN クエリ ヒントがクエリに追加されるように指定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が受信したクエリのテキストを正確にキャプチャするには、次の手順に従います。  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレースを開始し、イベントの種類として **SQL:BatchStarting** が選択されていることを確認します。  
  
2.  アプリケーションでクエリを実行します。  
  
3.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレースを一時停止します。  
  
4.  クエリに対応する **SQL:BatchStarting** イベントをクリックします。  
  
5.  イベントを右クリックして **[イベント データの抽出]** をクリックします。  
  
    > [!IMPORTANT]  
    >  SQL Server Profiler のトレース ウィンドウ内の下のペインで、バッチ テキストを選択してコピーすることは避けてください。 作成するプラン ガイドが元のバッチと一致しなくなる場合があります。  
  
6.  ファイルにイベント データを保存します。 バッチ テキストが保存されます。  
  
7.  メモ帳でバッチ テキスト ファイルを開き、テキストをクリップボードにコピーします。  
  
8.  プラン ガイドを作成し、**@stmt**引数に指定する引用符 ( **@stmt** ') 内にコピーしたテキストを貼り付けます。 **@stmt** 引数内に単一引用符がある場合は、その前にもう 1 つ単一引用符を追加してエスケープする必要があります。 単一引用符を挿入する際は、別の文字を追加したり削除したりしないように注意してください。 たとえば、日付リテラル **'** 20000101 **'** は、 **''** 20000101 **''** として区切る必要があります。  
  
 次に、このプラン ガイドを示します。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'MyGuide1',  
    @stmt = N'<paste the text copied from the batch text file here>',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = NULL,  
    @hints = N'OPTION (MERGE JOIN)';  
```  
  
## <a name="testing-plan-guides-by-using-sql-server-profiler"></a>SQL Server Profiler を使用したプラン ガイドのテスト  
 プラン ガイドがクエリに一致することを確認するには、次の手順に従います。  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレースを開始し、イベントの種類として **Showplan XML** が選択されていることを確認します ( **[Performance]** ノードの下にあります)。  
  
2.  アプリケーションでクエリを実行します。  
  
3.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレースを一時停止します。  
  
4.  影響するクエリの **Showplan XML** イベントを検索します。  
  
    > [!NOTE]  
    >  **Showplan XML for Query Compile** イベントは使用できません。 **PlanGuideDB** はそのイベントに存在しません。  
  
5.  プラン ガイドが OBJECT 型または SQL 型の場合は、 **Showplan XML** イベントに、クエリと一致させるプラン ガイドの **PlanGuideDB** 属性と **PlanGuideName** 属性が含まれていることを確認します。 または、TEMPLATE プラン ガイドの場合は、 **Showplan XML** イベントに、クエリと一致させるプラン ガイドの **TemplatePlanGuideDB** 属性と **TemplatePlanGuideName** 属性が含まれていることを確認します。 これにより、プラン ガイドが機能していることを確認できます。 これらの属性は、プランの **\<StmtSimple>** 要素に含まれます。  
  
## <a name="see-also"></a>関連項目  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)  
  
  
