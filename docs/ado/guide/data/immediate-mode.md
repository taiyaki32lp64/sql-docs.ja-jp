---
title: イミディ エイト モード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3952ef502bf79d6704cbaea80b9a825a3c70981b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925014"
---
# <a name="immediate-mode"></a>イミディエイト モード
イミディ エイト モードが有効なときに、 **LockType**プロパティに設定されて**adLockOptimistic**または**adLockPessimistic**します。 操作を宣言する行に完全な呼び出してとすぐには、レコードへの変更をデータ ソースに反映するようイミディ エイト モードで、 **Update**メソッド。  
  
## <a name="calling-update"></a>更新プログラムを呼び出す  
 レコードから移動した場合の追加または編集する呼び出しの前に、 **Update**メソッド、ADO の呼び出しが自動的に**Update**変更を保存します。 呼び出す必要があります、 **CancelUpdate**メソッドは、現在のレコードに加えられた変更をキャンセルするか、新しく追加したレコードを破棄する場合に移動する前にします。  
  
 現在のレコードを呼び出した後は、最新の状態、 **Update**メソッド。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 使用して、 **CancelUpdate**メソッド、現在の行に加えられた変更をキャンセルするかを新しく追加された行を破棄します。 呼び出した後は、現在の行または新しい行への変更を取り消すことはできません、**更新**メソッド、変更をロールバックできるトランザクションの一部である場合を除き、 **RollbackTrans**メソッドまたはの一部バッチ更新します。 バッチ更新を取り消すことができます、**更新**で、 **CancelUpdate**または**CancelBatch**メソッド。  
  
 呼び出すときに新しい行を追加するかどうか、 **CancelUpdate**メソッド、現在の行が前に、の現在の行、 **AddNew**呼び出します。  
  
 呼び出して、現在の行が変更されていないか、新しい行を追加するが場合、 **CancelUpdate**メソッドはエラーを生成します。
