---
title: Execute メソッド (ADO Command) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ef42c04944f39e0b2d1930cc6520df2b6c5fa5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918856"
---
# <a name="execute-method-ado-command"></a>Execute メソッド (ADO Command)
クエリや、SQL ステートメントで指定されたストアド プロシージャの実行、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)または[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)のプロパティ、[コマンド オブジェクト](../../../ado/reference/ado-api/command-object-ado.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>戻り値  
 返します、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト参照をストリームまたは**Nothing**します。  
  
#### <a name="parameters"></a>パラメーター  
 *RecordsAffected*  
 任意。 A**長い**変数を操作の影響を受けるレコードの数はプロバイダーに返されます。 *RecordsAffected*パラメーターはアクションのクエリまたはストアド プロシージャに対してのみ適用されます。 *RecordsAffected*結果を返すクエリまたはストアド プロシージャによって返されるレコードの数は返されません。 この情報を入手するには使用、 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)プロパティ。 **Execute**メソッドで使用する場合は、正しい情報が返されません**adAsyncExecute**、単にときにコマンドが非同期的に実行された、ため、影響を受けたレコードの数がまだが認識されていません。時にメソッドを返します。  
  
 *パラメーター*  
 任意。 A**バリアント**で指定されたストリーム、入力文字列と組み合わせて使用するパラメーター値の配列**CommandText**または**CommandStream**します。 (出力パラメーターは、この引数で渡されるときに正しい値を返しますがありません)。  
  
 *[オプション]*  
 任意。 A**長い**プロバイダーを評価する方法を示す値、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)または[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)のプロパティ、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。 指定できる値のビットマスクを使用して確立[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)や[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)値。 たとえば、使用する**adCmdText**と**adExecuteNoRecords** ado の値を評価する場合の組み合わせで、 **CommandText**プロパティとして、テキストと示しますのコマンドは、する必要がありますを破棄し、コマンド テキストの実行時に生成されるレコードは返されません。  
  
> [!NOTE]
>  使用して、 **ExecuteOptionEnum**値**adExecuteNoRecords**内部処理を最小限に抑えることでパフォーマンスを向上させるためにします。 場合**adExecuteStream**が指定されているオプション**adAsyncFetch**と**adAsynchFetchNonBlocking**は無視されます。 使用しないでください、 **CommandTypeEnum**値**adCmdFile**または**adCmdTableDirect**で**Execute**します。 これらの値は、オプションとしてのみ使用できます、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)と[Requery](../../../ado/reference/ado-api/requery-method.md)のメソッド、**レコード セット**します。  
  
## <a name="remarks"></a>コメント  
 使用して、 **Execute**メソッドを**コマンド**オブジェクトで指定されたクエリの実行、 **CommandText**プロパティまたは**CommandStream**オブジェクトのプロパティです。  
  
 結果が返されます、 **Recordset** (既定) またはバイナリ情報のストリームとして。 バイナリ ストリームを取得するには、次のように指定します。 **adExecuteStream**で*オプション*、設定してストリームを指定し、 **Command.Properties ("出力 Stream")** します。 ADO **Stream**結果を受信するオブジェクトを指定するか、IIS の応答オブジェクトなどの別のストリーム オブジェクトを指定することができます。 呼び出しの前にストリームが指定されなかった場合**Execute**で**adExecuteStream**エラーが発生します。 返された場合、ストリームの位置**Execute**がプロバイダーを特定します。  
  
 プロバイダーが返すかどうか、コマンドを (たとえば、SQL UPDATE クエリ) の結果を返すことはありません**Nothing**オプション限り**adExecuteNoRecords**が指定されて; 実行それ以外の場合、閉じられた**Recordset**します。 ない場合は、この戻り値を無視することはいくつかのアプリケーション言語**レコード セット**が必要です。  
  
 **実行**、ユーザーの値を指定する場合、エラーが発生**CommandStream**ときに、 **CommandType**は**adCmdStoredProc**、 **adCmdTable**、または**adCmdTableDirect**します。  
  
 現在の値、クエリにパラメーターがある場合、**コマンド**オブジェクトのパラメーターには、これらに渡されたパラメーター値を上書きしない限り、使用、 **Execute**を呼び出します。 呼び出すときに、一部のパラメーターの新しい値を省略することで、パラメーターのサブセットをオーバーライドすることができます、 **Execute**メソッド。 パラメーターを指定する順序は、メソッドがそれらに渡すと同じ順序です。 たとえば、4 つ (以上) のパラメーターが、1 番目と 4 番目のパラメーターのみの新しい値を渡すに渡す場合`Array(var1,,,var4)`として、*パラメーター*引数。  
  
> [!NOTE]
>  出力パラメーターで渡されるときに正しい値を返しません、*パラメーター*引数。  
  
 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)この操作の終了時にイベントが発行されます。  
  
> [!NOTE]
>  自動的に起動は、http スキームを使用する Url を含むコマンドを発行するときに、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Execute、Requery、および Clear のメソッドの例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery、および Clear のメソッドの例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery、および Clear のメソッドの例 (vc++)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream プロパティ (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText プロパティ (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute メソッド (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete イベント (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
