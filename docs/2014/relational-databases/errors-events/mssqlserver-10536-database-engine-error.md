---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5ddb4df0089b488d3a15c76a76abef8be154848
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870525"
---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10536|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_TOO_MANY_STMTS|  
|メッセージ テキスト|プラン ガイドを作成することはできません ' % です。\*ls' ため、バッチまたはモジュールを指定された対応する`@plan_handle`ステートメントが 1000 以上が含まれています。 バッチまたはモジュールの各ステートメントに対して `statement_start_offset` 値を指定して、ステートメントごとにプラン ガイドを作成します。|  
  
## <a name="explanation"></a>説明  
 指定した `@plan_handle` に対応するバッチまたはモジュールに、条件を満たすステートメントが 1000 以上含まれています。  
  
## <a name="user-action"></a>ユーザーの操作  
 バッチまたはモジュールの各ステートメントに対して `statement_start_offset` 値を指定して、ステートメントごとにプラン ガイドを作成します。  
  
## <a name="see-also"></a>参照  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [プラン ガイド](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
