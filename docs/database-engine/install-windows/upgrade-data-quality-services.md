---
title: Data Quality Services のアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: fab545b34f257563466ec2f64911cdfaceca9456
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934856"
---
# <a name="upgrade-data-quality-services"></a>Data Quality Services のアップグレード

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Services (DQS) の既存のインストールをアップグレードする方法について説明します。 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality サーバーをアップグレードする作業の一環として、DQS データベース スキーマもアップグレードする必要があります。  
  
> [!IMPORTANT]
>  -   スキーマのアップグレード中に誤ってデータが削除されることを防ぐため、DQS をアップグレードする前に DQS データベースをバックアップしておく必要があります。 DQS データベースのバックアップの詳細については、「 [DQS データベースのバックアップと復元](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)」を参照してください。  
> -   データ品質タスクを実行するために、現在または以前のバージョンの Data Quality クライアントか、Integration Services 内の [DQS クレンジング変換](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)を使用して、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality サーバーに接続できます。  
> -   Data Quality Services およびマスター データ サービスをアップグレードした後は、以前のバージョンの Excel 用マスター データ サービス アドインは機能しなくなります。 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] ここ [から、](https://go.microsoft.com/fwlink/?LinkID=506665)バージョンの Excel 用マスター データ サービス アドインをダウンロードできます。  
  
##  <a name="Prerequisites"></a> 前提条件  
  
-   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの Administrators グループのメンバーとしてログオンする必要があります。  
  
-   Windows ユーザー アカウントが、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] がインストールされている SQL Server インスタンスの sysadmin 固定サーバー ロールのメンバーであることが必要です。  
  
##  <a name="Upgrade"></a> DQS のアップグレード  
 DQS をアップグレードするには:  
  
1.  スキーマのアップグレードを開始する前に、DQS データベースをバックアップします。 DQS データベースのバックアップの詳細については、「 [DQS データベースのバックアップと復元](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)」を参照してください。  
  
2.  DQS のインストール先である SQL Server インスタンスをアップグレードします。  
  
    1.  [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] セットアップ ウィザードを実行します。  
  
    2.  左ペインで、 **[インストール]** をクリックします。  
  
    3.  右ペインで、**アップグレード** ボタンをクリックし、以前のバージョンの SQL Server からアップグレードします。  
  
    4.  セットアップ ウィザードを完了します。  
  
        > [!NOTE]  
        >  この結果、SQL Server インスタンスが [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] にアップグレードされ、また、このコンピューターに以前に Data Quality クライアントがインストールされていた場合は、最新の Data Quality クライアントがインストールされます。 他のコンピューターに Data Quality クライアントをインストールしていた場合は、それらのコンピューターに対して手順 2. の下位の手順を実行して、現在のバージョンの Data Quality クライアントをインストールする必要があります。 セットアップ ウィザードは、Data Quality クライアントの既存のバージョンと並行して、Data Quality クライアントの現在のバージョンをインストールします。 DQS データベース スキーマをアップグレードした後、現在または以前のバージョンの Data Quality クライアントを使用して、Data Quality サーバーの [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] バージョンに接続できます。  
  
3.  DQS データベース スキーマをアップグレードします。  
  
    1.  管理者としてコマンド プロンプトを起動します。  
  
    2.  コマンド プロンプトで、DQSInstaller.exe が格納されている場所にディレクトリを変更します。 SQL Server の既定のインスタンスの場合は、DQSInstaller.exe ファイルは C:\Program Files\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn に格納されます。  

      >[!NOTE]
      >フォルダーのパスで、[nn] は [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のバージョン番号に置き換えます。
      >- SQL Server 2016 の場合:13
      >- SQL Server 2017 の場合:14

        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  コマンド プロンプトに次のコマンドを入力し、Enter キーを押します。  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  処理を続ける前に DQS データベースをバックアップするように求められます。 既に DQS データベースをバックアップした場合は「 **Y** 」または「 **Yes**」と入力して Enter キーを押し、アップグレードを続行します。  
  
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
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|[error]|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMAIN\UserName>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMAIN\UserName>|2||  
  
## <a name="see-also"></a>参照  
 [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Data Quality Server オブジェクトの削除](../../sql-server/install/remove-data-quality-server-objects.md)   
 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  
