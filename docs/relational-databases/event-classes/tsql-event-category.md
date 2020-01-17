---
title: TSQL イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, TSQL event category
- TSQL event category [SQL Server]
- event classes [SQL Server], TSQL event category
ms.assetid: 215f8747-64b5-4bf3-9845-d476b10cda3a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: af5cd09c9c00c0b250f1b51c72ce642be01dc9a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996078"
---
# <a name="tsql-event-category"></a>TSQL イベント カテゴリ
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **TSQL** イベント カテゴリには一般的な TSQL イベントが含まれます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[Exec Prepared SQL イベント クラス](../../relational-databases/event-classes/exec-prepared-sql-event-class.md)|SqlClient、ODBC、OLE DB、または DB-Library が、準備された 1 つまたは複数の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行したことを示します。|  
|[Prepare SQL イベント クラス](../../relational-databases/event-classes/prepare-sql-event-class.md)|SqlClient、ODBC、OLE DB、または DB-Library が、1 つまたは複数の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用するために準備したことを示します。|  
|[SQL:BatchCompleted イベント クラス](../../relational-databases/event-classes/sql-batchcompleted-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ処理が完了したことを示します。|  
|[SQL:BatchStarting イベント クラス](../../relational-databases/event-classes/sql-batchstarting-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ処理が開始したことを示します。|  
|[SQL:StmtCompleted イベント クラス](../../relational-databases/event-classes/sql-stmtcompleted-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが完了したことを示します。|  
|[SQL:StmtRecompile イベント クラス](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)|ストアド プロシージャ、トリガー、アドホック バッチ、クエリなど、すべての種類のバッチに起因するステートメント レベルの再コンパイルが発生したことを示します。|  
|[SQL:StmtStarting イベント クラス](../../relational-databases/event-classes/sql-stmtstarting-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが開始したことを示します。|  
|[Unprepare SQL イベント クラス](../../relational-databases/event-classes/unprepare-sql-event-class.md)|SqlClient、ODBC、OLE DB、または DB-Library が、準備された 1 つまたは複数の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを削除したことを示します。|  
|[XQuery Static Type イベント クラス](../../relational-databases/event-classes/xquery-static-type-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって XQuery 式が実行された場合に発生します。|  
  
## <a name="see-also"></a>参照  
 [TRANSACT-SQL リファレンス &#40;データベース エンジン&#41;](../../t-sql/transact-sql-reference-database-engine.md)  
  
  
