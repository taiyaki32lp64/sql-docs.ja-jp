---
title: レコードへのジャンプ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cead84eed4e7689d6b5df907b6a61ef07ab74e8a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924934"
---
# <a name="jumping-to-a-record"></a>レコードへのジャンプ
[移動](../../../ado/reference/ado-api/move-method-ado.md)メソッドでは、前方または後方に移動することができます、**レコード セット**次の構文を使用してレコード数を指定します。  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>コメント  
 **移動**メソッドがすべてでサポートされている**Recordset**オブジェクト。  
  
 場合、 *NumRecords*引数に 0 を超えると、現在のレコードの位置を前方に移動 (の終了に向けて、 **Recordset**)。 場合*NumRecords* 0、現在のレコードの位置は後方に移動します未満です (の先頭に向かって、 **Recordset**)。  
  
 場合、**移動**呼び出しは最初のレコードの前に、現在のレコードの位置を移動するが、現在のレコードの最初のレコードの前に、の位置を設定、 **Recordset** (**BOF**は**True**)。 旧バージョンとのときに移動しよう、 **BOF**プロパティが既に**True**エラーが生成されます。  
  
 場合、**移動**呼び出しは最後のレコードの後のポイントに現在のレコードの位置を移動すると、ADO は、最後のレコードの後の位置に、現在のレコードを設定、 **Recordset** (**EOF**は**True**)。 転送時に移動しよう、 **EOF**プロパティが既に**True**エラーが生成されます。  
  
 呼び出す、**移動**メソッド空から**レコード セット**オブジェクト、エラーが発生します。  
  
 内のブックマークを渡した場合、*開始*レコード、このブックマークを基準とした引数では、この移動と仮定すると、**レコード セット**オブジェクトは、ブックマークをサポートしています。 ブックマークを使用して取得されます、[ブックマーク](../../../ado/reference/ado-api/bookmark-property-ado.md)プロパティ。 指定しない場合、この移動は現在のレコードを基準とは。  
  
 使用する場合、 **CacheSize**渡す、プロバイダーからのレコードをローカルにキャッシュするプロパティを*NumRecords*引数キャッシュされたレコードの現在のグループの外側、現在のレコードの位置を移動します。強制的に目的のレコードからレコードの新しいグループを取得します。 **CacheSize**プロパティは、新たに取得したグループのサイズを決定し、目的のレコードが最初のレコードを取得します。
