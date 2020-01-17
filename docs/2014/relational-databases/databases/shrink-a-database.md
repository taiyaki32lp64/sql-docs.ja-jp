---
title: データベースの圧縮 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.shrinkdatabase.f1
helpviewer_keywords:
- shrinking databases
- databases [SQL Server], shrinking
- decreasing database size
- database shrinking [SQL Server]
- reducing database size
ms.assetid: 83afbf74-fd50-4c39-831c-b1f473a50620
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21f58cd6991b760edeefb81c37e02c617f8e09cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917009"
---
# <a name="shrink-a-database"></a>データベースの圧縮
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] から [!INCLUDE[tsql](../../includes/tsql-md.md)]のオブジェクトを使用して、データベースを圧縮する方法について説明します。  
  
 ファイルの末尾にあるデータのページを、ファイルの先頭に近い占有されていない領域に移動することにより、データ ファイルが圧縮され、領域が回復されます。 ファイル末尾に十分な空き領域が作成された場合は、ファイル末尾のデータ ページの割り当てを解除して、ファイル システムに戻すことができます。  
  

  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベースは、そのデータベースの最小サイズより小さくすることはできません。 最小サイズは、データベースが最初に作成されたときに指定されたサイズか、DBCC SHRINKFILE などのファイル サイズ変更操作によって最後に明示的に設定されたサイズのいずれかになります。 たとえば、作成時にサイズを 10 MB に指定したデータベースが 100 MB まで拡張した場合、データベース内のすべてのデータを削除したとしても、縮小できる限界は 10 MB までです。  
  
-   データベースのバックアップ中、データベースを圧縮することはできません。 逆に、データベースの圧縮操作の進行中、データベースをバックアップすることはできません。  
  
-   DBCC SHRINKDATABASE は、xVelocity メモリ最適化列ストア インデックスを検出すると失敗します。 列ストア インデックスを検出する前に完了した処理は成功するので、データベースが小さくなる場合があります。 DBCC SHRINKDATABASE を完了するには、DBCC SHRINKDATABASE を実行する前にすべての列ストア インデックスを無効にし、後で列ストア インデックスを再構築します。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   データベース内にある現在の空き (未割り当て) 領域の大きさを確認します。 詳細については、「 [データベースのデータ領域とログ領域情報の表示](display-data-and-log-space-information-for-a-database.md)」をご覧ください。  
  
-   データベースを圧縮する場合は次のことを考慮してください。  
  
    -   圧縮操作は、テーブルの切り捨てやテーブルの削除操作など、大きな未使用領域を生成する操作の後に実行すると最も効果的です。  
  
    -   ほとんどのデータベースでは、毎日の定期的操作で使用するための空き領域が必要です。 データベースを何度圧縮しても、データベースのサイズが大きくなってしまう場合は、通常の操作にそれだけの領域が必要であることを示しています。 このような場合、繰り返しデータベースを圧縮することは無意味です。  
  
    -   圧縮操作では、データベース内のインデックスの断片化状態は保持されず、一般に、断片化の程度が大きくなります。 この理由からも、データベースを繰り返し圧縮することはお勧めできません。  
  
    -   特別な要件がない限り、AUTO_SHRINK データベース オプションを ON に設定しないでください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-shrink-a-database"></a>データベースを圧縮するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、圧縮するデータベースを右クリックします。  
  
3.  **[タスク]** 、 **[圧縮]** の順にポイントし、 **[データベース]** をクリックします。  
  
     **[データベース]**  
     選択しているデータベースの名前が表示されます。  
  
     **[現在割り当てられている領域]**  
     選択されているデータベースの使用済み領域と未使用領域の合計を表示します。  
  
     **[使用可能な空き領域]**  
     選択されているデータベースのログ ファイルおよびデータ ファイル内の空き領域の合計を表示します。  
  
     **[未使用領域の解放前にファイルを再構成する]**  
     このオプションをオンにすることは、目的のパーセント オプションを指定して DBCC SHRINKDATABASE を実行することと同じです。 このオプションをオフにすると、TRUNCATEONLY オプションを使用して DBCC SHRINKDATABASE を実行するのと同じ効果があります。 既定では、ダイアログが開いたときに、このオプションはオフに設定されます。 このオプションをオンにした場合、ユーザーは目的のパーセント オプションを指定する必要があります。  
  
     **[圧縮後のファイルの最大空き領域]**  
     データベースを圧縮した後に、データベース ファイル内に残す空き領域の最大パーセンテージを入力します。 0 ～ 99 の値を指定できます。  
  
4.  **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-shrink-a-database"></a>データベースを圧縮するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [DBCC SHRINKDATABASE](/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql) を使用して、 `UserDB` データベース内のデータ ファイルとログ ファイルのサイズを圧縮し、データベースの空き領域が `10` % になるようにします。  
  
 [!code-sql[DBCC#DBCC_SHRINKDB1](../../snippets/tsql/SQL14/tsql/dbcc/transact-sql/dbcc_other.sql#dbcc_shrinkdb1)]  
  
##  <a name="FollowUp"></a>補足情報: データベースを圧縮した後  
 ファイルを圧縮するために移動されたデータは、ファイル内のあらゆる使用可能な場所に分散される場合があります。 これにより、インデックスの断片化が発生し、広範なインデックスを検索するクエリのパフォーマンスが低下する場合があります。 断片化を解消するには、圧縮後にファイルのインデックスを再構築することを検討してください。  
  
## <a name="see-also"></a>関連項目  
 [ファイルの圧縮](shrink-a-file.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)   
 [データベース ファイルとファイル グループ](database-files-and-filegroups.md)  
  
  
