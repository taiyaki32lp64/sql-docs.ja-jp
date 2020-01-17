---
title: データベース要件 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: fe731839-c5c4-4884-bb6a-644eca28bb30
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 75bd453d4540a675809973f711bd778ab8639d10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479312"
---
# <a name="database-requirements-master-data-services"></a>データベース要件 (マスター データ サービス)
  マスター データはすべて [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースに格納されます。 このデータベースをホストするコンピューターでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンスを実行する必要があります。  
  
 ローカル コンピューターまたはリモート コンピューターで [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] データベースを作成および構成するには、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] を使用します。 環境間でデータベースを移動する場合、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web サービスと [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] を新しい場所のデータベースに関連付けることにより、新しい環境で情報を維持できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] のコンポーネントをインストールするコンピューターはすべてライセンス供与を受けている必要があります。 詳細については、使用許諾契約書 (EULA) を参照してください。  
  
## <a name="requirements"></a>必要条件  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースを作成する前に、次の要件が満たされていることを確認してください。  
  
### <a name="sql-server-edition"></a>SQL Server のエディション  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースは、次のエディションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でホストできます。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence (64 ビット) x64  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (64 ビット) x64  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer (64 ビット) x64  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Business Intelligence (64 ビット) x64  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Enterprise (64 ビット) x64 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Enterprise からのアップグレードの場合のみ)  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Developer (64 ビット) x64  
  
-   Microsoft SQL Server 2008 R2 Enterprise (64 ビット) x64  
  
-   Microsoft SQL Server 2008 R2 Developer (64 ビット) x64  
  
 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
### <a name="operating-system"></a>オペレーティング システム  
 サポートされている Windows オペレーティング システムと他の要件について[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]を参照してください[Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)します。  
  
### <a name="accounts-and-permissions"></a>アカウントと権限  
  
|型|説明|  
|----------|-----------------|  
|ユーザー アカウント|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]では、Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントを使用して [!INCLUDE[ssDE](../../includes/ssde-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続し、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースをホストできます。 このユーザー アカウントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスの **sysadmin** サーバー ロールに属している必要があります。 **sysadmin** ロールの詳細については、「 [サーバー レベルのロール](../../relational-databases/security/authentication-access/server-level-roles.md)」を参照してください。|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 管理者アカウント|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースを作成する場合、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] システム管理者となるドメイン ユーザー アカウントを指定する必要があります。 このユーザーは、このデータベースに関連付けられているすべての[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションについて、すべての機能領域のすべてのモデルおよびすべてのデータを更新できます。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](../administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。|  
  
### <a name="database-backup"></a>データベース バックアップ  
 システムの使用率が低い時間帯にデータベース全体を毎日バックアップし、使用している環境のニーズに応じて、毎日数回、トランザクション ログをバックアップすることをお勧めします。 データベース バックアップの詳細については、「[バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのインストール](install-master-data-services.md)   
 [マスター データ サービス データベースの作成](create-a-master-data-services-database.md)   
 [マスター データ サービス データベース](../master-data-services-database.md)   
 [[マスター データ サービス データベースへの接続] ダイアログ ボックス](../connect-to-a-master-data-services-database-dialog-box.md)   
 [データベースの作成ウィザード &#40;マスター データ サービス構成マネージャー&#41;](../create-database-wizard-master-data-services-configuration-manager.md)  
  
  
