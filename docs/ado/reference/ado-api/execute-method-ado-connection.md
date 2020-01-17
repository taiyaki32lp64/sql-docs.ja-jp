---
title: Execute メソッド (ADO Connection) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4999b1e21ec145713cadae28ff7ee8a64dd460b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932892"
---
# <a name="execute-method-ado-connection"></a>Execute メソッド (ADO Connection)
指定されたクエリ、SQL ステートメント、ストアド プロシージャ、またはプロバイダー固有のテキストを実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>戻り値  
 返します、[レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト参照。  
  
#### <a name="parameters"></a>パラメーター  
 *CommandText*  
 A**文字列**値を含む SQL ステートメント、ストアド プロシージャ、URL、またはプロバイダー固有のテキストを実行します。 **必要に応じて**テーブル名は、プロバイダーが SQL 対応である場合にのみ使用できます。 「顧客」の場合、テーブル名の例を使用すると、ADO は自動的に先頭に追加を形成し、"SELECT * FROM Customers"を渡す標準の SQL Select 構文として、[!INCLUDE[tsql](../../../includes/tsql-md.md)]プロバイダーにステートメント。  
  
 *RecordsAffected*  
 任意。 A**長い**変数を操作の影響を受けるレコードの数はプロバイダーに返されます。  
  
 *[オプション]*  
 任意。 A**長い**プロバイダーが CommandText 引数を評価する方法を示す値です。 1 つ以上のビットマスクを指定できます[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)または[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)値。  
  
 **注**使用、 **ExecuteOptionEnum**値**adExecuteNoRecords**内部処理を最小限に抑えることで、Visual Basic 6.0 から移植するアプリケーションのパフォーマンスを向上させる。  
  
 使用しない**adExecuteStream**で、 **Execute**のメソッド、**接続**オブジェクト。  
  
 Execute を使用 adCmdFile または adCmdTableDirect CommandTypeEnum 値を使わないでください。 これらの値は、オプションとしてのみ使用できます、 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)と[Requery メソッド](../../../ado/reference/ado-api/requery-method.md)のメソッド、 **Recordset**します。  
  
## <a name="remarks"></a>コメント  
 使用して、 **Execute**メソッドを[接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトは、指定した接続で CommandText 引数でメソッドに渡す任意のクエリを実行します。 新しい実行によって生成される結果を格納 CommandText 引数は、行を返すクエリを指定する場合**Recordset**オブジェクト。 プロバイダーが返すかどうか、コマンドを (たとえば、SQL UPDATE クエリ) の結果を返すことはありません**Nothing**オプション限り**adExecuteNoRecords**が指定されて; 実行それ以外の場合、閉じられた**Recordset**します。  
  
 返された**Recordset**オブジェクトが読み取り専用、順方向専用カーソルでは常にします。 必要がある場合、 **Recordset**オブジェクトの多くの機能では、まず作成、**レコード セット**必要なプロパティの設定を持つオブジェクトを使用して、**レコード セット**オブジェクト[Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)をクエリを実行し、目的のカーソルの種類を返すメソッド。  
  
 内容、 *CommandText*引数は、プロバイダーに固有と標準の SQL 構文またはプロバイダーがサポートする任意の特殊なコマンド形式を指定できます。  
  
 ExecuteComplete イベントは、この操作の終了時に発行されます。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
