---
title: AUTO_SHRINK データベース オプションを OFF に設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2b202f2856e066047c5458ef8ed1f40b2422b391
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021692"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>AUTO_SHRINK データベース オプションを OFF に設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このルールでは、AUTO_SHRINK データベース オプションが OFF に設定されているかどうかをチェックします。 データベースの圧縮と拡張により、物理的な断片化が発生することがよくあります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 AUTO_SHRINK データベース オプションを OFF に設定します。 再利用している領域が今後不要になることがわかっている場合は、データベースを手動で圧縮して領域を再利用できます。  
  
## <a name="for-more-information"></a>詳細情報  
 サポート技術情報の資料 [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
