---
title: デタッチとアタッチを使用してデータベースを移動する方法 (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 517814aa9878206fa46c4ce8ea775cda18265ede
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095253"
---
# <a name="move-a-database-using-detach-and-attach-transact-sql"></a>デタッチとアタッチを使用してデータベースを移動する方法 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でデタッチしたデータベースを別の場所に移動し、同じまたは異なるサーバー インスタンスに再アタッチする方法について説明します。 ただし、データベースを移動するときは、デタッチとアタッチではなく、ALTER DATABASE による計画的再配置手順を使用することをお勧めします。 詳細については、「 [ユーザー データベースの移動](../../relational-databases/databases/move-user-databases.md)」を参照してください。  
  
> [!IMPORTANT]  
>  不明なソースや信頼されていないソースからデータベースをアタッチまたは復元しないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-move-a-database-by-using-detach-and-attach"></a>デタッチとアタッチを使用してデータベースを移動するには  
  
1.  データベースをデタッチします。 詳細については、「 [データベースのデタッチ](../../relational-databases/databases/detach-a-database.md)」を参照してください。  
  
2.  Windows エクスプローラーまたは Windows コマンド プロンプト ウィンドウで、デタッチされたデータベース ファイルとログ ファイルを新しい場所に移動します。  
  
     新しいログ ファイルを作成する場合でも、ログ ファイルを移動する必要があります。 場合によっては、データベースの再アタッチに既存のログ ファイルが必要になります。 したがって、デタッチしたログ ファイルを使わずにデータベースを正常にアタッチできるまで、デタッチしたログ ファイルは必ずすべて保管しておいてください。  
  
    > [!NOTE]  
    >  ログ ファイルを指定せずにデータベースのインポートを試みると、アタッチ操作は元の場所でログ ファイルを検索します。 ログのコピーが依然として元の場所にある場合は、そのコピーがアタッチされます。 元のログ ファイルが使用されないようにするには、新しいログ ファイルのパスを指定するか、ログ ファイルの元のコピーを (新しい場所にコピーした後で) 削除します。  
  
3.  コピーしたファイルをアタッチします。 詳細については、「 [Attach a Database](../../relational-databases/databases/attach-a-database.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] という `MyAdventureWorks`データベースのコピーを作成しています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、アタッチするサーバー インスタンスに接続されたクエリ エディター ウィンドウで実行しています。  
  
1.  次の [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] ステートメントを実行して [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースをデタッチします。  
  
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
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
