---
title: バックアップの圧縮の構成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bcfc0dea167b972f4e463333ab6851b038a284ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922253"
---
# <a name="configure-backup-compression-sql-server"></a>バックアップの圧縮の構成 (SQL Server)
  インストール時には、既定でバックアップ圧縮が無効になっています。 バックアップ圧縮の既定の動作は、 **backup compression default** サーバー レベル構成オプションで定義されています。 ただし、単一バックアップの作成時や、一連の定期的バックアップのスケジュール設定時には、サーバー レベルの既定値をオーバーライドできます。 サーバー レベルの既定値を変更する方法については、「 [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)」を参照してください。  
  
## <a name="override-the-backup-compression-default"></a>backup compression default のオーバーライド  
 バックアップ、バックアップ ジョブ、またはログ配布構成ごとにバックアップ圧縮動作を変更できます。  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     バックアップの作成時に、サーバーの backup compression default をオーバーライドするには、[BACKUP](/sql/t-sql/statements/backup-transact-sql) ステートメントで WITH NO_COMPRESSION または WITH COMPRESSION を使用します。  
  
     ログ配布構成の場合は、[sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql) を使用して、ログ バックアップのバックアップ圧縮動作を制御できます。  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのバックアップ圧縮の既定オプションを表示または構成する方法については、「[backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)」を参照してください。  
  
     サーバーのバックアップ圧縮に対する既定の動作は、バックアップの作成時、次のダイアログ ボックスのいずれかで **[バックアップを圧縮する]** または **[バックアップを圧縮しない]** を指定してオーバーライドできます。  
  
    -   [[データベースのバックアップ] ([オプション] ページ)](back-up-database-backup-options-page.md)  
  
         データベースをバックアップすると、個別のデータベース、ファイル、またはログのバックアップについて、圧縮を制御できます。  
  
    -   [メンテナンス プラン ウィザードの使用](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         メンテナンス プラン ウィザードを使用すると、スケジュール設定対象の完全データベース バックアップ、差分データベース バックアップ、またはログ バックアップについて、圧縮を制御できます。  
  
    -   Integration Services (SSIS) の [データベースのバックアップ タスク](../../integration-services/control-flow/back-up-database-task.md)  
  
         単一データベースまたは複数データベースをバックアップするパッケージの作成時に、バックアップ圧縮動作を制御できます。  
  
    -   [[トランザクション ログのバックアップの設定]](../databases/log-shipping-transaction-log-backup-settings.md)  
  
         ログのバックアップのバックアップ圧縮動作を制御できます。  
  
  
## <a name="see-also"></a>関連項目  
 [バックアップの圧縮 &#40;SQL Server&#41;](backup-compression-sql-server.md)  
  
  
