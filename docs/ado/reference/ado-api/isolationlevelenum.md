---
title: IsolationLevelEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15ae2aac2851c496b6cac9e47d37fe5fa26b8e34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918370"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
トランザクションの分離のレベルを指定します、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|プロバイダーを使用している別の分離レベルを指定するよりも、レベルを特定できないことを示します。|  
|**adXactChaos**|16|保留中のより高度な分離レベルのトランザクションから変更できません上書きされることを示します。|  
|**adXactBrowse**|256|1 つのトランザクションからできますを表示するコミットされていない変更の他のトランザクションを示します。|  
|**adXactReadUncommitted**|256|同じ**adXactBrowse**します。|  
|**adXactCursorStability**|4096|1 つのトランザクションからことができますを表示する変更の他のトランザクションでコミットされた後にのみを示します。|  
|**adXactReadCommitted**|4096|同じ**adXactCursorStability**します。|  
|**adXactRepeatableRead**|65536|1 つのトランザクションから他のトランザクションで行われた変更を表示できませんが、新しいを取得するクエリを再実行できることを示します**Recordset**オブジェクト。|  
|**adXactIsolated**|1048576|他のトランザクションの分離でトランザクションが実行されたことを示します。|  
|**adXactSerializable**|1048576|同じ**adXactIsolated**します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>適用対象  
 [IsolationLevel プロパティ](../../../ado/reference/ado-api/isolationlevel-property.md)
