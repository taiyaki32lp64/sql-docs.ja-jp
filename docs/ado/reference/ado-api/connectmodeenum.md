---
title: ConnectModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: debf6f9dc4ac1326caf9fbf32b65f15f34a19094
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933458"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
データを変更する使用可能なアクセス許可を指定します、[接続](../../../ado/reference/ado-api/connection-object-ado.md)を開いて、[レコード](../../../ado/reference/ado-api/record-object-ado.md)の値を指定するか、[モード](../../../ado/reference/ado-api/mode-property-ado.md)のプロパティ、 **レコード**と[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|読み取り専用アクセス許可を示します。|  
|**adModeReadWrite**|3|読み取り/書き込みアクセス許可を示します。|  
|**adModeRecursive**|0x400000|他と組み合わせて使用 *\*ShareDeny\** 値 (**adModeShareDenyNone**、 **adModeShareDenyWrite**、または**adModeShareDenyRead**)、現在のすべてのサブ レコードに共有の制限が反映されるまでに**レコード**します。 これは、影響を与えません場合、**レコード**子はありません。 使用した場合、実行時エラーが生成される**adModeShareDenyNone**のみです。 ただしで使用する**adModeShareDenyNone**他の値と組み合わせたときにします。 たとえば、使用することができます"**adModeRead**または**adModeShareDenyNone**または**adModeRecursive**"。|  
|**adModeShareDenyNone**|16|すべてのアクセス許可を持つ接続を開く他のユーザーを使用できます。 他のユーザーに対して、読み取りアクセスも書き込みアクセスも拒否できません。|  
|**adModeShareDenyRead**|4|読み取りアクセス許可で接続を開くには、他のユーザーを禁止します。|  
|**adModeShareDenyWrite**|8|書き込みアクセス許可を持つ接続を開くには、他のユーザーを禁止します。|  
|**adModeShareExclusive**|12|接続を開くには、他のユーザーを禁止します。|  
|**adModeUnknown**|0|既定値です。 アクセス許可がまだ設定されていないか、特定できないことを示します。|  
|**adModeWrite**|2|書き込み専用のアクセス許可を示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|(AdoEnums.ConnectMode.RECURSIVE の相当するものはありません)|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums.ConnectMode.UNKNOWN|  
|AdoEnums.ConnectMode.WRITE|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Mode プロパティ (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
