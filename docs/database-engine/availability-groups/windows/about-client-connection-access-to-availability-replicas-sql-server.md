---
title: 可用性グループ内のレプリカに対するクライアント接続の種類
description: SQL Server 内の Always On 可用性グループのプライマリまたはセカンダリ レプリカにクライアントから行える接続の種類について説明します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 29027e46-43e4-4b45-b650-c4cdeacdf552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a47e3c79bacbd75ca6761bdb250b05084caf2832
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991732"
---
# <a name="types-of-client-connections-to-replicas-within-an-always-on-availability-group"></a>Always On 可用性グループ内のレプリカに対するクライアント接続の種類
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  AlwaysOn 可用性グループでは、1 つまたは複数の可用性レプリカを構成して、セカンダリ ロールで実行しているとき (つまり、セカンダリ レプリカとして実行しているとき) に読み取り専用接続を許可することができます。 各可用性レプリカをプライマリ ロールで実行しているとき (つまり、プライマリ レプリカとして実行しているとき) に、読み取り専用接続を許可または除外するように構成することもできます。  
  
 特定の可用性グループのプライマリ データベースまたはセカンダリ データベースに対するクライアント アクセスを容易にするために、可用性グループ リスナーを定義する必要があります。 既定では、可用性グループ リスナーは、着信接続をプライマリ レプリカにダイレクトします。 ただし、可用性グループは、読み取り専用ルーティングをサポートするように構成できます。これにより、可用性グループ リスナーが、読み取りを目的としたアプリケーションの接続要求を読み取り可能なセカンダリ レプリカにリダイレクトできます。 詳細については、「 [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)」をご参照ください。  
  
 フェールオーバー中に、セカンダリ レプリカはプライマリ ロールに移行し、元のプライマリ レプリカはセカンダリ レプリカに移行します。 フェールオーバー プロセス中に、プライマリ レプリカとセカンダリ レプリカの両方に対するクライアント接続がすべて終了されます。 フェールオーバー後にクライアントが可用性グループ リスナーに再接続すると、リスナーは、クライアントを新しいプライマリ レプリカに再接続します。ただし、読み取りを目的とした接続要求は除きます。 クライアントとサーバーのインスタンスと、少なくとも 1 つの読み取り可能なセカンダリ レプリカで、新しいプライマリ レプリカをホストする読み取り専用ルーティングが構成された場合、読み取りを目的とした接続要求は、クライアントが必要とするタイプの接続アクセスをサポートするセカンダリ レプリカに再ルーティングされます。 フェールオーバー後にクライアントが快適にサービスを利用できるように、すべての可用性レプリカのセカンダリ ロールとプライマリ ロールに対して接続アクセスを構成することが重要です。  
  
> [!NOTE]  
>  クライアント接続要求を処理する可用性グループ リスナーの詳細については、「 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)」をご参照ください。  
  
##  <a name="ConnectAccessForSecondary"></a> セカンダリ ロールでサポートされる接続アクセスの種類  
 セカンダリ ロールは、次に示すように 3 種類のクライアント接続をサポートします。  
  
 接続不可  
 ユーザーの接続は許可されません。 セカンダリ データベースは読み取りアクセスでは利用できません。 これは、セカンダリ ロールの既定の動作です。  
  
 読み取りを目的とした接続のみ  
 セカンダリ データベースは、 **アプリケーションの目的** 接続プロパティが **ReadOnly** (*読み取り目的の接続*) に設定されている接続に対してのみ利用できます。  
  
 この接続プロパティの詳細については、「 [SQL Server Native Client の HADR サポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)」を参照してください。  
  
 読み取り専用接続の許可  
 セカンダリ データベースは、すべて読み取りアクセス接続に利用できます。 このオプションでは、下位バージョンのクライアントを接続できます。  
  
 詳細については、「 [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)が存在する必要があります。  
  
##  <a name="ConnectAccessForPrimary"></a> プライマリ ロールでサポートされる接続アクセスの種類  
 プライマリ ロールは、次に示すように 2 種類のクライアント接続をサポートします。  
  
 すべての接続を許可する  
 プライマリ データベースに対する読み取り/書き込み接続と読み取り専用接続の両方が許可されます。 これは、プライマリ ロールの既定の動作です。  
  
 読み取り/書き込接続のみを許可する  
 **アプリケーションの目的** 接続プロパティが **ReadWrite** に設定されるか、または値が設定されていない場合、接続が許可されます。 **Application Intent** 接続文字列キーワードが **ReadOnly** に設定されている接続は許可されません。 読み取り/書き込み接続のみを許可することにより、読み取りを目的としたワークロードが誤ってプライマリ レプリカに接続されるのを防ぐことができます。  
  
 この接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 詳細については、「 [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)」をご参照ください。  
  
