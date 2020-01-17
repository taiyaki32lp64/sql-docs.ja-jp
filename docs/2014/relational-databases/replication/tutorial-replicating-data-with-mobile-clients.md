---
title: チュートリアル:モバイル クライアントとデータをレプリケートする |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c36eae0ca3d9613dfdaf13bce3a5e748f91b123f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255395"
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>チュートリアル:モバイル クライアントとの間のデータのレプリケーション
  レプリケーションは、中央のサーバーと、常時接続でないモバイル クライアントの間でデータを移動する際の問題を解決する有効なソリューションです。 レプリケーション ウィザードを使用すると、レプリケーション トポロジを簡単に設定し、管理できます。 このチュートリアルでは、モバイル クライアント用のレプリケーション トポロジを設定する方法を学習します。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、マージ レプリケーションを使用して中央のデータベースから 1 名以上のモバイル ユーザーにデータをパブリッシュし、各ユーザーが独自にフィルター選択されたデータ サブセットを取得するようにします。 最初のレッスンでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使ってパブリケーションを作成する方法を学習し、 後のレッスンではサブスクリプションを作成および同期する方法を学習します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルは、データベースの基本的な操作は理解しているが、レプリケーション機能についてはあまり詳しくないユーザーを対象としています。 このチュートリアルを行うには、[チュートリアル: レプリケーションのため、サーバーを準備](tutorial-preparing-the-server-for-replication.md)します。  
  
 このチュートリアルを使用するには、システムに次のコンポーネントがインストールされている必要があります。  
  
-   パブリッシャー サーバー側 (レプリケーション元) :  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]の任意のエディション。ただし、Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) と [!INCLUDE[ssEW](../../includes/ssew-md.md)]は除きます。 レプリケーションのパブリッシャーとして使用できないため除きます。  
  
    -   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベース。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。  
  
-   サブスクライバー サーバー側 (レプリケーション先) :  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]の任意のエディション。ただし、 [!INCLUDE[ssEW](../../includes/ssew-md.md)]は除きます。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] は、このチュートリアルで作成するパブリケーションで使用できません。  
  
    > [!NOTE]  
    >  既定では、レプリケーションは [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]にインストールされません。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、固定サーバー ロール sysadmin のメンバーとしてログインし、パブリッシャーとサブスクライバーに接続する必要があります。  
  
 **このチュートリアルの推定所要時間: 30 分。**  
  
## <a name="lessons-in-this-tutorial"></a>このチュートリアルで行うレッスン  
  
-   [レッスン 1:マージ レプリケーションを使用してデータのパブリッシュ](lesson-1-publishing-data-using-merge-replication.md)  
  
-   [レッスン 2:マージ パブリケーションに対するサブスクリプションを作成します。](lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
 [チュートリアルを開始する](merge/merge-replication.md)  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのプログラミング概念](concepts/replication-programming-concepts.md)  
  
  
