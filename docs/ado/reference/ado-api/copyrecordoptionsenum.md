---
title: CopyRecordOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6692125b7323bedc7a416e51555c373ef850ce0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919379"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
動作を指定します、 [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)メソッド。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|示します、*ソース*プロバイダーによりダウンロードを使用してコピーをシミュレートし、アップロード操作のために、このメソッドが失敗した場合*先*別のサーバー上または異なるによって処理されますプロバイダーよりも*ソース*します。 プロバイダーの機能のさまざまなパフォーマンスが低下したりデータが失われることに注意してください。|  
|**adCopyNonRecursive**|2|現在のディレクトリは、そのサブディレクトリの先にコピーします。 コピー操作は、再帰ではありません。|  
|**adCopyOverWrite**|1|場合、ファイルまたはディレクトリの上書き、*先*既存のファイルまたはディレクトリを指します。|  
|**adCopyUnspecified**|-1|既定値です。 既定のコピー操作を実行します。変換先ファイルまたはディレクトリが既に存在する場合、操作は失敗し、操作のコピーは再帰的にします。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [CopyRecord メソッド (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
