---
title: CommandTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a2de155d9c4a61246245b2c7f9c3c73a535994a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919682"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
コマンド引数を解釈する方法を指定します。  
  
 ユーザーが指定したかを検証することが重要*クラスヒント*アプリケーション ユーザーに実行する ADO の危険性のあるコマンドを挿入する機会を提供しないようにする値。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|コマンドの型引数を指定しません。|  
|**adCmdText**|1|評価[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)コマンドまたはストアド プロシージャのテキストの定義として呼び出します。|  
|**adCmdTable**|2|評価**CommandText**をテーブル名を列の変更がすべて、内部的に生成された SQL クエリで返されます。|  
|**adCmdStoredProc**|4|評価**CommandText**としてストアド プロシージャの名前。|  
|**adCmdUnknown**|8|既定値です。 示しますコマンドの種類、 **CommandText**プロパティが不明です。<br /><br /> ADO で解釈するいくつかの試行は、コマンドの種類が不明の場合に、 **CommandText**します。<br /><br /> -   **CommandText**コマンドまたはストアド プロシージャの呼び出しのテキストの定義として解釈されます。 これと同じ動作**adCmdText**します。<br />-   **CommandText**ストアド プロシージャの名前を指定します。 これと同じ動作**adCmdStoredProc**します。<br />-   **CommandText**はテーブルの名前として解釈されます。 内部的に生成された SQL クエリでは、すべての列が返されます。 これと同じ動作**adCmdTable**します。|  
|**adCmdFile**|256|評価**CommandText**永続的にストアドのファイル名として[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。 併用**レコード セット**。[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)または[Requery](../../../ado/reference/ado-api/requery-method.md)のみです。|  
|**adCmdTableDirect**|512|評価**CommandText**をテーブル名を持つ列がすべて返されます。 併用**Recordset.Open**または**Requery**のみです。 使用する、[シーク](../../../ado/reference/ado-api/seek-method.md)メソッド、**レコード セット**で開く必要がある**adCmdTableDirect**します。<br /><br /> この値は組み合わせることができない、 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)値**adAsyncExecute**します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[CommandType プロパティ (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Execute メソッド (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute メソッド (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery メソッド](../../../ado/reference/ado-api/requery-method.md)||
