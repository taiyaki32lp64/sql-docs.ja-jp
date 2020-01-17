---
title: Execute メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1a5fa5c9002d4a27490dfc98fb79f482539f042
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964318"
---
# <a name="execute-method-rds"></a>Execute メソッド (RDS)
要求を実行し、2.5 以降は、ADO で使用する ADO レコード セットを作成します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ConnectionString*  
 実行の要求を送信する先の OLE DB プロバイダーへの接続に使用する文字列。 使用して、ハンドラーが指定されている場合*HandlerString*編集、接続文字列に置き換えます。  
  
 *HandlerString*  
 この実行で使用するハンドラーを識別するための 2 つの部分文字列。 文字列には、2 つの部分が含まれています。 最初の部分には、使用するハンドラーの名前 (ProgID) が含まれています。 2 番目の部分には、ハンドラーに渡される引数が含まれています。 引数の文字列を解釈する方法の詳細については、各ハンドラーに固有です。 2 つの部分は、最初のインスタンスの文字列で、コンマで区切られます。 引数の文字列は、追加のコンマを含めることができます。 引数は省略可能です。  
  
 *QueryString*  
 接続文字列で識別される OLE DB プロバイダーでサポートされているコマンド言語でのコマンド。 SQL ベースのプロバイダーでは、 *QueryString* TRANSACT-SQL コマンドのステートメントを含めることができますが、非 SQL プロバイダー (たとえば、MSDataShape) のこのできない可能性があります、[!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントのクエリを実行します。  
  
 ハンドラーを使用している場合、ハンドラーが変更またはここで指定した値を置き換えることができます。 ハンドラーが通常置換など*QueryString* .ini ファイルからクエリ文字列を使用します。 既定では、Msdfmap.ini ファイルが使用されます。  
  
 *lFetchOptions*  
 非同期のフェッチの種類を示します。  
  
 詳細については、次を参照してください。 [FetchOptions プロパティ (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)します。  
  
 *TableID*  
 A**バリアント**型の VT_EMPTY または VT_BSTR のいずれか。 この値が VT_EMPTY 型の場合は無視されます。 使用して、レコード セットが作成された VT_BSTR 型の場合、 **adCmdTableDirect**とここで指定した値と*QueryString*パラメーターは無視されます。  
  
 *lExecuteOptions*  
 実行オプションのビット マスク。  
  
 1 =*ReadOnly* 、レコード セットを使用して開いたは**adLockReadOnly**します。  
  
 2 =*NoBatch* 、レコード セットを使用して開いたは**adLockOptimistic**します。  
  
 4 =*AllParamInfoSupplied* 、呼び出し元のすべてのパラメーターのパラメーター情報を提供することを保証*pParameters*します。  
  
 8 =*GetInfo* 、クエリのパラメーター情報が、OLE DB プロバイダーから取得しで返される、 *pParameters*パラメーター。 クエリが実行されないと、レコード セットは返されません。  
  
 16 =*GetHiddenColumns* 、レコード セットを使用して開いたは**adLockBatchOptimistic**して非表示の列は、レコード セットに含められます。  
  
 *読み取り専用*、 *NoBatch*と*GetHiddenColumns*相互排他的なオプションです。 ただし、それらの 1 つ以上を設定するとエラーに生成されません。 複数のオプションが設定されている場合*GetHiddenColumns*他のすべてを続けてよりも優先*ReadOnly*します。 使用して、レコード セットを開くオプションが指定されていない場合、既定では、 **adLockBatchOptimistic**と非表示の列は、レコード セットに含まれません。  
  
 *pParameters*  
 A**バリアント**パラメーター定義のセーフ配列を格納しています。 場合、 *GetInfo*オプションに指定されました*lExecuteOptions*、OLE DB プロバイダーから取得したパラメーターの定義を返すこのパラメーターを使用します。 それ以外の場合、このパラメーターを空にすることができます。  
  
 *lcid*  
 返されるエラーをビルドするために使用、LCID *pInformation*します。  
  
 *pInformation*  
 実行によって返される情報エラーへのポインター。 NULL の場合、エラー情報は返されません。  
  
## <a name="remarks"></a>コメント  
 *HandlerString*パラメーターを null にすることがあります。 この場合の動作は、RDS サーバーを構成する方法によって異なります。 "MSDFMAP.handler"のハンドラーの文字列では、Microsoft から提供されたハンドラー (Msdfmap.dll) を使用することを示します。 "MASDFMAP.handler,sample.ini"のハンドラーの文字列は、Msdfmap.dll ハンドラーを使用することと、ハンドラーに"sample.ini"引数を渡す必要がありますを示します。 MSDFMAP.dll は、方向、sample.ini を使用して、接続およびクエリ文字列を確認すると、引数を解釈します。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


