---
title: Transactions イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5de24851562858eced26c7189fca5e786f395b94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069650"
---
# <a name="transactions-event-category"></a>Transactions イベント カテゴリ
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Transactions** イベント カテゴリのイベント クラスを使用すると、トランザクションの状態を監視できます。 **TM:** というプレフィックスが付いたイベント クラス名は、トランザクション管理のインターフェイス経由で送信されたトランザクション関連の操作を追跡する場合に使用します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[DTCTransaction イベント クラス](../../relational-databases/event-classes/dtctransaction-event-class.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) によってコーディネートされたトランザクションを追跡します。 これらは、複数のデータベース間または [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンス間で分散されたトランザクションです。|  
|[SQLTransaction イベント クラス](../../relational-databases/event-classes/sqltransaction-event-class.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] の BEGIN TRAN、COMMIT TRAN、SAVE TRAN、および ROLLBACK TRAN の各ステートメントを追跡します。|  
|[TM:Begin Tran Completed イベント クラス](../../relational-databases/event-classes/tm-begin-tran-completed-event-class.md)|BEGIN TRANSACTION 要求が完了したことを示します。|  
|[TM:Begin Tran Starting イベント クラス](../../relational-databases/event-classes/tm-begin-tran-starting-event-class.md)|BEGIN TRANSACTION 要求が開始されていることを示します。|  
|[TM:Commit Tran Completed イベント クラス](../../relational-databases/event-classes/tm-commit-tran-completed-event-class.md)|COMMIT TRANSACTION 要求が完了したことを示します。|  
|[TM:Commit Tran Starting イベント クラス](../../relational-databases/event-classes/tm-commit-tran-starting-event-class.md)|COMMIT TRANSACTION 要求が開始されていることを示します。|  
|[TM:Promote Tran Completed イベント クラス](../../relational-databases/event-classes/tm-promote-tran-completed-event-class.md)|PROMOTE TRANSACTION 要求が完了したことを示します。|  
|[TM:Promote Tran Starting イベント クラス](../../relational-databases/event-classes/tm-promote-tran-starting-event-class.md)|PROMOTE TRANSACTION 要求が開始されていることを示します。|  
|[TM:Rollback Tran Completed イベント クラス](../../relational-databases/event-classes/tm-rollback-tran-completed-event-class.md)|ROLLBACK TRANSACTION 要求が完了したことを示します。|  
|[TM:Rollback Tran Starting イベント クラス](../../relational-databases/event-classes/tm-rollback-tran-starting-event-class.md)|ROLLBACK TRANSACTION 要求が開始されていることを示します。|  
|[TM:Save Tran Completed イベント クラス](../../relational-databases/event-classes/tm-save-tran-completed-event-class.md)|SAVE TRANSACTION 要求が完了したことを示します。|  
|[TM:Save Tran Starting イベント クラス](../../relational-databases/event-classes/tm-save-tran-starting-event-class.md)|SAVE TRANSACTION 要求が開始されていることを示します。|  
|[TransactionLog イベント クラス](../../relational-databases/event-classes/transactionlog-event-class.md)|トランザクションがデータベース トランザクション ログに書き込まれる時点を追跡します。|  
  
  