##  <a name="HowConnectionAccessAffectsConnectivity"></a> 接続アクセス構成がクライアント接続に与える影響  
 レプリカの接続アクセス設定によって、接続試行が失敗するか成功するかが決まります。 次の表に、特定の接続試行が成功するか失敗するかを接続アクセス設定別に示します。  
  
|レプリカのロール|レプリカでサポートされる接続アクセス|接続の目的|接続の試行の結果|  
|------------------|--------------------------------------------|-----------------------|--------------------------------|  
|セカンダリ|All|読み取り目的、読み取り/書き込み、または接続目的の指定なし|成功|  
|セカンダリ|なし (これは、セカンダリの既定の動作です)。|読み取り目的、読み取り/書き込み、または接続目的の指定なし|失敗|  
|セカンダリ|[読み取り目的のみ]|読み取り目的|成功|  
|セカンダリ|[読み取り目的のみ]|読み取り/書き込み、または接続目的の指定なし|失敗|  
|プライマリ|すべて (これはプライマリの既定の動作です)|読み取りのみ、読み取り/書き込み、または接続目的の指定なし|成功|  
|プライマリ|読み取り/書き込み|[読み取り目的のみ]|失敗|  
|プライマリ|読み取り/書き込み|読み取り/書き込み、または接続目的の指定なし|成功|  
  
 クライアント接続要求を処理する可用性グループ リスナーの詳細については、「 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)」をご参照ください。  
  
### <a name="example-connection-access-configuration"></a>接続のアクセス構成の例  
 可用性レプリカの接続アクセスの構成内容がそれぞれ異なっている場合、可用性グループがフェールオーバーした後でクライアント接続のサポートが変わる可能性があります。 たとえば、リモートの非同期コミット セカンダリ レプリカでレポートが実行された可用性グループについて考えてみましょう。 この可用性グループのデータベースのすべての読み取り専用アプリケーションで、 **アプリケーションの目的** 接続プロパティが **ReadOnly**に設定されているため、すべての読み取り専用接続が読み取りを目的とした接続です。  
  
 この例の可用性グループには、メインのコンピューティング センターにある 2 つの同期コミット レプリカと、サテライト サイトにある 2 つの非同期コミット レプリカが含まれています。 プライマリ ロールに対しては、すべてのレプリカに読み取り/書き込みアクセスが構成され、どのような状況でもプライマリ レプリカへの読み取りを目的とした接続ができないようになっています。 同期コミットのセカンダリ ロールでは、既定の接続アクセス構成 ("なし") が使用されるため、セカンダリ ロールではすべてのクライアント接続が禁止されます。  一方、非同期コミット レプリカは、セカンダリ ロールでの読み取り目的の接続を許可するように構成されています。 次の表に、この例の構成をまとめます。  
  
|[レプリカ]|コミット モード|[初期ロール]|セカンダリ ロールの接続アクセス|プライマリ ロールの接続アクセス|  
|-------------|-----------------|------------------|------------------------------------------|----------------------------------------|  
|Replica1|同期|プライマリ|なし|読み取り/書き込み|  
|Replica2|同期|セカンダリ|なし|読み取り/書き込み|  
|Replica3|非同期|セカンダリ|読み取り目的のみ|読み取り/書き込み|  
|Replica4|非同期|セカンダリ|[読み取り目的のみ]|読み取り/書き込み|  
  
 一般的に、この例のシナリオでは、フェールオーバーは同期コミット レプリカ間でのみ実行され、フェールオーバーの直後に、読み取り目的のアプリケーションが非同期コミット セカンダリ レプリカの 1 つに再接続できます。 ただし、メインのコンピューティング センターで障害が発生した場合は両方の同期コミット レプリカが失われます。 サテライト サイトのデータベース管理者が、非同期コミット セカンダリ レプリカへの強制フェールオーバーを手動で実行して対処します。 残りのセカンダリ レプリカのセカンダリ データベースは強制フェールオーバーによって中断されるため、読み取り専用のワークロードで使用できなくなります。 読み取り/書き込み接続が構成されている新しいプライマリ レプリカでは、読み取り目的のワークロードと読み取り/書き込みワークロードが競合しません。 つまり、データベース管理者が残りの非同期コミット セカンダリ レプリカのセカンダリ データベースを再開するまでは、読み取り目的のクライアントはどの可用性レプリカにも接続できません。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [可用性グループの監視 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
-   [可用性レプリカのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [統計](../../../relational-databases/statistics/statistics.md)  
  
  
