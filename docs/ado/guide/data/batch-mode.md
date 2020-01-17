---
title: バッチ モード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 188a95f985ac1d578bca8c7e10ac4c4054c935c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925955"
---
# <a name="batch-mode"></a>バッチ モード
バッチ モードが有効なときに、 **LockType**プロパティに設定されて**adLockBatchOptimistic**バッチ更新プロバイダーによってサポートされています。 カーソル位置に応じて特定のロックの種類の設定が利用できません。 たとえば、ペシミスティック ロックの種類場合は使用できません、 **CursorLocation**に設定されている**adUseClient**します。 逆に、プロバイダーは、サーバー カーソルの場所がある場合、バッチ オプティミスティック ロックをサポートできません。 バッチ更新を keyset または static カーソルのみを使用する必要があります。  
  
 **UpdateBatch**メソッドを使用して、送信**Recordset**変更は、データ ソースを更新するサーバーに、コピー バッファーに保持します。 次のセクションで開くが、**レコード セット**バッチ モードで、コピー バッファーに変更を加えるし、呼び出しに使用してデータ ソースに変更を送信**UpdateBatch**します。  
  
 このセクションでは、次のトピックについて説明します。  
  
-   [更新プログラムの送信。UpdateBatch メソッド](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [更新されたレコードのフィルター処理](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [失敗した更新の処理](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [競合の検出および解決](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [レコードセットの切断と再接続](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [結合の結果を更新します。一意テーブル](../../../ado/guide/data/updating-joined-results-unique-table.md)
