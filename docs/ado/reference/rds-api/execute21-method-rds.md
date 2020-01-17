---
title: Execute21 メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8434345dcc4436865e4981a19ef1164d35a852f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964204"
---
# <a name="execute21-method-rds"></a>Execute21 メソッド (RDS)
要求を実行し、ADO 2.1 で使用する ADO レコード セットを作成します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ConnectionString*  
 実行の要求を送信する先の OLE DB プロバイダーへの接続に使用する文字列。 使用して、ハンドラーが指定されている場合*HandlerString*、編集、接続文字列に置き換えます。  
  
 *HandlerString*  
 文字列は、この実行で使用するハンドラーを識別します。 文字列には、2 つの部分が含まれています。 最初の部分には、使用するハンドラーの名前 (ProgID) が含まれています。 文字列の 2 番目の部分には、ハンドラーに渡される引数が含まれています。 特定のハンドラーには、引数文字列を解釈する方法です。 2 つの部分は、(ただし、引数文字列には、追加のコンマを含めることができます)、コンマ、文字列内の最初のインスタンスで区切られます。 引数は省略可能です。  
  
 *QueryString*  
 接続文字列で識別される OLE DB プロバイダーでサポートされているコマンド言語でのコマンド。 SQL ベースのプロバイダーでは、含まれる、[!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントでは、コマンドしますが、非 SQL プロバイダー (たとえば、MSDataShape) のこのできない可能性があります、[!INCLUDE[tsql](../../../includes/tsql-md.md)]クエリ ステートメント。  
  
 また、ハンドラーが使用されている (およびハンドラーを使用することを強くお勧め) 場合、ハンドラーできます alter またはここで指定した値を置き換えます。 ハンドラーが通常置換など*QueryString* .ini ファイルからクエリ文字列を使用します。 既定では、Msdfmap.ini ファイルが使用されます。  
  
 *lMarshalOptions*  
 返される行セットとレコード セットでマーシャ リング オプションを設定するために使用します。  
  
 *TableID*  
 バリアントは、VT_EMPTY または VT_BSTR のいずれかを入力します。 この値が VT_EMPTY 型の場合は無視されます。 使用して、レコード セットが作成された VT_BSTR 型の場合、 **adCmdTableDirect**ここで指定された値を使用して、 *QueryString*パラメーターは無視されます。  
  
 *lExecuteOptions*  
 実行オプションのビットマスクを指定します。  
  
 1 =*ReadOnly* 、レコード セットを使用して開いたは**adLockReadOnly**します。  
  
 2 =*NoBatch* 、レコード セットを使用して開いたは**adLockOptimistic**します。  
  
 4 =*AllParamInfoSupplied* 、呼び出し元のすべてのパラメーターのパラメーター情報を提供することを保証*pParameters*します。  
  
 8 =*GetInfo* 、クエリのパラメーター情報が、OLE DB プロバイダーから取得しで返される、 *pParameters*パラメーター。 クエリが実行されないと、レコード セットは返されません。  
  
 16 = を使用して、レコード セットを開いたは GetHiddenColumns **adLockBatchOptimistic**して非表示の列は、レコード セットに含められます。  
  
 *ReadOnly*、 *NoBatch*と*GetHiddenColumns*相互排他的なオプションは、それらの 1 つ以上を設定するエラーではありません。 複数のオプションが設定されている場合*GetHiddenColumns*後に、その他のすべてのオプションよりも優先*ReadOnly*します。 使用して、レコード セットを開くオプションが指定されていない場合、既定では、 **adLockBatchOptimistic**が非表示の列が、レコード セットに含まれていません。  
  
 *pParameters*  
 パラメーターの定義のセーフ配列を格納するバリアント。 場合、 *GetInfo*オプションに指定されました*lExecuteOptions*、OLE DB プロバイダーから取得したパラメーターの定義を返すこのパラメーターを使用します。 それ以外の場合、このパラメーターを空にすることがあります。  
  
## <a name="remarks"></a>コメント  
 *HandlerString*パラメーターを null にすることがあります。 この場合の処理は、RDS サーバーを構成する方法によって異なります。 "MSDFMAP.handler"のハンドラーの文字列では、Microsoft から提供されたハンドラー (Msdfmap.dll) を使用することを示します。 "MASDFMAP.handler,sample.ini"のハンドラーの文字列は、Msdfmap.dll ハンドラーを使用することと、ハンドラーに"sample.ini"引数を渡す必要がありますを示します。 MSDFMAP.dll は、方向、sample.ini を使用して、接続およびクエリ文字列を確認すると、引数を解釈します。  
  
> [!NOTE]
>  **Execute21**メソッドは、バージョンの[Execute メソッド (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)します。 使用する必要がある、 **Execute** 2.1 では、ADO と通信するメソッド、 **Execute21**メソッドを代わりに呼び出すことができます。 機能、 **Execute**メソッド ADO 2.5 以降では ADO 2.1 では、同じメソッドを提供する機能のスーパー セットです。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


