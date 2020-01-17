---
title: レプリケーションの種類 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: aa6cc0eb253c0f21a1b66870f9dac2607f65e2e3
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769297"
---
# <a name="types-of-replication"></a>レプリケーションの種類
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、以下の種類のレプリケーションを分散アプリケーションで利用できます。  

| **型** | **[説明]** |
|:-------- | :-------------- |
| [トランザクション レプリケーション](transactional/transactional-replication.md)| パブリッシャーの変更は、発生すると (ほぼリアルタイムで) サブスクライバーに配信されます。 データの変更は、パブリッシャーで発生したときと同じ順序で、同じトランザクションの境界内でサブスクライバーに適用されます。 | 
| [マージ レプリケーション](merge/merge-replication.md) | データはパブリッシャーとサブスクライバーの両方で変更される可能性があり、トリガーを使用して追跡されます。 サブスクライバーは、ネットワークに接続されたときにパブリッシャーと同期して、前回の同期以降にパブリッシャーとサブスクライバーの間で変更されたすべての行を交換します。 | 
| [スナップショット レプリケーション](snapshot-replication.md) | パブリッシャーからサブスクライバーにスナップショットを適用します。これにより、特定の時点で出現するとおりにデータが配信され、データの更新は監視されません。 同期が発生するとデータ全体のスナップショットが作成され、サブスクライバーに送信されます。| 
| [ピア ツー ピア](transactional/peer-to-peer-transactional-replication.md) | ピア ツー ピア レプリケーションはトランザクション レプリケーションを基礎としており、トランザクション的に一貫性のある変更がほぼリアルタイムで複数のサーバー インスタンス間に反映されます。 | 
| [双方向](transactional/bidirectional-transactional-replication.md)| 双方向トランザクション レプリケーションとは、トランザクション レプリケーションの中でも特に、2 台のサーバーが互いに変更内容を交換し合うことのできるトポロジのことです。各サーバーはデータをパブリッシュすると共に、同じデータを含んだパブリケーションをもう一方のサーバーからサブスクライブします。 | 
| [更新可能なサブスクリプション](transactional/updatable-subscriptions-for-transactional-replication.md) | トランザクション レプリケーションの基礎に基づいて構築されており、更新可能なサブスクリプションのサブスクライバーでデータが更新されると、まずパブリッシャーに反映され、次に他のサブスクライバーに反映されます。 | 
  
 
アプリケーションで使用するレプリケーションの種類は、物理的なレプリケーション環境、レプリケートするデータの種類と量、データをサブスクライバーで更新するかどうかなどの、さまざまな要因によって異なります。 物理環境には、レプリケーションに関係するコンピューターの数と場所、これらのコンピューターがクライアント (ワークステーション、ラップトップ、またはハンドヘルド デバイス) なのかサーバーなのか、などが含まれます。  
  
どの種類のレプリケーションも、通常、パブリッシュされたオブジェクトをパブリッシャーとサブスクライバー間で初期同期することから始まります。 初期同期は、 *スナップショット*を使用したレプリケーションで実行できます。スナップショットは、パブリケーションで指定されたすべてのオブジェクトおよびデータのコピーです。 作成されたスナップショットはサブスクライバーに配信されます。 アプリケーションによっては、スナップショット レプリケーションのみで十分なこともあります。 スナップショット レプリケーションだけでは不十分なアプリケーションでは、その後行われたデータ変更が、一定期間にわたって増分としてサブスクライバーに渡されることが重要です。 また、アプリケーションによっては、サブスクライバーからパブリッシャーに変更を送り返す必要もあります。 トランザクション レプリケーションおよびマージ レプリケーションには、このような種類のアプリケーション用のオプションがあります。  
  
 
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)
  
  
