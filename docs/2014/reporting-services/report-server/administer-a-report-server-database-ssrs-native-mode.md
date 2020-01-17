---
title: レポート サーバー データベースを管理する (SSRS ネイティブ モード) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- renaming databases
- report server database
- databases [Reporting Services], administering
- reportservertempdb
- reportserver database
ms.assetid: 97b2e1b5-3869-4766-97b9-9bf206b52262
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d155437880f1fb93779a2352bd507ea83de16256
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104279"
---
# <a name="administer-a-report-server-database-ssrs-native-mode"></a>レポート サーバー データベースを管理する (SSRS ネイティブ モード)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の環境では、2 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベースが内部記憶域として使用されます。 既定では、データベース名がそれぞれ ReportServer と ReportServerTempdb になります。 ReportServerTempdb は、レポート サーバーのプライマリ データベースと共に作成され、一時データ、セッション情報、およびキャッシュされたレポートを格納する目的に使用されます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]でのデータベースの管理には、レポート サーバー データベースのバックアップと復元、および機密データの暗号化と暗号化解除に使用する暗号化キーの管理が含まれます。  
  
 レポート サーバー データベースを管理するために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではさまざまなツールを用意しています。  
  
-   レポート サーバー データベースのバックアップや復元、移動、または復旧を行うには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンド、またはデータベース コマンド プロンプト ユーティリティを使用します。 手順については、SQL Server オンライン ブックの「[別のコンピューターへのレポート サーバー データベースの移動 &#40;SSRS ネイティブ モード&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」を参照してください。  
  
-   既存のデータベース コンテンツを他のレポート サーバー データベースにコピーする場合、レポート サーバー データベースのコピーをアタッチして、別のレポート サーバー インスタンスで使用します。 また、SOAP 呼び出しを使用して新しいデータベースにレポート サーバー コンテンツを再作成するスクリプトを作成して、実行することもできます。 スクリプトを実行するには、 **rs** ユーティリティを使用します。  
  
-   レポート サーバーとレポート サーバー データベースの接続の管理、および特定のレポート サーバー インスタンスで使用しているデータベースの検索を行うには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]構成ツールの [データベースのセットアップ] ページを使用します。 レポート サーバー データベースへのレポート サーバーの接続の詳細については、「 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。  
  
## <a name="sql-server-login-and-database-permissions"></a>SQL Server のログインとデータベースの権限  
 レポート サーバー データベースは、レポート サーバーによって内部的に使用されます。 データベースへの接続は、レポート サーバー サービスによって行われます。 レポート サーバー データベースに対するレポート サーバー接続を構成するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用します。  
  
 データベースに対するレポート サーバー接続の資格情報には、サービス アカウント、Windows のローカルまたはドメイン ユーザー アカウント、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ユーザーを使用できます。 接続に使用するアカウントには、既存のアカウントを選択する必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ではアカウントは作成されません。  
  
 レポート サーバー データベースに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインは、指定したアカウントに対して自動的に作成されます。  
  
 データベースに対する権限も自動的に構成されます。 Reporting Services 構成ツールでは、アカウントまたはデータベース ユーザーが、レポート サーバー データベースの `Public` ロールおよび `RSExecRole` ロールに割り当てられます。 `RSExecRole` には、データベース テーブルにアクセスしたり、ストアド プロシージャを実行したりするための権限が割り当てられています。 `RSExecRole`レポート サーバー データベースを作成するときに master および msdb に作成します。 `RSExecRole` は、レポート サーバー データベースの `db_owner` ロールのメンバーであるため、自動アップグレード プロセスなどで、レポート サーバーが自己のスキーマを更新することもできます。  
  
## <a name="naming-conventions-for-the-report-server-databases"></a>レポート サーバー データベースの名前付け規則  
 プライマリ データベースを作成する際、データベースの名前は、「 [データベース識別子](../../relational-databases/databases/database-identifiers.md)」に指定されている規則に従う必要があります。 一時データベースには、レポート サーバーのプライマリ データベース名に、Tempdb というサフィックスを追加した名前を使用する必要があります。 一時データベースに別の名前を選択することはできません。  
  
 レポート サーバーのデータベースは内部コンポーネントと見なされているため、レポート サーバー データベースの名前変更はサポートされません。 レポート サーバーのデータベース名を変更するとエラーが発生します。 具体的には、プライマリ データベースの名前を変更すると、データベース名が同期されていないという内容のエラー メッセージが表示されます。ReportServerTempdb データベースの名前を変更すると、レポートの実行時に次の内部エラーが発生します。  
  
 "レポート サーバーで内部エラーが発生しました。 詳細については、エラー ログを参照してください。 (rsInternalError)  
  
 オブジェクト名 'ReportServerTempDB.dbo.PersistedStream' が無効です。"  
  
 ReportServerTempdb の名前は内部的に保存され、ストアド プロシージャが内部的な操作を実行するときに使用されるため、このエラーが発生します。 一時データベースの名前を変更すると、ストアド プロシージャが正しく機能しなくなります。  
  
## <a name="enabling-snapshot-isolation-on-the-report-server-database"></a>レポート サーバー データベースのスナップショット分離の有効化  
 レポート サーバー データベースのスナップショット分離を有効にすることはできません。 スナップショット分離が有効な場合は、次のエラーが発生するは。"選択したレポートが表示できていません。 レポートが表示の準備中か、またはレポート スナップショットが利用できません" というエラーが発生します。  
  
 スナップショット分離を意図的に有効にしなくても、他のアプリケーションによって属性が設定されたり、 **model** データベースのスナップショット分離が有効になっていたために、新しいデータベースがすべてその設定を引き継いでしまうことも考えられます。  
  
 レポート サーバー データベースのスナップショット分離を無効にするには、Management Studio を起動して、新しいクエリ ウィンドウを開き、次のスクリプトを貼り付けて実行します。  
  
```  
ALTER DATABASE ReportServer  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServerTempdb  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServer  
SET READ_COMMITTED_SNAPSHOT OFF  
ALTER DATABASE ReportServerTempDb  
SET READ_COMMITTED_SNAPSHOT OFF  
```  
  
## <a name="about-database-versions"></a>データベースのバージョンについて  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、データベースのバージョンについて明確な情報を入手できません。 ただし、データベースのバージョンは常に製品のバージョンと同期しているので、製品バージョンの情報からデータベースのバージョンが変更された時期がわかります。 製品バージョンの情報[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ファイル バージョン情報のすべての SOAP 呼び出しのヘッダー内のログ ファイルに表示されると、レポート サーバーの URL に接続するときに示されます (たとえば、ブラウザーを開く http://localhost/reportserver) します。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [ネイティブ モード レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Reporting Services のバックアップおよび復元操作](../install-windows/backup-and-restore-operations-for-reporting-services.md)   
 [レポート サーバー データベース &#40;SSRS ネイティブ モード&#41;](report-server-database-ssrs-native-mode.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](reporting-services-report-server-native-mode.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
