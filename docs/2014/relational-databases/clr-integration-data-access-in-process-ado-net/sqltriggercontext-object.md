---
title: SqlTriggerContext オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: df384324ba16aac03a4c889cf4f3959c23374510
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874693"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext オブジェクト
  `SqlTriggerContext` クラスでは、トリガーに関するコンテキスト情報が提供されます。 このコンテキスト情報には、トリガーを起動した動作の種類、UPDATE 操作で変更された列が含まれます。DDL (データ定義言語) トリガーの場合は、トリガー操作が記述されている XML `EventData` 構造体も含まれます。 詳細と使用方法の例について、`SqlTriggerContext`クラスを参照してください[CLR トリガー](../../database-engine/dev-guide/clr-triggers.md)します。  
  
 詳細については、次を参照してください。、`Microsoft.SqlServer.Server.SqlTriggerContext`クラスの .NET Framework SDK ドキュメントのリファレンス ドキュメント。  
  
## <a name="see-also"></a>参照  
 [CLR トリガー](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
