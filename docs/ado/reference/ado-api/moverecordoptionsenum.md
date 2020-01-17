---
title: MoveRecordOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcdb825073b267c3e3351001ecc7b11c969582e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932044"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
動作を指定します、[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクト[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)メソッド。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|既定値です。 既定の移動操作を実行します。変換先ファイルまたはディレクトリが既に存在して、操作は、ハイパー テキスト リンクを更新する場合、操作は失敗します。|  
|**adMoveOverWrite**|1|既に存在する場合でも、変換先ファイルまたはディレクトリを上書きします。|  
|**adMoveDontUpdateLinks**|2|既定の動作を変更します。 **MoveRecord**更新されないため、ソースのハイパー テキスト リンク メソッド**レコード**します。 既定の動作は、プロバイダーの機能に依存します。 移動操作は、プロバイダーができる場合は、リンクを更新します。 プロバイダーへのリンクを解決できない場合、またはこの値が指定されていない場合は、移動が成功でもときのリンクが解決されていません。|  
|**adMoveAllowEmulation**|4|(ダウンロード、アップロード、および削除操作を使用して)、移動をシミュレートするために、プロバイダーを試みることを要求します。 場合に移動しようと、**レコード**送信先 URL とは別のサーバー上か、異なるソース プロバイダーによって処理される、これが原因で別のプロバイダーの機能により、増加の待機時間やデータ損失が失敗したときプロバイダー間でリソースを移動します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。  
  
## <a name="applies-to"></a>適用対象  
 [MoveRecord メソッド (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
