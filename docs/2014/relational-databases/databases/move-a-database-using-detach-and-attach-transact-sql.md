---
title: デタッチとアタッチを使用してデータベースを移動する方法 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- moving databases [SQL Server]
- database detaching [SQL Server]
- relocating databases [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 6732a431-cdef-4f1e-9262-4ac3b77c275e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16fa57c35c2c40d307b73809c21ccfbedc54f705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917095"
---
# <a name="move-a-database-using-detach-and-attach-transact-sql"></a>デタッチとアタッチを使用してデータベースを移動する方法 (Transact-SQL)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でデタッチしたデータベースを別の場所に移動し、同じまたは異なるサーバー インスタンスに再アタッチする方法について説明します。 ただし、データベースを移動するときは、デタッチとアタッチではなく、ALTER DATABASE による計画的再配置手順を使用することをお勧めします。 詳細については、「 [ユーザー データベースの移動](move-user-databases.md)」を参照してください。  
  
> [!IMPORTANT]  
>  不明なソースや信頼されていないソースからデータベースをアタッチまたは復元しないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-move-a-database-by-using-detach-and-attach"></a>デタッチとアタッチを使用してデータベースを移動するには  
  
1.  データベースをデタッチします。 詳細については、「 [データベースのデタッチ](detach-a-database.md)」を参照してください。  
  
2.  Windows エクスプローラーまたは Windows コマンド プロンプト ウィンドウで、デタッチされたデータベース ファイルとログ ファイルを新しい場所に移動します。  
  
    > [!NOTE]  
    >  単一ファイルのデータベースを移動する場合は、電子メールを使用できます。ただし、ファイル サイズが電子メールで対応できる大きさである場合に限られます。  
  
     新しいログ ファイルを作成する場合でも、ログ ファイルを移動する必要があります。 場合によっては、データベースの再アタッチに既存のログ ファイルが必要になります。 したがって、デタッチしたログ ファイルを使わずにデータベースを正常にアタッチできるまで、デタッチしたログ ファイルは必ずすべて保管しておいてください。  
  
    > [!NOTE]  
    >  ログ ファイルを指定せずにデータベースのインポートを試みると、アタッチ操作は元の場所でログ ファイルを検索します。 ログのコピーが依然として元の場所にある場合は、そのコピーがアタッチされます。 元のログ ファイルが使用されないようにするには、新しいログ ファイルのパスを指定するか、ログ ファイルの元のコピーを (新しい場所にコピーした後で) 削除します。  
  
3.  コピーしたファイルをアタッチします。 詳細については、「 [Attach a Database](attach-a-database.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例のコピーを作成する、[!INCLUDE[ssSampleDBnormal](../../includes/tsql-md.md)]ステートメントに接続されている、サーバー インスタンスがアタッチされているクエリ エディター ウィンドウで実行されます。  
  
1.  デタッチ、[!INCLUDE[ssSampleDBnormal](../../includes/tsql-md.md)]ステートメント。  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'AdventureWorks2012';  
    GO  
    ```  
  
2.  任意の方法で、データベース ファイル (AdventureWorks208R2_Data.mdf と AdventureWorks208R2_log) をC:\MySQLServer\AdventureWorks208R2_Data.mdf と C:\MySQLServer\AdventureWorks208R2_Log.ldf にそれぞれコピーします。  
  
    > [!IMPORTANT]  
    >  実稼動データベースの場合は、データベースとトランザクション ログを別のディスクに配置します。  
  
     ファイルをネットワーク経由でリモート コンピューターのディスクにコピーするには、そのリモート コンピューターの UNC (Universal Naming Convention) 名を使用します。 UNC 名の形式は、 **\\\\** _Servername_ **\\** _Sharename_ **\\** _Path_ **\\** _Filename_です。 ローカル ハード ディスクにファイルを書き込む場合と同様、リモート ディスクでのファイルの読み取りや書き込みに必要な適切な権限が、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで使用するユーザー アカウントに許可されている必要があります。  
  
3.  次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、移動したデータベースとログをアタッチします (ログのアタッチは省略できます)。  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Data.mdf'),  
        (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Log.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、新しくアタッチされたデータベースはオブジェクト エクスプローラーにすぐに表示されません。 このデータベースを表示するには、オブジェクト エクスプローラーで、 **[表示]** をクリックし、 **[最新の情報に更新]** をクリックします。 オブジェクト エクスプローラーの **[データベース]** ノードを展開すると、データベースの一覧に新しくアタッチされたデータベースが表示されるようになります。  
  
## <a name="see-also"></a>参照  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
