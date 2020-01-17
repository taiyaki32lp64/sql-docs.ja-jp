---
title: 'レッスン 3: サブスクリプションの検証と待機時間の計測 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 6968331bc7699334f61997ec6a16e521c158078a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721052"
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>レッスン 3: サブスクリプションの検証と待機時間の計測
  このレッスンでは、トレーサー トークンを使用して、変更がサブスクライバーにレプリケートされているかどうかを検証し、待機時間を計測します。待機時間とは、パブリッシャーで加えられた変更がサブスクライバーに反映されるまでの所用時間です。 このレッスンでは、前のレッスンを完了している必要があります[レッスン 2。トランザクション パブリケーションに対するサブスクリプションを作成する](lesson-2-creating-a-subscription-to-the-transactional-publication.md)します。  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>トレーサー トークンを挿入してトークンの情報を表示するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続します。次に、サーバー ノードを展開して **[レプリケーション]** フォルダーを右クリックし、 **[レプリケーション モニターの起動]** をクリックします。  
  
     レプリケーション モニターが起動します。  
  
2.  左ペインでパブリッシャー グループを展開し、パブリッシャー インスタンスを展開して、 **[AdvWorksProductTrans]** パブリケーションをクリックします。  
  
3.  **[トレーサー トークン]** タブをクリックします。  
  
4.  **[トレーサーの挿入]** をクリックします。  
  
5.  次の列にトレーサー トークンの経過時間を表示します。 **[Publisher to Distributor]\(パブリッシャーからディストリビューターまで\)** 、 **[Distributor to Subscriber]\(ディストリビューターからサブスクライバーまで\)** 、 **[合計待機時間]** 。 **[保留中]** と表示された場合は、トークンが特定のポイントに到達していないことを示します。  
  
## <a name="next-steps"></a>次の手順  
 このレッスンでは、トレーサー トークンを使用して、データの変更がパブリッシャーからスクライバへレプリケートされているかどうかを検証しました。 パブリッシャー側の **Product** テーブルに対してデータの挿入、更新、または削除を行い、レプリケーション後、サブスクライバー側の **Product** テーブルをクエリすることもできます。  
  
 チュートリアル「常時接続サーバー間でのデータのレプリケーション」はこれで完了です。 マージ レプリケーションを使用する類似のチュートリアルを参照してください。[チュートリアル。モバイル クライアントとデータをレプリケートする](tutorial-replicating-data-with-mobile-clients.md)します。  
  
## <a name="see-also"></a>参照  
 [トランザクション レプリケーションの待機時間の計測および接続の検証](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
