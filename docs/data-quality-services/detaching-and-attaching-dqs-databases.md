---
title: DQS データベースのデタッチとアタッチ
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 841e2991e672aa9c8a8ab74437fcd12fecdfaa2f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251679"
---
# <a name="detaching-and-attaching-dqs-databases"></a>DQS データベースのデタッチとアタッチ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  ここでは、DQS データベースをデタッチおよびアタッチする方法について説明します。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Limitations"></a>制限事項と制約事項  
 制限事項と制約事項の一覧については、「 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md)のデータベースをデタッチする方法について説明します。  
  
###  <a name="Prerequisites"></a>応募  
  
-   DQS で実行中のアクティビティまたはプロセスがないことを確認します。 これは **[アクティビティ監視]** 画面を使用して確認できます。 この画面の操作の詳細については、「 [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md)」を参照してください。  
  
-   
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]にログオンしているユーザーがいないことを確認します。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
  
-   DQS データベースをデタッチするには、Windows ユーザー アカウントが、SQL Server インスタンスの db_owner 固定サーバー ロールのメンバーであることが必要です。  
  
-   データベースをアタッチするには、Windows ユーザー アカウントに、CREATE DATABASE、CREATE ANY DATABASE、または ALTER ANY DATABASE の権限が必要です。  
  
-   DQS の実行中のアクティビティを終了させたり実行中のプロセスを停止させたりするには、DQS_MAIN データベースの dqs_administrator ロールが必要です。  
  
##  <a name="Detach"></a>DQS データベースのデタッチ  
 SQL Server Management Studio を使用して DQS データベースをデタッチすると、デタッチされたファイルはコンピューターに残り、同じ SQL Server インスタンスに再アタッチすることも、別のサーバーに移動して、そこにアタッチすることもできます。 DQS データベース ファイルは通常、Data Quality Services コンピューターの C:\Program Files\Microsoft SQL Server\MSSQL13.*<インスタンス名>* \MSSQL\DATA にあります。  
  
1.  Microsoft SQL Server Management Studio を起動し、適切な SQL Server インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、 **[データベース]** ノードを展開します。  
  
3.  
  **DQS_MAIN** データベースを右クリックして **[タスク]** をポイントし、 **[デタッチ]** をクリックします。 
  **[データベースのデタッチ]** ダイアログ ボックスが表示されます。  
  
4.  
  **[削除]** 列の下にあるチェック ボックスをオンにし、 **[OK]** をクリックして DQS_MAIN データベースをデタッチします。  
  
5.  DQS_PROJECTS データベースと DQS_STAGING_DATA データベースで手順 3. と 4. を繰り返し、それらをデタッチします。  
  
 Transact-SQL ステートメントで sp_detach_db ストアド プロシージャを使用して、DQS データベースをデタッチすることもできます。 Transact-SQL ステートメントを使用したデータベースのデタッチに関する詳細については、「 [Using Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) 」の「 [Detach a Database](../relational-databases/databases/detach-a-database.md)」を参照してください。  
  
##  <a name="Attach"></a>DQS データベースをアタッチする  
 次の手順を使用して、DQS データベースを (デタッチした場所から) 同じ SQL Server インスタンスまたは [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] がインストールされている別の SQL Server インスタンスにアタッチします。  
  
1.  Microsoft SQL Server Management Studio を起動し、適切な SQL Server インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、 **[データベース]** を右クリックし、 **[アタッチ]** をクリックします。 
  **[データベースのデタッチ]** ダイアログ ボックスが表示されます。  
  
3.  アタッチするデータベースを指定するには、 **[追加]** をクリックします。 
  **[データベース ファイルの検索]** ダイアログ ボックスが表示されます。  
  
4.  データベースが存在するディスク ドライブを選択し、ディレクトリ ツリーを展開してデータベースの .mdf ファイルを選択します。 たとえば、DQS_MAIN データベースの場合は、次のようになります。  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  
  **[データベースの詳細]** (下部) ペインには、アタッチするファイルの名前が表示されます。 ファイルのパス名を確認または変更するには、**参照**ボタン [...] をクリックしてください。  
  
6.  DQS_MAIN データベースをアタッチするには、 **[OK]** をクリックします。  
  
7.  DQS_PROJECTS データベースと DQS_STAGING_DATA データベースで手順 2. ～ 6. を繰り返し、それらをアタッチします。  
  
8.  また、DQS_MAIN データベースを復元した後の次の手順で Transact-SQL ステートメントを実行する必要もあります。これを実行しない場合、Data Quality Client アプリケーションを使用して Data Quality Server に接続しようとするとエラー メッセージが表示され、接続できません。 ただし、DQS_PROJECTS データベースまたは DQS_STAGING_DATA データベースをアタッチし、DQS_MAIN をアタッチしていない場合、手順 9. と 10. を実行する必要はありません。  
  
     Transact-SQL ステートメントを実行するには、オブジェクト エクスプローラーで、サーバーを右クリックし、 **[新しいクエリ]** をクリックします。  
  
9. クエリ エディター ウィンドウで、SQL ステートメントをコピーします。  
  
    ```  
    ALTER DATABASE [DQS_MAIN] SET TRUSTWORTHY ON;  
    EXEC sp_configure 'clr enabled', 1;  
    RECONFIGURE WITH OVERRIDE  
    ALTER DATABASE [DQS_MAIN] SET ENABLE_BROKER  
    ALTER AUTHORIZATION ON DATABASE::[DQS_MAIN] TO [##MS_dqs_db_owner_login##]  
    ALTER AUTHORIZATION ON DATABASE::[DQS_PROJECTS] TO [##MS_dqs_db_owner_login##]  
  
    ```  
  
10. F5 キーを押してステートメントを実行します。 [結果] ペインを確認してステートメントが正常に実行されたことを確認します。 " `Configuration option 'clr enabled' changed from 1 to 1. Run the RECONFIGURE statement to install.`" というメッセージが表示されます。  
  
11. Data Quality Client を使用して Data Quality Server に接続し、正常に接続できるかどうかを確認します。  
  
 また、Transact-SQL ステートメントを使用して DQS データベースをアタッチすることもできます。 Transact-SQL ステートメントを使用したデータベースのインポートに関する詳細については、「 [Using Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) 」の「 [Attach a Database](../relational-databases/databases/attach-a-database.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)  
  
  
