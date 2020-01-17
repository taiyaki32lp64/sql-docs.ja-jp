---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3aa0ba350e4c1e7e56a545e26793be193b4b5a2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903918"
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|601|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名||  
|メッセージ テキスト|データが移動されたので NOLOCK を使用したスキャンは続行できませんでした。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]が別のトランザクションによって更新または削除されたデータを読み取ろうとしているため、クエリの実行を続行できません。 このクエリでは、NOLOCK ロック ヒントまたは READ UNCOMMITTED トランザクション分離レベルのいずれかが使用されています。  
  
通常、別のトランザクションによって変更されているデータへのアクセスは、データがロックされているために拒否されます。 しかし、NOLOCK ロック ヒントや READ UNCOMMITTED トランザクション分離レベルを使用すると、別のトランザクションによってロックされているデータをクエリで読み取ることができます。 まだコミットされておらず変更される可能性がある値を読み取ることができるため、この操作はダーティ リードと呼ばれます。  
  
## <a name="user-action"></a>ユーザーの操作  
このエラーが発生するとクエリは取り消されます。 クエリを再送信するか、NOLOCK ロック ヒントを削除します。  
  
## <a name="see-also"></a>参照  
[MSSQLSERVER_605](../../relational-databases/errors-events/mssqlserver-605-database-engine-error.md)  
[テーブル ヒント &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-table.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](~/t-sql/statements/set-transaction-isolation-level-transact-sql.md)  
  
