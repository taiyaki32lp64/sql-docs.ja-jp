---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 85901c0fc1a720849cb93f7392ade34ff1db35e0
ms.sourcegitcommit: 0ea19d8e3bd9d91a416311e00a5fb0267d41949e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71174281"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10536|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_TOO_MANY_STMTS|  
|メッセージ テキスト|プラン ガイド '%.\*ls' を作成できません。指定された **\@plan_handle** に対応するバッチまたはモジュールに含まれるステートメントが 1000 個を超えています。 バッチまたはモジュール内の各ステートメントに **statement_start_offset** 値を指定して、各ステートメントにプラン ガイドを作成してください。|  
  
## <a name="explanation"></a>説明  
指定した **\@plan_handle** に対応するバッチまたはモジュールに、条件を満たすステートメントが 1000 以上含まれています。  
  
## <a name="user-action"></a>ユーザーの操作  
バッチまたはモジュール内の各ステートメントに **statement_start_offset** 値を指定して、各ステートメントにプラン ガイドを作成してください。  
  
## <a name="see-also"></a>参照  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[プラン ガイド](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
