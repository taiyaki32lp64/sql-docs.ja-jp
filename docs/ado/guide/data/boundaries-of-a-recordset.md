---
title: レコード セットの境界 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f4efddad1b55ce57c62ce52418539ec06599bb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925910"
---
# <a name="boundaries-of-a-recordset"></a>レコードセットの境界
**レコード セット**サポート、 **BOF**と**EOF**プロパティに、データセットの先頭と末尾をそれぞれ含めます。 考えることができます**BOF**と**EOF**先頭と末尾の位置「ファントム」のレコードとして、 **Recordset**します。 カウント**BOF**と**EOF**、サンプル**レコード セット**ようになりますようになりました。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|おじさん Bob の有機的な乾燥なし|30.0000|  
|14|階層|23.2500|  
|28|Rssle ザワークラウト|45.6000|  
|51|りんご|53.0000|  
|74|Longlife 階層|10.0000|  
|EOF|||  
  
 過去の最後のレコードでは、カーソルが移動したときに**EOF**に設定されている**True**。 それ以外の値は**False**します。 カーソルが最初のレコードの前に移動したときに同様に、 **BOF**に設定されている**True**。 それ以外の値は**False**します。 これらのプロパティは、JScript コードを次に示すように、データセット内のレコードを列挙するためによく使用します。  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 両方**BOF**と**EOF**は**True**、**レコード セット**オブジェクトは空です。 両方のプロパティになります**False**新しく開かれたが、空でないため**Recordset**オブジェクト。 使用することができます、 **BOF**と**EOF**プロパティかどうかをまとめて、**レコード セット**オブジェクトが空か、次の JScript コード フラグメントに示すとして。  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 このスキームでは、すべての種類のカーソル動作し、は、基になるプロバイダーに依存しません。 空かどうかを判断しようとした場合、**レコード セット**オブジェクトをチェックすることでその**RecordCount**プロパティの値がゼロ (0) か、適切なカーソルとプロバイダーを使用する際に対策を行う必要がありますが結果内のレコードの数を返すをサポートします。  
  
 最後の残りのレコードを削除する場合、 **Recordset**オブジェクト、カーソルが不確定な状態のままにします。 **BOF**と**EOF**プロパティが残る可能性がある**False**現在のレコードの位置を変更しようとするまでは、プロバイダーによって異なります。 詳細については、次を参照してください。 [Delete メソッドを使用して削除すると、レコード](../../../ado/guide/data/deleting-records-using-the-delete-method.md)します。
