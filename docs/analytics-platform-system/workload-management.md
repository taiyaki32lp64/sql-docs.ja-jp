---
title: ワークロード管理
description: 分析プラットフォームシステムのワークロード管理。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399446"
---
# <a name="workload-management-in-analytics-platform-system"></a>Analytics Platform System のワークロード管理

SQL Server PDW のワークロード管理機能を使用すると、ユーザーと管理者は、事前設定されたメモリの構成および同時実行に対して要求を割り当てることができます。 ワークロード管理を使用すると、要求が永久に失われることなく、要求に適切なリソースを割り当てることができるため、一貫性のある、または混在するワークロードのパフォーマンスを向上させることができます。  
  
たとえば、SQL Server PDW のワークロード管理手法を使用すると、次のことができます。  
  
-   負荷ジョブに大量のリソースを割り当てます。  
  
-   列ストアインデックスを構築するためのリソースをさらに指定します。  
  
-   実行速度の遅いハッシュ結合のトラブルシューティングを行って、より多くのメモリが必要かどうかを確認してから、より多くのメモリを確保します。  
  
## <a name="Basics"></a>ワークロード管理の基礎  
  
### <a name="key-terms"></a>主な用語  
ワークロード管理  
*ワークロード管理*は、同時要求に最適なパフォーマンスを実現するために、システムリソースの使用率を把握し、調整する機能です。  
  
リソース クラス  
SQL Server PDW の*リソースクラス*は、メモリと同時実行に対して事前に割り当てられた制限を持つ組み込みのサーバーロールです。 SQL Server PDW は、要求を送信するログインのリソースクラスサーバーロールメンバーシップに従って、リソースを要求に割り当てます。  
  
コンピューティングノードでは、リソースクラスの実装で SQL Server の Resource Governor 機能が使用されます。 Resource Governor の詳細については、MSDN の「 [Resource Governor](../relational-databases/resource-governor/resource-governor.md) 」を参照してください。  
  
### <a name="understand-current-resource-utilization"></a>現在のリソース使用率について  
現在実行中の要求のシステムリソース使用率を把握するには、SQL Server PDW 動的管理ビューを使用します。 たとえば、Dmv を使用すると、実行速度の遅い大きなハッシュ結合がメモリを増やすことによってメリットがあるかどうかを把握できます。  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>リソース割り当ての調整  
リソース使用率を調整するには、要求を送信しているログインのリソースクラスのメンバーシップを変更します。 リソースクラスのサーバーロールには、 **mediumrc**、 **largerc**、および**xlargerc**という名前が付けられます。 これらは、それぞれ中規模、大規模、および特大のリソース割り当てを表します。  
  
たとえば、大量のシステムリソースを要求に割り当てるには、要求を送信しているログインを**largerc**サーバーロールに追加します。 次の ALTER SERVER ROLE ステートメントでは、ログイン Anna を largerc サーバーロールに追加します。  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>リソースクラスの説明  
次の表では、リソースクラスとそのシステムリソースの割り当てについて説明します。  
  
|リソース クラス|要求の重要度|最大メモリ使用量 *|同時実行スロット (最大 = 32)|説明|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|中|400 MB|1 で保護されたプロセスとして起動されました|既定では、各ログインには、少量のメモリと、その要求に対する同時実行リソースが許可されます。<br /><br />リソースクラスにログインを追加すると、新しいクラスが優先されます。 ログインがすべてのリソースクラスから削除されると、ログインは既定のリソース割り当てに戻ります。|  
|MediumRC|中|1200 MB|3|中規模リソースクラスを必要とする可能性のある要求の例を次に示します。<br /><br />大きなハッシュ結合を持つ CTAS 操作。<br /><br />ディスクへのキャッシュを回避するために、より多くのメモリを必要とする操作を選択します。<br /><br />クラスター化列ストアインデックスへのデータの読み込み。<br /><br />10-15 列を含む小さいテーブルのクラスター化列ストアインデックスを構築、再構築、再編成します。|  
|Largerc|高|2.8 GB|7|大きなリソースクラスを必要とする可能性のある要求の例を次に示します。<br /><br />大量のハッシュ結合を持つか、大きな集計 (large ORDER BY 句や GROUP BY 句など) を含む非常に大きな CTAS 操作。<br /><br />ハッシュ結合などの操作に非常に大量のメモリを必要とする操作、または ORDER BY 句や GROUP BY 句などの集計を選択します。<br /><br />クラスター化列ストアインデックスへのデータの読み込み。<br /><br />10-15 列を含む小さいテーブルのクラスター化列ストアインデックスを構築、再構築、再編成します。|  
|xlargerc|高|8.4 GB|22|特大のリソースクラスは、実行時に追加の大規模なリソース消費が必要になる可能性のある要求に使用されます。|  
  
<sup>*</sup>最大メモリ使用量は近似値です。  
  
