---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0cdf2c06311e703b6a07667ba41d1c853c17eb86
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305889"
---
# <a name="mssqlserver_10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10509|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PG_INVALID_STMT|  
|メッセージ テキスト|プラン ガイド '%.\*ls' を作成できません。 **\@stmt** または **\@statement_start_offset** で指定されたステートメントは、構文エラーを含んでいるか、プラン ガイドで使用するには不適切です。 有効な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを 1 つだけ指定するか、またはバッチ内のステートメントの有効な開始位置を指定します。 有効な開始位置を取得するには、動的管理関数 sys.dm_exec_query_stats の statement_start_offset 列のクエリを実行します。|  
  
## <a name="explanation"></a>説明  
**\@stmt** または **\@statement_start_offset** で指定されたステートメントは、構文エラーを含んでいるか、プラン ガイドで使用するには不適切です。  
  
## <a name="user-action"></a>ユーザーの操作  
有効な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを 1 つだけ指定するか、またはバッチ内のステートメントの有効な開始位置を指定します。 有効な開始位置を取得するには、動的管理関数 sys.dm_exec_query_stats の statement_start_offset 列のクエリを実行します。  
  
## <a name="see-also"></a>参照  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[プラン ガイド](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
