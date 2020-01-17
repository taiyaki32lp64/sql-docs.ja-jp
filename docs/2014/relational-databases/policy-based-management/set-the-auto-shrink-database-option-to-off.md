---
title: AUTO_SHRINK データベース オプションを OFF に設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c81885e5a3aaec197b8963c2e868b6f65a0b0544
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691511"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>AUTO_SHRINK データベース オプションを OFF に設定
  このルールでは、AUTO_SHRINK データベース オプションが OFF に設定されているかどうかをチェックします。 データベースの圧縮と拡張により、物理的な断片化が発生することがよくあります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 AUTO_SHRINK データベース オプションを OFF に設定します。 再利用している領域が今後不要になることがわかっている場合は、データベースを手動で圧縮して領域を再利用できます。  
  
## <a name="for-more-information"></a>詳細情報  
 サポート技術情報の資料 [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
