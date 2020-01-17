---
title: Synchronize21 メソッド (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66c3b9ecefd63cf7de1806e6fa838a0204626605
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963251"
---
# <a name="synchronize21-method-rds"></a>Synchronize21 メソッド (RDS)
ADO 2.1 で使用する接続文字列で指定されたデータベースでは、特定のレコード セットを同期します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ConnectionString*  
 要求が送信され、OLE DB プロバイダーへの接続に使用する文字列。 ハンドラーを使用する場合、ハンドラーが編集または接続文字列を置換できます。  
  
 *HandlerString*  
 文字列は、この実行で使用するハンドラーを識別します。 文字列には、2 つの部分が含まれています。 最初の部分には、使用するハンドラーの名前 (ProgID) が含まれています。 文字列の 2 番目の部分には、ハンドラーに渡される引数が含まれています。 特定のハンドラーには、引数文字列を解釈する方法です。 2 つの部分は、最初のインスタンスの文字列で、コンマで区切られます。 引数の文字列は、追加のコンマを含めることができます。 引数は省略可能です。  
  
 *lSynchronizeOptions*  
 同期オプションのビット マスクです。  
  
 1 =*UpdateTransact*データベースへの更新は、トランザクションにラップされます。 更新プログラムの失敗した場合は、トランザクションが中止されました。  
  
 2 =*RefreshWithUpdate*原因は、どちらの場合に返される状態を行*更新*も*RefreshConflicts*設定されます。  
  
 4 =*更新*データベースの現在のデータでレコード セットが更新されます。 保留中の更新は データベースにプッシュされません。 このビットが設定されていない場合、レコード セットは更新されていないと、保留中の更新プログラムがデータベースにプッシュされます。  
  
 8 =*RefreshConflicts*保留中の変更行の更新が失敗します。 更新に失敗した行は、データベースの現在のデータで更新されます。  
  
 *ppRecordset*  
 同期するレコード セットへのポインターへのポインター。  
  
 *pStatusArray*  
 影響を受ける行の行の状態のセーフ配列を返すために使用バリアントを同期します。 次の同期オプションのいずれも設定されている場合を設定できません。*RefreshWithUpdate*、*更新*と*RefreshConflicts*します。  
  
## <a name="remarks"></a>コメント  
 *HandlerString*パラメーターを null にすることができます。 この場合の動作は、RDS サーバーを構成する方法によって異なります。 "MSDFMAP.handler"のハンドラーの文字列では、Microsoft から提供されたハンドラー (Msdfmap.dll) を使用することを示します。 "MASDFMAP.handler,sample.ini"のハンドラーの文字列は、Msdfmap.dll ハンドラーを使用することと、ハンドラーに"sample.ini"引数を渡す必要がありますを示します。 Msdfmap.dll は、方向、sample.ini を使用して、接続およびクエリ文字列を確認すると、引数を解釈します。  
  
> [!NOTE]
>  **Synchronize21**メソッドは、単純のバージョン、[同期メソッド (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md)します。 使用する必要がある、**同期**2.1 では、ADO と通信するメソッド、 **Synchronize21**メソッドを代わりに呼び出すことができます。 機能、**同期**メソッド ADO 2.5 以降では ADO 2.1 では、同じメソッドを提供する機能のスーパー セットです。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


