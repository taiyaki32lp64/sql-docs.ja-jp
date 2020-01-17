---
title: Delete メソッドを使用してレコードを削除する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a862a244f06c64767f41529b4fff36881895a0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925554"
---
# <a name="deleting-records-using-the-delete-method"></a>Delete メソッドを使用してレコードを削除する
使用して、**削除**メソッドは、現在のレコードまたはレコードのグループを示します、 **Recordset**オブジェクトを削除します。 場合、 **Recordset**オブジェクトは、レコードの削除を許可しないため、エラーが発生します。 即時更新モードの場合は、削除はすぐに、データベースで発生します。 呼び出しの後に、レコードが編集モードのままは場合 (たとえば、データベース整合性違反) のため、レコードを正常に削除することはできません、**更新します。** つまりを使用して更新をキャンセルする必要があります[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)現在のレコードから移動する前に (たとえばを使用して[閉じる](../../../ado/reference/ado-api/close-method-ado.md)、[移動](../../../ado/reference/ado-api/move-method-ado.md)、または[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 バッチ更新モードの場合は、レコードがキャッシュからの削除とマークされてし、実際の削除の動作を呼び出すとき、 **UpdateBatch**メソッド。 (削除されたレコードを表示するには、設定、**フィルター**プロパティを**adFilterAffectedRecords**後**削除**が呼び出されます)。  
  
 削除されたレコードからフィールドの値を取得しようとすると、エラーが生成されます。 現在のレコードを削除すると、削除されたレコードを別のレコードに移動するまで最新の状態します。 移動すると、削除されたレコードはアクセスできません。  
  
 使用して削除されたレコードを回復するには、トランザクションで削除を入れ子にする場合、 **RollbackTrans**メソッド。 バッチ更新モードでは、取り消すことができます、保留中の削除または保留中の削除のグループを使用して、 **CancelBatch**メソッド。  
  
 基になるデータとの競合レコードを削除する試行が失敗した場合 (たとえば、レコードが別のユーザーが既に削除されている場合)、プロバイダーに警告を返し、**エラー**コレクション プログラムは停止されませんが、実行します。 要求されたすべてのレコードの競合がある場合にのみ、実行時エラーが発生します。  
  
 場合、**一意テーブル**動的プロパティの設定と**レコード セット**は複数のテーブルに対して結合操作を実行した結果、**削除**メソッド行のみが削除されます指定したテーブルから、**一意テーブル**プロパティ。  
  
 **削除**メソッドは対象となるレコードを指定することができます、省略可能な引数、**削除**操作。 この引数の唯一の有効な値は、次の ADO のいずれかの**AffectEnum**列挙定数。  
  
-   **adAffectCurrent**現在のレコードのみに影響を与えます。  
  
-   **adAffectGroup**現在に適合するレコードのみに影響を与えます**フィルター**プロパティの設定。 **フィルター**にプロパティを設定する必要があります、 **FilterGroupEnum**値または配列の**ブックマーク**このオプションを使用します。  
  
 次のコードは、指定する例を示しています。 **adAffectGroup**を呼び出すときに、**削除**メソッド。 この例では、レコードの一部をサンプルに追加**Recordset**し、データベースを更新します。 フィルター処理し、**レコード セット**を使用して、 **adFilterAffectedRecords**新しく追加されたレコードだけをそのままで表示フィルター列挙型定数、**レコード セット。** 最後に、呼び出し、**削除**メソッドことを指定してすべてのレコードを現在を満たす**フィルター**プロパティの設定 (新しいレコード) を削除する必要があります。  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```
