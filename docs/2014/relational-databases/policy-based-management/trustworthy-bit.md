---
title: 信頼可能なビット | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c8e03217eef0ee9e23d6efa2bbcb8e715fe64dcb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63252728"
---
# <a name="trustworthy-bit"></a>信頼可能なビット
  このルールでは、sysadmin 固定サーバー ロールにデータベースの dbo ロールが割り当てられているかどうか、およびデータベースの信頼可能なビットがオンに設定されているかどうかを確認します。  
  
 これらの条件が満たされている場合、権限のあるデータベース ユーザーは、特権を sysadmin ロールに昇格させることができます。 このロールでは、ユーザーはシステムを危険にさらす安全ではないアセンブリを作成して実行できます。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 信頼可能なビットをオフにするか、dbo データベース ロールから sysadmin 権限を取り消します。  
  
## <a name="for-more-information"></a>詳細情報  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
