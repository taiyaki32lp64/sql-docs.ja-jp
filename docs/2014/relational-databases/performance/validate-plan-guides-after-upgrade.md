---
title: アップグレード後のプラン ガイドの検証 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3f3f8fd278d1141417adec4f1ef6a1faced386c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151212"
---
# <a name="validate-plan-guides-after-upgrade"></a>アップグレード後のプラン ガイドの検証
  アプリケーションを新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリリースにアップグレードした場合は、プラン ガイドの定義を再評価し、テストすることをお勧めします。 新しいリリースでは、パフォーマンス チューニングの要件とプラン ガイドの照合動作が異なる場合があります。 無効なプラン ガイドが原因でクエリが失敗することはありませんが、そのプラン ガイドは使用されずにプランがコンパイルされるので、最適な選択ではない場合があります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にデータベースをアップグレードした後は、次の作業を実行することをお勧めします。  
  
-   既存のプラン ガイドを [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) 関数を使用して検証する。  
  
-   拡張イベントで、プラン ガイドによって不適切に生成されたプランがないか、 [Plan Guide Unsuccessful](../event-classes/plan-guide-unsuccessful-event-class.md) イベントを使用して一定期間の間監視する。  
  
  
