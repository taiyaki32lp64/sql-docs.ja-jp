---
title: ConnectPromptEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afd5d9ca0de6b8d2ffba75f862e6ca0afb594848
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919445"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
データ ソースへの接続を開くときに、不足しているパラメーターを要求する ダイアログ ボックスを表示するかどうかを指定します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|常にメッセージが表示されます。|  
|**adPromptComplete**|2|詳細については、必要な場合は、メッセージが表示されます。|  
|**adPromptCompleteRequired**|3|詳細についての情報が必要ですが、省略可能なパラメーターは使用できない場合のプロンプトを表示します。|  
|**adPromptNever**|4|要求しません。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>適用対象  
 [Prompt プロパティ - 動的 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
