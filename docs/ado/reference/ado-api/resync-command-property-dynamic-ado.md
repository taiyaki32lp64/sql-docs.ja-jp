---
title: Resync Command プロパティ-動的 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e81fa9ffb28ba31f50d77cacf372bc24d09787ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917144"
---
# <a name="resync-command-property-dynamic-ado"></a>Resync Command プロパティ - 動的 (ADO)
文字列をユーザーが指定したコマンドを指定します、[再同期](../../../ado/reference/ado-api/resync-method.md)でという名前のテーブルにデータを更新するメソッドの問題、[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動的プロパティ。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**コマンド文字列である値。  
  
## <a name="remarks"></a>コメント  
 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトが複数のベース テーブルで実行される結合操作の結果。 影響を受ける行によって異なります、 *AffectRecords*のパラメーター、[再同期](../../../ado/reference/ado-api/resync-method.md)メソッド。 標準**再同期**場合、メソッドが実行される、[一意テーブル](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)と**Resync Command**プロパティが設定されていません。  
  
 コマンド文字列、 **Resync Command**プロパティは、パラメーター化コマンドまたは更新される行を一意に識別するストアド プロシージャとする行として同じ数と列の順序を含む単一行を返します更新されます。 コマンド文字列には各主キー列のパラメーターが含まれています、**一意テーブル**。 そうしないと、実行時エラーが返されます。 パラメーターには、更新する行の主キーの値が自動的に入力します。  
  
 SQL ベースの 2 つの例を次に示します。  
  
 1\) 、 **Recordset**コマンドによって定義されます。  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 **Resync Command**プロパティに設定します。  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **一意テーブル**は*注文*とその主キーを*OrderID*、パラメーター化されます。 サブクエリの select では、プログラムで、同じ数と列の順序は、元のコマンドによって返されることを確認する簡単な方法を提供します。  
  
 2\) 、 **Recordset**ストアド プロシージャによって定義されます。  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **再同期**メソッドは、次のストアド プロシージャを実行する必要があります。  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 **Resync Command**プロパティに設定します。  
  
```  
"{call CustordersResync (?)}"  
```  
  
 もう一度、**一意テーブル**は*注文*とプライマリ キー、 *OrderID*がパラメーター化します。  
  
 **コマンドを再同期**に動的なプロパティが追加、**レコード セット**オブジェクト[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション時に、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) にプロパティを設定**adUseClient**します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
