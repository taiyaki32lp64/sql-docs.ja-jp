---
title: Windows 上で PolyBase スケールアウト グループを構成する | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: tutorial
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: d686cbe2fb314a59085adee76b3bbad22fcea0fc
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906885"
---
# <a name="configure-polybase-scale-out-groups-on-windows"></a>Windows 上で PolyBase スケールアウト グループを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、Windows 上で [PolyBase スケールアウト グループ](polybase-scale-out-groups.md)を設定する方法について説明します。 これにより、Hadoop や Azure Blob Storage などの外部データ ソースからの大量のデータ セットを、クエリ パフォーマンスの向上のためにスケールアウト形式で処理するために、SQL Server インスタンス クラスターが作成されます。

## <a name="prerequisites"></a>Prerequisites
  
- 同じドメイン内の複数のマシン  
  
- PolyBase サービスを実行するドメイン ユーザー アカウント  
  
## <a name="process-overview"></a>プロセスの概要

次の手順は、PolyBase スケールアウト グループを作成するプロセスをまとめたものです。 次のセクションでは、各手順の詳細なチュートリアルを提供します。
  
1. N 台のマシンに、同じバージョンの SQL Server と PolyBase をインストールします。
  
2. 1 つの SQL Server インスタンスをヘッド ノードとして選択します。 ヘッド ノードは、SQL Server Enterprise を実行するインスタンスでのみ指定できます。
  
3. [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md) を使用して、残りの SQL Server インスタンスをコンピューティング ノードとして追加します。

4. [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) を使用して、グループのノードを監視します。

5. 省略可。 [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md) を使用して、コンピューティング ノードを削除します。

## <a name="example-walk-through"></a>サンプル チュートリアル

ここでは、次のものを使用して PolyBase グループを構成する手順について説明します。  
  
1. ドメイン *PQTH4A* 内の 2 つのマシン。マシン名は次のとおりです。  
  
   - PQTH4A-CMP01  
  
   - PQTH4A-CMP02  
  
2. ドメイン アカウント:*PQTH4A\PolyBaseUse*r  

## <a name="install-sql-server-with-polybase-on-all-machines"></a>すべてのマシンに、PolyBase を使用する SQL Server をインストールする

1. setup.exe を実行します。
  
2. [機能の選択] ページで、 **[外部データ用 PolyBase クエリ サービス]** を選択します。
  
3. [サーバーの構成] ページで、SQL Server PolyBase エンジンと SQL Server PolyBase Data Movement サービス用に**ドメイン アカウント** PQTH4A\PolyBaseUser を使用します。
  
4. [PolyBase の構成] ページで、 **[PolyBase スケール アウト グループの一部として、SQL Server インスタンスを使用します]** オプションを選択します。 これにより、ファイアウォールが開かれて、PolyBase サービスへの着信接続が許可されます。
  
5. セットアップが完了したら、 **services.msc**を実行します。 SQL Server、PolyBase エンジン、および PolyBase データ移動サービスが実行されていることを確認します。
  
   ![PolyBase サービス](../../relational-databases/polybase/media/polybase-services.png "PolyBase サービス")  
  
## <a name="select-one-sql-server-as-head-node"></a>1 つの SQL Server をヘッド ノードとして選択する  
  
セットアップが完了すると、両方のマシンが PolyBase グループのヘッド ノードとして機能できます。 この例では、PQTH4A-CMP01 上の "MSSQLSERVER" をヘッド ノードとして選択します。
  
## <a name="add-other-sql-server-instances-as-compute-nodes"></a>その他の SQL Server インスタンスをコンピューティング ノードとして追加する  
  
1. PQTH4A-CMP02 上の SQL Server に接続します。
  
2. ストアド プロシージャ [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)を実行します。

   ```sql
   -- Enter head node details:
   -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';
   ```  

3. コンピューティング ノード (PQTH4A-CMP02) で、services.msc を実行します。
  
4. PolyBase エンジンをシャット ダウンし、PolyBase データ移動サービスを再起動します。
  
## <a name="optional-remove-a-compute-node"></a>省略可能:コンピューティング ノードを削除する  
  
1. コンピューティング ノードの SQL Server (PQTH4A-CMP02) に接続します。
  
2. ストアド プロシージャ sp_polybase_leave_group を実行します。
  
    ```sql  
    EXEC sp_polybase_leave_group;  
    ```  
  
3. 削除するコンピューティング ノード (PQTH4A-CMP02) で、services.msc を実行します。
  
4. PolyBase エンジンを起動します。 PolyBase データ移動サービスを再起動します。
  
5. PQTH4A-CMP01 で DMV sys.dm_exec_compute_nodes を実行して、ノードが削除されたことを確認します。 これで、PQTH4A-CMP02 はスタンドアロンのヘッド ノードとして機能するようになります。  
  
## <a name="next-steps"></a>次の手順  

トラブルシューティングについては、「 [PolyBase troubleshooting with dynamic management views](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)」を参照してください。
  
PolyBase について詳しくは、[PolyBase の概要](../../relational-databases/polybase/polybase-guide.md)に関する記事をご覧ください。
