---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa6bce659e20fb80f013539049cc1b99e3e0b4c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870650"
---
# <a name="mssqlserver10538"></a>MSSQLSERVER_10538
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10538|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_INVALID_PLANGUIDE_HANDLE|  
|メッセージ テキスト|指定したプラン ガイドの ID が NULL または無効であるか、またはプラン ガイドが参照しているオブジェクトに対する権限がないため、プラン ガイドを見つけることができません。 プラン ガイドの ID が有効であること、現在のセッションが適切なデータベース コンテキストに設定されていること、およびプラン ガイドが参照しているオブジェクトに対する ALTER DATABASE 権限または ALTER 権限のいずれかがあることを確認してください。|  
  
## <a name="explanation"></a>説明  
 指定したプラン ガイドの ID が NULL または無効であるか、またはプラン ガイドが参照しているオブジェクトに対する権限がありません。  
  
## <a name="user-action"></a>ユーザーの操作  
 プラン ガイドの ID が有効であること、現在のセッションが適切なデータベース コンテキストに設定されていること、およびプラン ガイドが参照しているオブジェクトに対する ALTER DATABASE 権限または ALTER 権限があることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [プラン ガイド](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
