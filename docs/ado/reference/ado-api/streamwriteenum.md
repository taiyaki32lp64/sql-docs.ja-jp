---
title: StreamWriteEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cc9de1481cc683bddafe2f92959977319600f6a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928632"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
書き込まれる文字列に行区切り記号を追加するかどうかを指定します、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|既定値です。 指定したテキスト文字列を書き込みます (で指定された、*データ*パラメーター) を**Stream**オブジェクト。|  
|**adWriteLine**|1|テキスト文字列と行区切り記号を書き込みます、 **Stream**オブジェクト。 場合、 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)プロパティが定義されていませんし、実行時エラーが返されます。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [WriteText メソッド](../../../ado/reference/ado-api/writetext-method.md)
