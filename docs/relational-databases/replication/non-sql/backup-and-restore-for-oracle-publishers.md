---
title: Oracle パブリッシャーのバックアップと復元 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], Oracle publishing
- backups [SQL Server replication], Oracle publishing
- Oracle publishing [SQL Server replication], backup and restore
- restoring [SQL Server replication], Oracle publishing
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ea6539e0d004f573281d54f7bb4a4c055c7b3e73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901113"
---
# <a name="backup-and-restore-for-oracle-publishers"></a>Oracle パブリッシャーのバックアップと復元
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  バックアップと復元を実行する場合は、次のガイドラインに従ってください。  
  
-   パブリッシャーのバックアップ中は、ログ リーダー エージェントを実行したり、パブリッシュされたテーブルでその他のデータベースの処理を実行しないようにします。  
  
-   パブリッシャーとディストリビューターは同時にバックアップします。  
  
-   パブリッシャーまたはディストリビューターを復元する必要がある場合は、すべてのサブスクリプションを再初期化します。  
  
-   バックアップからサブスクライバーを復元するには (サブスクリプションの再初期化は不要)、前回のサブスクリプション データベースのバックアップ完了後にディストリビューション データベースに配信されたトランザクションも使用できる必要があります。 トランザクションが使用できる時間の長さは、ディストリビューションの保有期間の設定によって異なります。 これらの設定については、「[サブスクリプションの有効期限と非アクティブ化](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)」を参照してください。  
  
-   データベースを復元した結果、パブリッシャーまたはディストリビューターが同期しなくなった場合は、レプリケーション エージェントによってエラー メッセージが記録されます。 この時点で、関連するパブリケーションとサブスクリプションをすべて削除して再作成する必要があります。  
  
    1.  パブリケーションおよびサブスクリプションの定義のスクリプトを作成します。 詳細については、「[レプリケーションのスクリプト作成](../../../relational-databases/replication/scripting-replication.md)」を参照してください。  
  
         パブリッシャーとディストリビューターの状態のバージョン間でパブリケーションの定義が変更された場合は、スクリプトを変更する必要があります。  
  
    2.  パブリケーションとサブスクリプションを削除します。  
  
    3.  手順 1. で作成したスクリプトを実行します。  
  
     パブリッシャーを削除および再構成する必要がある場合は、 **MSSQLSERVERDISTRIBUTOR** パブリック シノニムと、 **CASCADE** オプションで構成した Oracle レプリケーション ユーザーを削除して、Oracle パブリッシャーからすべてのレプリケーション オブジェクトを削除します。  
  
## <a name="see-also"></a>参照  
 [レプリケートされたデータベースのバックアップと復元](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Oracle パブリッシャーの構成](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle パブリッシングの概要](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
