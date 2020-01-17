---
title: ExecuteOptionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bef70bd72425e749865e31ecf162e719737dd272
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932844"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
プロバイダーがコマンドを実行する方法を指定します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|コマンドを非同期的に実行することを示します。<br /><br /> この値は組み合わせることができない、 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)値**adCmdTableDirect**します。|  
|**adAsyncFetch**|0x20|残りの行を後で指定した初期量を示します、 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)プロパティを非同期的に取得する必要があります。|  
|**adAsyncFetchNonBlocking**|0x40|取得中にメイン スレッドがブロックされないことを示します。 要求された行が取得されていない、現在の行が自動的にファイルの末尾に移動します。<br /><br /> 開く場合、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)から、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)永続的に保存を含む**レコード セット**、 **adAsyncFetchNonBlocking**必要はありません効果。操作は、ブロックして同期されます。<br /><br /> **adAsynchFetchNonBlocking**にない場合は影響、 [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md)オプションを使用して開く、**レコード セット**。|  
|**adExecuteNoRecords**|0x80|コマンド テキストがコマンドまたは行 (データの挿入のみコマンドなど) を返さないストアド プロシージャであることを示します。 すべての行が取得される場合は破棄されていては返されません。<br /><br /> **adExecuteNoRecords**のみを任意のパラメーターとして渡すことができます、**コマンド**または**接続実行**メソッド。|  
|**adExecuteStream**|0x400|コマンドの実行結果をストリームとして返すことを示します。<br /><br /> **adExecuteStream**のみを任意のパラメーターとして渡すことができます、 **Command Execute**メソッド。|  
|**adExecuteRecord**||示します、 **CommandText**コマンドまたはストアド プロシージャを返す 1 つの行として返される必要がありますが、**レコード**オブジェクト。|  
|**adOptionUnspecified**|-1|コマンドが指定されていないことを示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Execute メソッド (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute メソッド (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery メソッド](../../../ado/reference/ado-api/requery-method.md)|
