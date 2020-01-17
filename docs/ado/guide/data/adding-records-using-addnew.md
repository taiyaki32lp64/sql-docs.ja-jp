---
title: AddNew を使用してレコードを追加する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f6bad9a8f0d74a81d02ce64c78d7a91ddc0fa8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926283"
---
# <a name="adding-records-using-addnew-method"></a>AddNew メソッドを使用してレコードを追加します。
基本的な構文は、 **AddNew**メソッド。

 *レコード セット*します。AddNew *FieldList*、*値*

 *FieldList*と*値*引数は省略可能です。 *FieldList*単一の名前または名前の配列または新しいレコードのフィールドの序数位置のいずれかです。

 *値*引数が 1 つの値または新しいレコードのフィールドの値の配列。

 通常、1 つのレコードを追加する場合にを呼び出す、 **AddNew**メソッドを引数なし。 具体的を呼び出す**AddNew**; 設定、**値**の各フィールドに新しいレコードを呼び出して**Update**または**UpdateBatch**、または両方とも。 できること確認する、**レコード セット**を使用して新しいレコードの追加をサポートしています、**サポート**プロパティを**adAddNew**列挙型定数。

 次のコードでは、この手法を使用して、サンプルを新しい配送会社を追加する**Recordset**します。 SQL Server では、運送フィールドの値を自動的に提供します。 したがって、コードは、新しいレコードのフィールド値を指定するは試行されません。

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>コメント
 このコードを使用して接続が切断されたため**レコード セット**バッチ モードでクライアント側カーソルでは、再接続する必要があります、 **Recordset**を新しいデータ ソースに**接続**オブジェクトを呼び出すには、 **UpdateBatch**データベースへの変更を投稿するメソッド。 新しい関数を使用して、これは、簡単に**GetNewConnection**します。
