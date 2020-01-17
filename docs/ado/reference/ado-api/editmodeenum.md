---
title: EditModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c4ddb27bbc6831095062af5491fb501b6d5b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933044"
---
# <a name="editmodeenum"></a>EditModeEnum
レコードの編集状態を指定します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|進行中の編集操作がないことを示します。|  
|**adEditInProgress**|1|現在のレコード内のデータが変更されたが、保存されないことを示します。|  
|**adEditAdd**|2|示します、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)メソッドが呼び出されたれ、コピー バッファーの現在のレコードが新しいレコードがデータベースに保存されていないでします。|  
|**adEditDelete**|4|現在のレコードが削除されたことを示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>適用対象  
 [EditMode プロパティ](../../../ado/reference/ado-api/editmode-property.md)
