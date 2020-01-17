---
title: 'ISQLServerErrorInfo:: GetErrorInfo (OLE DB) |Microsoft Docs'
description: ISQLServerErrorInfo::GetErrorInfo (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 54e9c71ca21647004ea3899306dcb15689dcc3d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015442"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]エラーの詳細を含む SQL Server SSERRORINFO 構造体の OLE DB ドライバーへのポインターを返します。  
  
 OLE DB Driver for SQL Server では、 **ISQLServerErrorInfo**エラーインターフェイスが定義されています。 このインターフェイスは、重大度や状態など、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エラーの詳細情報を返します。  

  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>引数  
 *ppSSErrorInfo*[out]  
 SSERRORINFO 構造体へのポインター。 メソッドが失敗するか、エラーに関連する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 情報がない場合、プロバイダーはメモリの割り当てを行わず、出力時に *ppSSErrorInfo* 引数に NULL ポインターを設定します。  
  
 *ppErrorStrings*[out]  
 Unicode 文字列ポインターへのポインター。 メソッドが失敗するか、エラーに関連する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 情報がない場合、プロバイダーはメモリの割り当てを行わず、出力時に *ppErrorStrings* 引数に NULL ポインターを設定します。 **IMalloc::Free** メソッドを使用して *ppErrorStrings* 引数を解放すると、メモリがブロック単位で割り当てられているので、結果の SSERRORINFO 構造体の 3 つの各文字列メンバーが解放されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_INVALIDARG  
 *PpSSErrorInfo*または*Pperrorstrings*引数のいずれかが NULL でした。  
  
 E_OUTOFMEMORY  
 SQL Server の OLE DB ドライバーが、要求を完了するために必要なメモリを割り当てられませんでした。  
  
## <a name="remarks"></a>Remarks  
 OLE DB Driver for SQL Server は、コンシューマーが渡したポインターを使用して返される、SSERRORINFO 文字列と OLECHAR 文字列用にメモリを割り当てます。 コンシューマーはエラー データにアクセスする必要がなくなった時点で、**IMalloc::Free** メソッドを使用してこのメモリの割り当てを解除する必要があります。  
  
 SSERRORINFO 構造体は、次のように定義されています。  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|メンバー|[説明]|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエラー メッセージ。 このメッセージは、**IErrorInfo::GetDescription** メソッドにより返されます。|  
|*pwszServer*|エラーが発生した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前。|  
|*pwszProcedure*|エラーがストアド プロシージャ内で発生している場合は、エラーが発生したストアド プロシージャの名前です。それ以外の場合は、空文字列になります。|  
|*lNative*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のエラー番号。 このエラー番号は、**ISQLErrorInfo::GetSQLInfo** メソッドの *plNativeError* パラメーターに返されるものと同じになります。|  
|*bState*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エラーの状態。|  
|*bClass*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エラーの重大度。|  
|*wLineNumber*|該当する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ストアド プロシージャのエラー メッセージを生成した行です。 プロシージャが関係していない場合は、既定値 1 が使用されます。|  
  
 構造体内のポインターは、*ppErrorStrings* 引数に返される文字列内のアドレスを指します。  
  
## <a name="see-also"></a>参照  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR &#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
