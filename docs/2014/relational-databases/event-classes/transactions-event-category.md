---
title: Transactions イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 076e68de4dc5d4e25f6cabe6b39ac4a61a05033a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062230"
---
# <a name="transactions-event-category"></a>Transactions イベント カテゴリ
  **Transactions** イベント カテゴリのイベント クラスを使用すると、トランザクションの状態を監視できます。 **TM:** というプレフィックスが付いたイベント クラス名は、トランザクション管理のインターフェイス経由で送信されたトランザクション関連の操作を追跡する場合に使用します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[DTCTransaction イベント クラス](dtctransaction-event-class.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) によってコーディネートされたトランザクションを追跡します。 これらは、複数のデータベース間または [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンス間で分散されたトランザクションです。|  
|[SQLTransaction イベント クラス](sqltransaction-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] の BEGIN TRAN、COMMIT TRAN、SAVE TRAN、および ROLLBACK TRAN の各ステートメントを追跡します。|  
|[TM:Begin Tran Completed イベント クラス](tm-begin-tran-completed-event-class.md)|BEGIN TRANSACTION 要求が完了したことを示します。|  
|[TM:Begin Tran Starting イベント クラス](tm-begin-tran-starting-event-class.md)|BEGIN TRANSACTION 要求が開始されていることを示します。|  
|[TM:Commit Tran Completed イベント クラス](tm-commit-tran-completed-event-class.md)|COMMIT TRANSACTION 要求が完了したことを示します。|  
|[TM:Commit Tran Starting イベント クラス](tm-commit-tran-starting-event-class.md)|COMMIT TRANSACTION 要求が開始されていることを示します。|  
|[TM:Promote Tran Completed イベント クラス](tm-promote-tran-completed-event-class.md)|PROMOTE TRANSACTION 要求が完了したことを示します。|  
|[TM:Promote Tran Starting イベント クラス](tm-promote-tran-starting-event-class.md)|PROMOTE TRANSACTION 要求が開始されていることを示します。|  
|[TM:Rollback Tran Completed イベント クラス](tm-rollback-tran-completed-event-class.md)|ROLLBACK TRANSACTION 要求が完了したことを示します。|  
|[TM:Rollback Tran Starting イベント クラス](tm-rollback-tran-starting-event-class.md)|ROLLBACK TRANSACTION 要求が開始されていることを示します。|  
|[TM:Save Tran Completed イベント クラス](tm-save-tran-completed-event-class.md)|SAVE TRANSACTION 要求が完了したことを示します。|  
|[TM:Save Tran Starting イベント クラス](tm-save-tran-starting-event-class.md)|SAVE TRANSACTION 要求が開始されていることを示します。|  
|[TransactionLog イベント クラス](transactionlog-event-class.md)|トランザクションがデータベース トランザクション ログに書き込まれる時点を追跡します。|  
  
  
