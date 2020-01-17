---
title: SaveOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 807a8d7e5757a2caf76f100a1ae51c4a8a3f4e98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931144"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
ファイルを作成または上書きを保存するときにするかどうかを指定します、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。 値は、 **adSaveCreateNotExist**または**adSaveCreateOverWrite**.  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|既定値です。 によって、ファイルが指定されている場合は、新しいファイルを作成、 *FileName*パラメーターが存在しません。|  
|**adSaveCreateOverWrite**|2|データを現在開いているファイルが上書きされます**Stream**によってファイルが指定されている場合、オブジェクト、 *Filename*パラメーターは既に存在します。 によって、ファイルが指定されている場合、 *Filename*パラメーターが存在しないか、新しいファイルが作成されます。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [SaveToFile メソッド](../../../ado/reference/ado-api/savetofile-method.md)
