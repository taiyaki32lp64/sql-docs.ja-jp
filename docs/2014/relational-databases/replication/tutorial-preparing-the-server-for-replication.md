---
title: チュートリアル:レプリケーションのためのサーバーの準備 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9b8ed6778a087c2200012c6df1409b187b39329
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199068"
---
# <a name="tutorial-preparing-the-server-for-replication"></a>チュートリアル:レプリケーションに備えたサーバーの準備
  レプリケーション トポロジを構成するには、事前にセキュリティ計画を立てることが重要です。 このチュートリアルでは、レプリケーション トポロジのセキュリティを向上する方法と、データのレプリケートで最初のステップとなるディストリビューションの構成方法を学習します。 他のチュートリアルを行う前に、まずこのチュートリアルを実行してください。  
  
> [!NOTE]  
>  サーバー間でデータを安全にレプリケートするには、「 [レプリケーション セキュリティの推奨事項](security/replication-security-best-practices.md)」の推奨事項をすべて実践してください。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、サーバーを準備し、レプリケーションを最小の特権で安全に実行できるようにする方法を学習します。 最初のレッスンでは、レプリケーション エージェントの実行に使用する Windows サービス アカウントの作成方法を学習します。 2 番目のレッスンでは、パブリケーション スナップショットの生成と保存に使用するフォルダーの構成方法を学習します。 3 番目のレッスンでは、ディストリビューションの構成方法と権限の設定方法を学習します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルは、データベースの基本的な操作は理解しているが、レプリケーション機能についてはあまり詳しくないユーザーを対象としています。  
  
 このチュートリアルを使用するには、システムに次のコンポーネントがインストールされている必要があります。  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] と [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。  
  
 **このチュートリアルの推定所要時間: 30 分。**  
  
## <a name="lessons-in-this-tutorial"></a>このチュートリアルで行うレッスン  
  
-   [レッスン 1:レプリケーション用アカウントの Windows の作成](lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [レッスン 2:スナップショット フォルダーの準備](lesson-2-preparing-the-snapshot-folder.md)  
  
-   [レッスン 3:ディストリビューションの構成](lesson-3-configuring-distribution.md)  
  
 [チュートリアルを開始する](lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>参照  
 [[ディストリビューションの構成]](configure-distribution.md)   
 [SQL Server レプリケーションのセキュリティ](security/view-and-modify-replication-security-settings.md)  
  
  
