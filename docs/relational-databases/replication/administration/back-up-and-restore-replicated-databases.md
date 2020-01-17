---
title: レプリケートされたデータベースのバックアップと復元 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication]
- administering replication, restoring
- backing up replicated databases
- backups [SQL Server replication], about backups
- restoring replicated databases [SQL Server replication]
- recovery [SQL Server replication], about recovery
- restoring databases [SQL Server], replicated databases
- backing up databases [SQL Server], replicated databases
- restoring [SQL Server replication], about restoring
- recovery [SQL Server replication]
- replication [SQL Server], administering
- distribution databases [SQL Server replication], backing up
- restoring [SQL Server replication]
- administering replication, backing up
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 101c272e51a4a4fdab4456f87aac297c2ac56476
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768821"
---
# <a name="back-up-and-restore-replicated-databases"></a>レプリケートされたデータベースのバックアップと復元
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  レプリケートされたデータベースでは、データのバックアップと復元に対する特別な注意が必要です。 このトピックでは、それぞれの種類のレプリケーションのバックアップと復元の方法に関する概要、および詳細情報へのリンクを提供します。  
  
 レプリケーションでは、レプリケートされたデータベースをバックアップ作成元のサーバーおよびデータベースに復元する操作がサポートされます。 レプリケートされたデータベースのバックアップを別のサーバーまたはデータベースに復元する場合は、レプリケーションの設定は保存できません。 この場合、バックアップが復元された後で、すべてのパブリケーションとサブスクリプションを再作成する必要があります。  
  
> [!NOTE]  
>  ログ配布が使用されている場合は、レプリケートされたデータベースをスタンバイ サーバーに復元できます。 詳細については、「[ログ配布とレプリケーション &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)」 を参照してください。  
  
 レプリケートされたデータベースと関連付けられているシステム データベースは、定期的にバックアップする必要があります。 次のデータベースをバックアップします。  
  
-   パブリッシャーにあるパブリケーション データベース  
  
-   ディストリビューターにあるディストリビューション データベース  
  
-   各サブスクライバーにあるサブスクリプション データベース  
  
-   パブリッシャー、ディストリビューター、およびすべてのサブスクライバーにある **master** および **msdb** システム データベース。 これらのデータベースは、相互に関連するレプリケーション データベースとして、同時にバックアップする必要があります。 たとえば、パブリッシャーでパブリケーション データベースをバックアップするときに、 **master** および **msdb** データベースも同時にバックアップします。 パブリケーション データベースを復元するときは、 **master** および **msdb** データベースのレプリケーションの構成と設定が、パブリケーション データベースと一致していることを確認します。  
  
 定期的なログ バックアップを実行する場合は、レプリケーション関連の変更をログ バックアップでキャプチャする必要があります。 ログ バックアップを実行しない場合は、レプリケーションに関連する設定を変更するたびに、バックアップを実行する必要があります。 詳細については、「 [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md)」を参照してください。  
  
## <a name="backup-and-restore-strategies"></a>バックアップと復元の方法  
 レプリケーション トポロジの各ノードのバックアップと復元の方法は、使用されるレプリケーションの種類によって異なります。 それぞれの種類のレプリケーションのバックアップと復元の方法の詳細については、以下のトピックを参照してください。  
  
-   [スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [マージ レプリケーションのバックアップと復元の方式](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 どの方法で復元を行う場合でも、必ずレプリケーションの設定の現在のスクリプトを安全な場所に保管しておいてください。 サーバーで障害が発生した場合やテスト環境をセットアップする必要がある場合は、サーバー名の参照を変更してスクリプトを修正し、そのスクリプトをレプリケーションの設定の再作成に利用することができます。 現在のレプリケーションの設定用のスクリプトの他に、レプリケーションを有効にするスクリプトと無効にするスクリプトを作成する必要があります。 レプリケーション オブジェクトのスクリプトの作成方法の詳細については、「 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server データベースのバックアップと復元](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
