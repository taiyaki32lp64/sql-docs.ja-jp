---
title: 失敗した更新プログラムを扱う |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d442a9c397ad184658f9101343e139697c9b3756
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925634"
---
# <a name="dealing-with-failed-updates"></a>失敗した更新の処理
更新プログラムは、エラーの終了時に、種類と、エラーの重大度、およびアプリケーションのロジックに依存、エラーを解決する方法。 ただし、データベースは、他のユーザーと共有される場合、一般的なエラーは実行する前に、フィールドを変更他のユーザー。 この種のエラーは、競合と呼ばれます。 ADO では、このような状況を検出し、エラーを報告します。  
  
## <a name="remarks"></a>コメント  
 更新エラーがある場合は、エラー処理ルーチンにトラップされます。 競合する行のみが表示されるように、競合の定数を持つレコード セットをフィルター処理します。 この例で、エラーの解決方法は単なる作成者の印刷 (au_fname および au_lname) は、最初と最後の名前。  
  
 更新の競合をユーザーにアラートを生成するコードは、次のようになります。  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>関連項目  
 [バッチ モード](../../../ado/guide/data/batch-mode.md)
