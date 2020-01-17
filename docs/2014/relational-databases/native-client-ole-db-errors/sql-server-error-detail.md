---
title: SQL Server エラーの詳細 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c7535e4579204834fc8024b7c37c46675320b8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63156392"
---
# <a name="sql-server-error-detail"></a>SQL Server エラーの詳細
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、プロバイダー固有のエラー インターフェイスを定義します。 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)します。 このインターフェイスにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーの詳細が返されるので、コマンドの実行や行セットの操作が失敗したときに役立ちます。  
  
 **ISQLServerErrorInfo** インターフェイスにアクセスする方法は 2 つあります。  
  
 次のコード サンプルに示すように、コンシューマーは **IErrorRecords::GetCustomerErrorObject** を呼び出して **ISQLServerErrorInfo** ポインターを取得できます。 (**ISQLErrorInfo** を取得する必要はありません)。**ISQLErrorInfo** と **ISQLServerErrorInfo** は、どちらもカスタム OLE DB エラー オブジェクトです。**ISQLServerErrorInfo** は、プロシージャ名や行番号などの詳細情報を含むサーバー エラーの情報を取得するために使用するインターフェイスです。  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 **ISQLServerErrorInfo** ポインターを取得するもう 1 つの方法は、既に取得した **ISQLErrorInfo** ポインターの **QueryInterface** メソッドを呼び出すことです。 ただし、**ISQLServerErrorInfo** には **ISQLErrorInfo** から取得できる情報のスーパーセットが含まれているので、**GetCustomerErrorObject** から直接 **ISQLServerErrorInfo** を取得する方が効果的です。  
  
 **ISQLServerErrorInfo** インターフェイスでは、メンバー関数 [ISQLServerErrorInfo::GetErrorInfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md) が公開されます。 この関数では、SSERRORINFO 構造体へのポインターと文字列バッファーへのポインターが返されます。 どちらのポインターが参照するメモリも、コンシューマーが **IMalloc::Free** メソッドを使用して割り当て解除する必要があります。  
  
 コンシューマーでは SSERRORINFO 構造体のメンバーが次のように解釈されます。  
  
|Member|説明|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー メッセージです。 このエラー メッセージは、**IErrorInfo::GetDescription** で返される文字列と同じです。|  
|*pwszServer*|セッションの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。|  
|*pwszProcedure*|該当する場合は、エラーが発生したプロシージャの名前です。 該当しない場合は空文字列です。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネイティブ エラー番号です。 **ISQLErrorInfo::GetSQLInfo** の *plNativeError* パラメーターで返される値と同じです。|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー メッセージの状態です。|  
|*bClass*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー メッセージの重大度です。|  
|*wLineNumber*|該当する場合は、ストアド プロシージャでエラーが発生した行番号です。|  
  
## <a name="see-also"></a>参照  
 [エラー](errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
