---
title: :Bcpexec (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPExec (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPExec method
ms.assetid: 0f4ebb63-cf03-4e53-846e-6c3021cde007
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1d7e00f3412967a8257b27fa2c8637905e657cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62519316"
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec (OLE DB)
  一括コピー操作を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPExec(   
DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>コメント  
 **BCPExec** メソッドでは、[IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) メソッドで使用されている *eDirection* パラメーターの値に従って、データをユーザー ファイルからデータベース テーブルに、またはデータベース テーブルからユーザー ファイルにコピーします。  
  
 **BCPExec** を呼び出す前に、有効なユーザー ファイル名を指定して **BCPInit** メソッドを呼び出します。 この操作を行わないと、エラーが発生します。 唯一の例外は、一括コピーの出力操作にクエリを使用する場合です。 この場合は、**BCPInit** メソッドでテーブル名に NULL を指定してから、BCP_OPTION_HINTS オプションを使用してクエリを指定します。  
  
 **BCPExec** メソッドは、短時間に優れた結果を得られる唯一の一括コピー メソッドです。 そのため、このメソッドは非同期モードをサポートする唯一の一括コピー メソッドでもあります。 非同期モードを使用するには、プロバイダー固有のセッション プロパティ SSPROP_ASYNCH_BULKCOPY を VARIANT_TRUE に設定してから、**BCPExec** メソッドを呼び出します。 このプロパティは、DBPROPSET_SQLSERVERSESSION プロパティ セットに含まれています。 コピーの完了を確認するには、同じパラメーターを指定して **BCPExec** メソッドを呼び出します。 一括コピーがまだ完了していない場合は、**BCPExec** メソッドから DB_S_ASYNCHRONOUS が返されます。 また、*pRowsCopied* 引数には、サーバーとの間で送受信される行数の進行状況を表す数も返されます。 サーバーに送信された行は、バッチの終わりに到達するまではコミットされません。  
  
## <a name="arguments"></a>引数  
 *pRowsCopied*[out]  
 DWORD へのポインターです。 **BCPExec** メソッドは、正常にコピーされた行数を使用して、DWORD を設定します。 *pRowsCopied* 引数に NULL を設定すると、**BCPExec** メソッドはこの引数を無視します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) インターフェイスを使用してください。  
  
 E_UNEXPECTED  
 メソッドの呼び出しが予期されませんでした。 たとえば、このメソッドを呼び出す前に、**BCPInit** メソッドが呼び出されなかった場合などです。 また、操作が BCP_OPTION_ABORT オプションを使用して中断され、その後、**BCPExec** メソッドが呼び出された場合にも発生します。  
  
 E_OUTOFMEMORY  
 メモリ不足エラーです。  
  
 DB_S_ENDOFROWSET  
 一括コピー操作が終了し、すべてのデータ転送が完了しました。  
  
 DB_S_ASYNCHRONOUS  
 行の現在のバッチがコピーされました。 次のバッチを転送するには、**BCPExec** メソッドを再度呼び出します。  
  
 DB_S_ERRORSOCCURRED  
 一括コピー操作中にエラーが発生しました。そのため、一部の行がコピーされなかった可能性があります。 エラー数は、許容されるエラーの最大数には達していません。  
  
## <a name="see-also"></a>参照  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../native-client/features/performing-bulk-copy-operations.md)  
  
  
