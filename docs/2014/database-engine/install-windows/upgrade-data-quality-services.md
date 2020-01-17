---
title: Data Quality Services のアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c76fda112acae7b8a9314d217f5c32d197e87f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775632"
---
# <a name="upgrade-data-quality-services"></a>Data Quality Services のアップグレード
  このトピックでは、Data Quality Services (DQS) の既存のインストールを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2 にアップグレードする方法を紹介します。 DQS 内の Data Quality サーバーを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする作業の一環として、DQS データベース スキーマもアップグレードする必要があります。  
  
> [!IMPORTANT]
>  -   スキーマのアップグレード中に誤ってデータが削除されることを防ぐため、DQS をアップグレードする前に DQS データベースをバックアップしておく必要があります。 DQS データベースのバックアップの詳細については、「 [DQS データベースのバックアップと復元](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)」を参照してください。  
> -   データ品質タスクを実行するために、現在または以前のバージョンの Data Quality クライアントか、Integration Services 内の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] DQS クレンジング変換 [を使用して、Data Quality サーバーの](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) バージョンに接続できます。  
> -   Data Quality Services およびマスター データ サービスを [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] CTP2 にアップグレードした後も、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 バージョンの Excel 用マスター データ サービス アドインを使用し続けることができます。 ただし、SQL Server 2014 CTP2 にアップグレードした後、以前のバージョンの Excel 用マスター データ サービス アドインは機能しません。 ダウンロードすることができます、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 バージョンのマスター データ サービス アドインを使用して Excel の[ここ](https://go.microsoft.com/fwlink/?LinkId=328664)します。  
  
##  <a name="Prerequisites"></a> 前提条件  
  
-   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの Administrators グループのメンバーとしてログオンする必要があります。  
  
-   Windows ユーザー アカウントが、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] がインストールされている SQL Server インスタンスの sysadmin 固定サーバー ロールのメンバーであることが必要です。  
  
##  <a name="Upgrade"></a> DQS のアップグレード  
 DQS をアップグレードするには:  
  
1.  スキーマのアップグレードを開始する前に、DQS データベースをバックアップします。 DQS データベースのバックアップの詳細については、「 [DQS データベースのバックアップと復元](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)」を参照してください。  
  
2.  DQS のインストール先である SQL Server インスタンスを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードします。  
  
    1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ ウィザードを実行します。  
  
    2.  左ペインで、 **[インストール]** をクリックします。  
  
    3.  右側のウィンドウで次のようにクリックします。 **SQL Server 2005、SQL Server 2008、SQL Server 2008 R2 または SQL Server 2012 からアップグレード**します。  
  
    4.  セットアップ ウィザードを完了します。  
  
        > [!NOTE]  
        >  この結果、SQL Server インスタンスが [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードされ、また、このコンピューターに以前に Data Quality クライアントがインストールされていた場合は、最新の Data Quality クライアントがインストールされます。 他のコンピューターに Data Quality クライアントをインストールしていた場合は、それらのコンピューターに対して手順 2. の下位の手順を実行して、現在のバージョンの Data Quality クライアントをインストールする必要があります。 セットアップ ウィザードは、Data Quality クライアントの既存のバージョンと並行して、Data Quality クライアントの現在のバージョンをインストールします。 DQS データベース スキーマをアップグレードした後、現在または以前のバージョンの Data Quality クライアントを使用して、Data Quality サーバーの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンに接続できます。  
  
3.  DQS データベース スキーマをアップグレードします。  
  
    1.  管理者としてコマンド プロンプトを起動します。  
  
    2.  コマンド プロンプトで、DQSInstaller.exe が格納されている場所にディレクトリを変更します。 SQL Server の既定のインスタンスの場合は、DQSInstaller.exe ファイルは C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn に格納されます。  
  
        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  コマンド プロンプトに次のコマンドを入力し、Enter キーを押します。  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  処理を続ける前に DQS データベースをバックアップするように求められます。 既に DQS データベースをバックアップしてあるを場合は、入力`Y`または`Yes`、アップグレードを続行するには ENTER キーを押します。  
  
    5.  DQS データベース スキーマのアップグレードが正常に完了すると、完了のメッセージが表示されます。  
  
##  <a name="Verify"></a> DQS データベース スキーマのアップグレードの確認  
 DQS データベース スキーマが正常にアップグレードされたことを確認するために、各データベース内の A_DB_VERSION テーブルに対してクエリを実行し、DQS_MAIN データベースと DQS_PROJECTS データベースの現在のバージョンを確認することができます。 そのためには次を行います。  
  
1.  SQL Server Management Studio を起動し、アップグレード後の DQS データベース スキーマを含む SQL Server インスタンスに接続します。  
  
2.  次のクエリを実行します。  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  出力で、アップグレードの日付と共に、各アップグレードのエントリが表示されます。 最新の日付になっていて、値が最も大きい VERSION_ID と ASSEMBLY_VERSION が、現在のバージョンです。 STATUS 列に値 2 が表示されている場合は、成功を示しています。 エラーが発生した場合は、ERROR 列にそのエラーが表示されます。 サンプル出力を示します。  
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|ERROR|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMAIN\UserName>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMAIN\UserName>|2||  
  
## <a name="see-also"></a>関連項目  
 [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Data Quality Server オブジェクトの削除](../../sql-server/install/remove-data-quality-server-objects.md)   
 [SQL Server 2014 へのアップグレード](upgrade-sql-server.md)  
  
  
