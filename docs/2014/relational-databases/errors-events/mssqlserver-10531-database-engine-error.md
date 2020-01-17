---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7324979238eda7f3ee63a709c199878350edb82d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916199"
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10531|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_NO_ELIGIBLE_STMT|  
|メッセージ テキスト|プラン ガイド '%.*ls' をキャッシュから作成できません。ユーザーに適切な権限がありません。 プラン ガイドを作成するユーザーに VIEW SERVER STATE 権限を付与してください。|  
  
## <a name="explanation"></a>説明  
 指定したプラン ガイドをプラン キャッシュから作成するための適切な権限がユーザーにありません。  
  
## <a name="user-action"></a>ユーザーの操作  
 プラン ガイドを作成するユーザーに VIEW SERVER STATE 権限を付与します。  
  
## <a name="see-also"></a>参照  
 [プラン ガイド](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
