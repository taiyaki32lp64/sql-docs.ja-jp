---
title: 既定のトレース ログ ファイルの無効化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2ab57498c9b188818663cfe326287ee3f45a409f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705356"
---
# <a name="default-trace-log-files-disabled"></a>既定のトレース ログ ファイルの無効化
  このルールでは、sp_configure システム ストアド プロシージャの default trace enabled オプションの値を調べて、既定のトレースが ON (1) または OFF (0) のどちらに設定されているかを確認します。 このオプションを有効にした場合、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に対する構成および DDL の変更に関する情報が既定のトレースによって提供されます。 この情報は、顧客および [!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタマー サポート サービスが、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に関する問題のトラブルシューティングを行うときに役立つ場合があります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 sp_configure stored ストアド プロシージャを使用して default trace enabled の値を 1 に設定することで、トレースを有効にしてください。  
  
## <a name="for-more-information"></a>詳細情報  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
