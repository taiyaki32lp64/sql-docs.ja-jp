---
title: チュートリアル:接続サーバー間でデータを継続的にレプリケーション |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 32b97d456c42eab89511d8f5a9d1924914ea81ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655393"
---
# <a name="tutorial-replicating-data-between-continuously-connected-servers"></a>チュートリアル:常時接続サーバー間でのデータのレプリケーション
  レプリケーションは、常時接続サーバー間でデータを移動する際の問題を解決する有効なソリューションです。 レプリケーション ウィザードを使用すると、レプリケーション トポロジを簡単に設定し、管理できます。 このチュートリアルでは、常時接続サーバー間にレプリケーション トポロジを設定する方法を学習します。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、トランザクション レプリケーションによって 1 つのデータベースから別のデータベースにデータをパブリッシュする方法を学習します。 最初のレッスンでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使ってパブリケーションを作成する方法を学習し、 後のレッスンでは、サブスクリプションを作成および検証する方法と、待機時間を計測する方法を学習します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルは、データベースの基本的な操作は理解しているが、レプリケーション機能についてはあまり詳しくないユーザーを対象としています。 このチュートリアルを学習するには、前のチュートリアル「 [レプリケーションに備えたサーバーの準備](tutorial-preparing-the-server-for-replication.md)」を完了している必要があります。  
  
 このチュートリアルを使用するには、システムに次のコンポーネント必要です。  
  
-   パブリッシャー サーバー側 (レプリケーション元) :  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の任意のエディション。ただし、Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) と [!INCLUDE[ssEW](../../includes/ssew-md.md)]は除きます (これらのエディションはレプリケーションのパブリッシャーとして使用できません)。  
  
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] サンプル データベース。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。  
  
-   サブスクライバー サーバー側 (レプリケーション先) :  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の任意のエディション。ただし、 [!INCLUDE[ssEW](../../includes/ssew-md.md)]は除きます。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] は、トランザクション レプリケーションのサブスクライバーとして使用できません。  
  
    > [!NOTE]  
    >  既定では、レプリケーションは [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] にインストールされません。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、固定サーバー ロール **sysadmin** のメンバーとしてログインし、パブリッシャーとサブスクライバーに接続する必要があります。  
  
 **このチュートリアルの推定所要時間: 30 分。**  
  
## <a name="lessons-in-this-tutorial"></a>このチュートリアルで行うレッスン  
  
-   [レッスン 1:トランザクション レプリケーションを使用してデータのパブリッシュ](lesson-1-publishing-data-using-transactional-replication.md)  
  
-   [レッスン 2:トランザクション パブリケーションに対するサブスクリプションを作成します。](lesson-2-creating-a-subscription-to-the-transactional-publication.md)  
  
-   [レッスン 3:サブスクリプションの検証と待機時間の計測](lesson-3-validating-the-subscription-and-measuring-latency.md)  
  
 [チュートリアルを開始する](transactional/transactional-replication.md)  
  
## <a name="see-also"></a>参照  
 [レプリケーションのプログラミング概念](concepts/replication-programming-concepts.md)  
  
  
