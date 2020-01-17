---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9a20d1003e8b87179e2690fa35ad44b50894568
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870581"
---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10534|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_INVALID_PARAMS|  
|メッセージ テキスト|プラン ガイドを作成することはできません ' % です。\*ls' の指定した値`@params`が無効です。 *parameter_name parameter_type* 形式の値を指定するか、NULL を指定してください。|  
  
## <a name="explanation"></a>説明  
 `@params` に指定した値が無効です。  
  
## <a name="user-action"></a>ユーザーの操作  
 *parameter_name parameter_type* 形式の値を指定するか、NULL を指定してください。  
  
## <a name="see-also"></a>参照  
 [プラン ガイド](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
