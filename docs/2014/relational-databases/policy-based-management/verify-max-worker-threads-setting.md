---
title: max worker threads 設定の検証 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 861e24cf64a29d55a01fc9a10300e4174cd76d5f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676958"
---
# <a name="verify-max-worker-threads-setting"></a>max worker threads 設定の検証
  このルールでは、max worker threads サーバー オプションに不適切な設定がないかどうかを確認します。 max worker threads オプションに小さい値を設定すると、必要な数のスレッドを確保できなくて着信クライアント要求に適切なタイミングで対応できず、"スレッド不足" に陥る可能性があります。 その半面、アクティブな各スレッドは、32 ビット サーバー上で 512 KB、64 ビット サーバー上で最大 4 MB を消費するので、このオプションを大きい値に設定すると、アドレス空間が無駄に使用される可能性があります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 max worker threads オプションを 0 に設定します。 この設定により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ユーザー要求に基づいてアクティブなワーカー スレッドの適切な数が自動的に決定されます。  
  
## <a name="for-more-information"></a>詳細情報  
 [max worker threads サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