### <a name="request-importance"></a>要求の重要度  
要求の重要度は、コンピューティングノードで実行されている SQL Server の CPU 時間によって、要求に割り当てられます。  優先順位の高い要求には、より多くの CPU 時間が与えられます。  
  
### <a name="maximum-memory-usage"></a>メモリの最大使用量  
最大メモリ使用量は、要求が各処理領域内で使用できるメモリの最大量です。 たとえば、mediumrc 要求では、各ディストリビューション内の処理に最大 1200 MB を使用できます。 ほとんどの作業を実行するディストリビューションが少数にならないように、データがスキューされないようにすることも重要です。  
  
### <a name="concurrency-slots"></a>同時実行スロット  
1、3、7、および22の同時実行スロットを割り当てることの目標は、大規模なプロセスの実行中に小さなプロセスをブロックすることなく、大規模なプロセスと小さいプロセスの両方を同時に実行できるようにすることです。  たとえば、SQL Server PDW は最大32の同時実行スロットを割り当てて、1つの特大の要求 (22 個のスロット)、1つの大きな要求 (7 個のスロット)、および1つの中程度の要求 (3 スロット) を同時に実行できます。  
  
同時実行要求に最大32の同時実行スロットを割り当てる例を次に示します。  
  
-   28スロット = 4 large  
  
-   30スロット = 10 m  
  
-   32スロット = 既定値32  
  
-   32スロット = 1 超 large + 1 large + 1 medium  
  
-   32スロット = 2 large + 4 medium + 6 既定  
  
6個の大きな要求が SQL Server PDW に送信され、10個の既定の要求が送信されたとします。 SQL Server PDW は、次のように、優先順位に従って要求を処理します。  
  
-   メモリが使用可能になったときに4つの大きな要求の処理を開始するために28個の同時実行スロットを割り当て、キューに2つの大きな要求を保持します。  
  
-   4つの既定の要求の処理を開始し、待機キューで6個の既定の要求を保持するために、4つの同時実行スロットを割り当てます。  
  
要求の完了と同時実行スロットが使用可能になると、SQL Server PDW は使用可能なリソースと優先度に従って残りの要求を割り当てます。 たとえば、7つの同時実行スロットが開いている場合、サイズの大きい要求の待機は、中程度の要求を待機している7つのスロットに対して高い優先順位を持ちます。  6個のスロットが開いている場合、SQL Server PDW によって、既定のサイズの要求が6つ割り当てられます。 ただし、SQL Server PDW が要求を実行できるようにするには、メモリと同時実行スロットがすべて使用可能である必要があります。  
  
各リソースクラス内では、要求が先入れ先出し (FIFO) の順序で実行されます。  
  
## <a name="GeneralRemarks"></a>一般的な解説  
ログインが複数のリソースクラスのメンバーである場合は、最も多くのリソースを持つクラスが優先されます。  
  
リソースクラスに対してログインが追加または削除されると、その変更は、今後のすべての要求に対して直ちに有効になります。実行中または待機中の現在の要求は影響を受けません。 このログインは、変更を行うために切断して再接続する必要はありません。  
  
各ログインについて、リソースクラスの設定は、セッションではなく、個々のステートメントと操作に適用されます。  
  
SQL Server PDW は、ステートメントを実行する前に、要求に必要な同時実行スロットを取得しようとします。 十分な数の同時実行スロットを取得できない場合、SQL Server PDW は要求を実行待ち状態に移行します。 要求に既に割り当てられていたすべてのリソースシステムが、システムに戻されます。  
  
ほとんどの SQL ステートメントは、既定のリソース割り当てを常に必要とするため、リソースクラスによって制御されません。 たとえば、CREATE LOGIN は少量のリソースのみを必要とし、CREATE LOGIN を呼び出したログインがリソースクラスのメンバーである場合でも、既定のリソースが割り当てられます。  たとえば、Anna が largerc リソースクラスのメンバーであり、ユーザーが CREATE LOGIN ステートメントを送信した場合、CREATE LOGIN ステートメントは既定の数のリソースを使用して実行されます。  
  
リソースクラスによって管理される SQL ステートメントと操作:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   クラスター化インデックスの作成  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   SELECT としてリモートテーブルを作成する  
  
-   **Dwloader**を使用してデータを読み込んでいます。  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   コンピューティングノードの数が多いアプライアンスに復元する場合は、データベースを復元します。  
  
-   選択 (DMV のみのクエリを除く)  
  
## <a name="Limits"></a>制限事項と制約事項  
リソースクラスは、メモリと同時実行の割り当てを制御します。  入力/出力操作は制御されません。  
  
## <a name="Metadata"></a>Metadata  
リソースクラスおよびリソースクラスのメンバーに関する情報を含む Dmv。  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
要求の状態と必要なリソースに関する情報を含む Dmv。  
  
-   [dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
コンピューティングノードの SQL Server Dmv から公開された関連するシステムビュー。 MSDN のこれらの Dmv へのリンクについては、「 [SQL Server 動的管理ビュー](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) 」を参照してください。  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>関連タスク  
[ワークロード管理タスク](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
