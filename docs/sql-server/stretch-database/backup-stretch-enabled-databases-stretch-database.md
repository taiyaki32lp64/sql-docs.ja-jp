---
title: Stretch 対応データベースのバックアップ
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: 18f0dff0-d8ce-4bee-a935-76ed6dfb3208
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 897f748c5aeab43c7e3ef98f6dbfff84b9da69d7
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843833"
---
# <a name="backup-stretch-enabled-databases-stretch-database"></a>Stretch 対応データベースのバックアップ (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 データベースのバックアップは、さまざまな種類の障害、エラー、災害から回復するのに役立ちます。  
  
 -   Stretch 対応の SQL Server データベースをバックアップする必要があります。  
      
 -   Microsoft Azure では、Stretch Database が SQL Server から Azure に移行したリモート データを自動的にバックアップします。  

> [!TIP]
> バックアップは、完全な高可用性とビジネス継続性ソリューションの一部にすぎません。 高可用性についての詳細は、「 [高可用性ソリューション](../../database-engine/sql-server-business-continuity-dr.md)」を参照してください。
   
## <a name="back-up-your-sql-server-data"></a>SQL Server データのバックアップ  
  
Stretch 対応の SQL Server データベースをバックアップするには、現在使用している SQL Server のバックアップ方法を引き続き使用できます。 詳細については、「 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)」を参照してください。
  
 Stretch 対応の SQL Server データベースのバックアップには、ローカル データと、バックアップを実行した時点での移行対象データのみが含まれています (対象データとは、まだ移動されていないが、テーブルの移行設定に基づいて Azure に移行される予定のデータです)。これは**浅い**バックアップと呼ばれ、既に Azure に移行されたデータは含まれません。  
  
## <a name="back-up-your-remote-azure-data"></a>リモートの Azure データのバックアップ   
  
Microsoft Azure では、Stretch Database が SQL Server から Azure に移行したリモート データを自動的にバックアップします。    
### <a name="azure-reduces-the-risk-of-data-loss-with-automatic-backup"></a>Azure は自動バックアップによりデータ消失のリスクを軽減  
Azure の SQL Server Stretch Database サービスは、少なくとも 8 時間ごとの自動ストレージのスナップショットにより、リモート データベースを保護します。 復元ポイントを幅広く提供するため、各スナップショットを 7 日間保持します。  
  
### <a name="azure-reduces-the-risk-of-data-loss-with-geo-redundancy"></a>Azure は地理冗長によりデータ損失のリスクを軽減  
Azure のデータベース バックアップは、地理冗長の Azure Storage (RA-GRS) に格納されるため、既定で地理冗長になっています。 地理冗長ストレージは、プライマリ リージョンから数百マイル離れたセカンダリ リージョンにデータをレプリケートします。 プライマリ リージョンとセカンダリ リージョンの両方で、データは別々のフォールト ドメインとアップグレード ドメイン間でそれぞれ 3 回レプリケートされます。 これにより、いずれかの Azure リージョンが利用不能状態になるような局所的な停電や災害が発生した場合でも、データの持続性が保証されます。

### <a name="stretchRPO"></a>Stretch Database は、移行済みの行を一時的に保持することで、Azure データのデータ損失リスクを軽減
Stretch Database は SQL Server から Azure に対象となる行を移行した後、これらの行をステージング テーブルに 8 時間以上保持します。 Azure データベースのバックアップを復元する場合、Stretch Database はステージング テーブルに保存されている行を使用して、SQL Server と Azure データベースを調整します。

Azure データのバックアップを復元した後に、ストアド プロシージャ [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) を実行して、Stretch 対応の SQL Server データベースをリモートの Azure データベースに再接続する必要があります。 **sys.sp_rda_reauthorize_db**を実行すると、Stretch Database は SQL Server と Azure データベースを自動的に調整します。

Stretch Database がステージング テーブルに移行したデータを一時的に保持する時間を増やすには、ストアド プロシージャ [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) を実行し、8 より大きい値を時間に指定します。 保持するデータの量を決定するには、次の要因を検討します。
-   Azure の自動バックアップの頻度 (少なくとも 8 時間ごと)。
-   問題が発生してから、それを認識してバックアップを復元することを決定するまでに必要な時間。
-   Azure の復元操作の期間。

> [!NOTE]
> Stretch Database がステージング テーブルに一時的に保持するデータの量を増やすと、SQL Server 上で必要な領域の量も増加します。

Stretch Database がステージング テーブルに一時的に保持している時間を確認するには、ストアド プロシージャ [sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)を実行します。

## <a name="see-also"></a>参照  
[Stretch 対応データベースの復元](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
 [Stretch Database の管理とトラブルシューティング](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
   
  
  
