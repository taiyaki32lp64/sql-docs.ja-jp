---
title: Azure へのマネージバックアップの SQL Server:相互運用性と共存 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70d941786fd06e48bf071b8448b84c8f4857f8c8
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176065"
---
# <a name="sql-server-managed-backup-to-azure-interoperability-and-coexistence"></a>Azure へのマネージバックアップの SQL Server:相互運用性と共存
  このトピックでは、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] のいくつかの機能との [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]の相互運用性および共存について説明します。 使用できる機能には、次のようなものがあります。AlwaysOn 可用性グループ、データベースミラーリング、バックアップメンテナンスプラン、ログ配布、アドホックバックアップ、データベースのデタッチ、およびデータベースの削除。  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 可用性グループ  
 でサポートされている Azure のみの[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]ソリューションとして構成されている AlwaysOn 可用性グループ。 内部設置型のみまたはハイブリッドの AlwaysOn 可用性グループの構成はサポートされていません。 詳細およびその他の考慮事項については、「[可用性グループの Azure への SQL Server マネージバックアップの設定](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)」を参照してください。  
  
### <a name="database-mirroring"></a>データベース ミラーリング  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]は、プリンシパル データベースでのみサポートされます。 プリンシパルとミラーの両方が [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を使用するように構成されている場合、ミラーリングされたデータベースはスキップされ、バックアップされません。 ただしフェールオーバーが発生した場合、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]は、ミラーが役割の交代を完了してオンラインになった後に、バックアップ プロセスを開始します。 この場合、バックアップは新しいコンテナーに格納されます。 ミラーが [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を使用するように構成されていない場合は、フェールオーバー時にはバックアップがまったく作成されません。 フェールオーバー時にもバックアップが継続されるように、プリンシパルとミラーの両方に対して [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を構成することをお勧めします。  
  
> [!TIP]  
>  ミラー化されたデータベースを [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の既定の設定でインスタンス上に作成する場合、ミラー化されたデータベースに適用されないように [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] インスタンスの既定値を無効にして、プリンシパルとミラーを構成した後でインスタンスの既定値を有効にする方が望ましいことがあります。  
  
### <a name="maintenance-plan"></a>メンテナンスプラン  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]が有効になっている場合、データベースのバックアップ作成にメンテナンス プランを使用することはできません。 メンテナンス プランを使用すると、ログ チェーンが中断されます。また、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]では、復元中にデータベースの保障された復旧をサポートできなくなる可能性があります。 これは、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]がインスタンス レベルで有効になっている場合にも適用されます。  
  
> [!TIP]  
>  コピーのみのバックアップを指定したメンテナンス プランは、同じデータベースまたはインスタンスで [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を構成することによってサポートされます。  
  
### <a name="log-shipping"></a>ログ配布  
 同じデータベースに対してログ配布と [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を同時に構成することはできません。 同時に構成すると、いずれかの機能を使用したデータベースの復元に影響します。  
  
### <a name="ad-hoc-backups-using-transact-sql-and-sql-server-management-studio"></a>Transact-SQL と SQL Server Management Studio を使用したアドホック バックアップ  
 Transact-SQL または SQL Server Management Studio を使用して [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の外部で作成したアドホック バックアップ (1 回限りのバックアップ) は、バックアップの種類と使用される記憶域メディアに応じて、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] プロセスに影響する場合があります。 を使用しているものと[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]は別の azure ストレージアカウント、または azure Blob ストレージサービス以外の他の宛先にログバックアップを実行すると、ログチェーンが中断されます。 を[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]有効にしたデータベースでバックアップを開始するには、 [smart_admin &#40;&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)ストアドプロシージャを使用することをお勧めします。 このストアド プロシージャを使用して、データベースの完全バックアップまたはログ バックアップのどちらかを開始できます。  
  
### <a name="drop-database-and-detach-database"></a>データベースの削除とデータベースのデタッチ  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]が有効になっているデータベースをデタッチまたは削除すると、さらにバックアップすることはできなくなりますが、以前のバックアップは、保有期間が経過するまでストレージ内に保持され、保有期間が経過した時点で削除されます。  
  
### <a name="changes-to-recovery-model"></a>復旧モデルの変更  
  
-   データベースの復旧モデルを**単純**から**完全**または**一括ログ**に変更する場合は、データベース用にを構成[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]することもできます。 これは、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の観点から、新しいデータベースと見なされます。  
  
-   データベースの復旧モデルを**完全**または**一括ログ**から[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] **単純**に変更した場合、それが有効になっていると、バックアップ操作はスケジュールされなくなります。 保有期間設定はアクティブのままであるため、保有期間が経過するまでバックアップ ファイルはストレージ アカウントに残ります。 バックアップを保持する必要がある場合は、別のストレージ アカウントまたは内部設置型の場所にファイルをダウンロードすることをお勧めします。 構成設定は保持され、復旧モデルが**完全**または**一括ログ**に再び設定された場合に再利用できます。  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>他のバックアップ ツールまたはカスタム スクリプトを使用したログ バックアップ  
 2 つのバックアップが同じデータベースでログ バックアップを実行するように構成されていると、バックアップ ログ チェーンが中断されます。 チェーンの中断が検出されると、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]は完全バックアップをスケジュールしてバックアップ チェーンの中断を修復しようとしますが、これは中断が定期的に発生し、競合する 2 つのツールによってログ バックアップが実行されるという状態が続くことを意味します。 また、一方のツールがバックアップの完全なセットを順序どおりに保持することは期待できないため、データベースの回復性に影響する可能性があります。 これは、ログ バックアップを実行する 2 つの機能またはツールに当てはまりますが、次に示す具体的な例を強調する際に役立ちます。 また、これは、このトピックの以前のセクションで説明したメンテナンス プランまたはログ配布の構成に関する問題の根拠でもあります。  
  
 **Data Protection Manager (DPM) ベースのバックアップ:** Microsoft Data Protection Manager では、完全バックアップと増分バックアップを実行できます。 増分バックアップは、トランザクション ログ バックアップの作成後にログの切り捨てを実行するログ バックアップです。 そのため、同じデータベースで DPM と [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の両方を構成することはできません。  
  
 **サードパーティ製のツールまたはスクリプト:** ログの切り捨てが発生するログバックアップを実行するサードパーティのツールまた[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]はスクリプトは、と互換性がなく、サポートもされていません。  
  
 データベースインスタンスに対してを[ &#40;&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) 有効にし、アドホックバックアップを作成する場合は、前のセクションで説明したように、smart_adminストアドプロシージャを使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]することができます。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]以外に、スケジュールや定期的なバックアップも必要な場合は、[バックアップのみコピーする] を使用できます。  詳細については、「[コピーのみのバックアップ &#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md)」を参照してください。  
  
  
