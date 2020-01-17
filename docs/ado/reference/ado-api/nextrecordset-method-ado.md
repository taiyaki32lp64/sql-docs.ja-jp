---
title: NextRecordset メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c7af4f5d217670ab23e71a3c53ccd5cf7944b0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932035"
---
# <a name="nextrecordset-method-ado"></a>NextRecordset メソッド (ADO)
現在のクリア[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトし、[次へ] を返します**レコード セット**一連のコマンドを進めることで。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>戻り値  
 返します、 **Recordset**オブジェクト。 モデルでは、構文、 *recordset1*と*recordset2*は、同じ**レコード セット**オブジェクト、またはするには、別のオブジェクトを使用できます。 個別を使用する場合**Recordset**オブジェクト、リセット、 **ActiveConnection**元のプロパティ**レコード セット**(*recordset1*)後**NextRecordset**が呼び出されてはエラーを生成します。  
  
#### <a name="parameters"></a>パラメーター  
 *RecordsAffected*  
 任意。 A**長い**変数を現在の操作の影響を受けるレコードの数はプロバイダーに返されます。  
  
> [!NOTE]
>  このパラメーターは、操作が影響を受けたレコードの数のみを返しますレコードの数を生成するために使用する select ステートメントから返されません、 **Recordset**します。  
  
## <a name="remarks"></a>コメント  
 使用して、 **NextRecordset**複合コマンド ステートメントでは、次のコマンドのまたは複数の結果を返すストアド プロシージャの結果を返すメソッド。 開く場合、**レコード セット**オブジェクトに基づく複合コマンド ステートメント (たとえば、"選択\*table1; からSELECT \* TABLE2") を使用して、 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)メソッドを[コマンド](../../../ado/reference/ado-api/command-object-ado.md)または[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドを**レコード セット**、ADO は、最初のコマンドのみを実行しに結果が返されます*recordset*します。 ステートメント内の後続のコマンドの結果にアクセスするには、呼び出し、 **NextRecordset**メソッド。  
  
 その他の結果がある限り、**レコード セット**しない切断またはプロセスの境界を越えてマーシャ リング複合ステートメントを含む、 **NextRecordset**メソッドは引き続き返す**Recordset**オブジェクト。 行を返すコマンドが正常に実行されますが、返されるレコードは返されません**Recordset**オブジェクトが開いているが、空になります。 テストのことを確認して、この場合、 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)と[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)プロパティが両方とも**True**します。 かどうか、行を返すコマンドが正常に実行、返された**レコード セット**オブジェクトは閉じて、これをテストして確認できます、[状態](../../../ado/reference/ado-api/state-property-ado.md)プロパティを**Recordset**. 以外の結果がある場合に*レコード セット*に設定されます*Nothing*します。  
  
 **NextRecordset**メソッドは接続が切断されたで使用できません**レコード セット**オブジェクト、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)に設定されている**Nothing**(Microsoft Visual Basic で)、または NULL (その他の言語) にします。  
  
 編集が即時更新モードで実行中の場合は、呼び出し、 **NextRecordset**メソッドにはエラーが生成されます。 呼び出し、[更新](../../../ado/reference/ado-api/update-method.md)または[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)メソッド最初。  
  
 複合ステートメントで情報を入力して 1 つ以上のコマンドのパラメーターを渡す、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクション、または元の配列を渡すことによって**オープン**または**Execute**呼び出し、パラメーターは、コマンドのシリーズで、それぞれのコマンドと同じ順序で、コレクションまたは配列でなければなりません。 出力パラメーターの値を読み取る前にすべての結果を読み取りが完了する必要があります。  
  
 複合ステートメント内の各コマンドを実行すると、OLE DB プロバイダーを決定します。 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)、たとえば、複合ステートメントを受信すると、バッチ内のすべてのコマンドを実行します。 その結果、**レコード セット**を呼び出すときに返されるだけ**NextRecordset**します。  
  
 ただし、他のプロバイダーがコマンドを実行 [次へ] ステートメントで NextRecordset が呼び出された後にのみです。 これらのプロバイダーでは、明示的に閉じる場合、 **Recordset**コマンド全体のステートメントをステップ実行する前にオブジェクトの残りのコマンドは実行されません。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [NextRecordset メソッドの例 (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset メソッドの例 (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
