---
title: 階層レコード セットの作成 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6fcdb630f2391f685080ac594cfdb537edf626a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925322"
---
# <a name="fabricating-hierarchical-recordsets"></a>階層レコードセットの作成
次の例は、データのシェイプの親、子、および孫の列を定義する文法を使用して、基になるデータ ソースのない階層レコード セットを作成する方法を示しています。**レコード セット**します。  
  
 階層構造を作成する**レコード セット**を指定する必要があります、 [OLE DB (ADO サービス プロバイダー) の Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (MSDataShape) なしでのデータ プロバイダーの値を指定して、接続文字列パラメーター、[オープン](../../../ado/reference/ado-api/open-method-ado-connection.md)のメソッド、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。 詳細については、次を参照してください。[データ シェイプに必要なプロバイダー](../../../ado/guide/data/required-providers-for-data-shaping.md)します。  
  
```  
Dim cn As New ADODB.Connection  
Dim rsCustomers As New ADODB.Recordset  
  
cn.Open "Provider=MSDataShape;Data Provider=NONE;"  
  
strShape = _  
"SHAPE APPEND NEW adInteger AS CustID," & _  
            " NEW adChar(25) AS FirstName," & _  
            " NEW adChar(25) AS LastName," & _  
            " NEW adChar(12) AS SSN," & _  
            " NEW adChar(50) AS Address," & _  
         " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                        " NEW adInteger AS CustID," & _  
                        " NEW adChar(20) AS BodyColor, " & _  
                     " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                                    " NEW adChar(20) AS Make, " & _  
                                    " NEW adChar(20) AS Model," & _  
                                    " NEW adChar(4) AS Year) " & _  
                        " AS VINS RELATE VIN_NO TO VIN_NO))" & _  
            " AS Vehicles RELATE CustID TO CustID) "  
  
rsCustomers.Open strShape, cn, adOpenStatic, adLockOptimistic, -1  
```  
  
 すぐに、 **Recordset**された作成、設定、操作、またはそのファイルに保存します。  
  
## <a name="see-also"></a>参照  
 [階層レコード セット内の行へのアクセス](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Shape の正式文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [データ シェイプに必要なプロバイダー](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape の APPEND 句](../../../ado/guide/data/shape-append-clause.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)
