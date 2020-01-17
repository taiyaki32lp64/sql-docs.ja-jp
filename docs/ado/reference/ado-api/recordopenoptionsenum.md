---
title: RecordOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba165d51dde5224dac65467061eac0d38aeefc7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931424"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
開くのためのオプションを指定します、[レコード](../../../ado/reference/ado-api/record-object-ado.md)します。 使用して、これらの値を組み合わせることができますか。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|フィールドに関連付けられているプロバイダーに示します、**レコード**最初に、取得する必要がありませんが、フィールドにアクセスする最初の試行で取得できます。 ない場合、このフラグで示される、既定の動作がすべて取得するには、**レコード**フィールド オブジェクトします。|  
|**adDelayFetchStream**|0x4000|既定のストリームに関連付けられているプロバイダーに示します、**レコード**最初に取得する必要がありません。 関連付けられている既定のストリームを取得するがない場合、このフラグで示された既定の動作は、**レコード**オブジェクト。|  
|**adOpenAsync**|0x1000|示します、**レコード**オブジェクトは非同期モードで開きます。|  
|**adOpenExecuteCommand**|0x10000|ソース文字列が実行されるコマンド テキストが含まれていることを示します。 この値は、 **adCmdText**オプション**Recordset.Open**します。|  
|**adOpenRecordUnspecified**|-1|既定値です。 オプションが指定されていないことを示します。|  
|**adOpenOutput**|0x800000|ソースは、実行可能スクリプトを含むノードを指している場合は、ことを示します (など、します。ASP ページの場合)、開かれた**レコード**実行されたスクリプトの結果が含まれます。 この値はコレクションではないレコードのみです。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
