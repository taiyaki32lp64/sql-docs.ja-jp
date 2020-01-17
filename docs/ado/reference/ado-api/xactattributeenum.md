---
title: XactAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d828c2b9b49138cc4dfd6345d90e70c333554fe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947430"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
トランザクション属性を指定します、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|保持中止を呼び出して実行[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)を自動的に新しいトランザクションを開始します。 一部のプロバイダーは、この動作をサポートします。|  
|**adXactCommitRetaining**|131072|保持コミットを呼び出すことによって実行[CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)を自動的に新しいトランザクションを開始します。 一部のプロバイダーは、この動作をサポートします。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>適用対象  
 [Attributes プロパティ (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
