---
title: マネージド バックアップの設定を移行する
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: ae937ebb-24ff-4a33-be3c-8f85328dfc75
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 79cbc0a2fcd020cc1e4b59de6d4fc0a2c3320059
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258674"
---
# <a name="migrate-managed-backup-settings"></a>マネージド バックアップの設定を移行する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] にアップグレードする際の [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]の移行に関する考慮事項について説明します。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] のプロシージャと基になる動作は [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]で変更されています。 次のセクションで、機能の変更点とその関連事項について説明します。  
  
## <a name="overview"></a>概要  
 次の表では、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] に関する [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] と [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]の主要な機能の違いの一部について説明します。  
  
|領域|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  
|----------|---------------------------|---------------------------|  
|**名前空間:**|smart_admin|managed_backup|  
|**システム ストアド プロシージャ:**|sp_set_db_backup<br /><br /> sp_set_instance_backup|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)<br /><br /> [sp_backup_config_advanced](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)<br /><br /> [sp_backup_config_schedule](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|  
|**セキュリティ:**|Microsoft Azure ストレージ アカウントとアクセス キーを使用した SQL 資格情報。|Microsoft Azure Shared Access Signature (SAS) トークンを使用した SQL 資格情報。|  
|**基になるストレージ:**|ページ BLOB を使用した Microsoft Azure Storage。|ブロック BLOB を使用した Microsoft Azure Storage。|  
  
## <a name="benefits"></a>メリット  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]の新機能の使用には、いくつかの利点があります。  
  
-   ブロック BLOB により、格納のコストを抑えることができます。  
  
-   ストライピングを使用すると、はるかに大きなバックアップを格納できます (12 TB。一方のページ BLOB では 1 TB)。  
  
-   ストライピングにより、大規模データベースの復元時間も向上します。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] での [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]のその他の機能強化については、「 [Microsoft Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)」をご覧ください。  
  
## <a name="considerations"></a>考慮事項  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]からアップグレードした後、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] に関する次の考慮事項に注意してください。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] で以前に [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 用に構成したすべてのデータベースは、 **で** smart_admin [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]のシステム プロシージャと基になる動作を引き続き使用します。  
  
-   **smart_admin** のプロシージャは、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]の新しい構成ではサポートされません。 新しい **managed_backup** のプロシージャと機能を使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [Microsoft Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
