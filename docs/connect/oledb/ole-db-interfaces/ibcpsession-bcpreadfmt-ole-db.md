---
title: 'IBCPSession:: BCPReadFmt (OLE DB) |Microsoft Docs'
description: 'フォーマットファイルからのデータの読み取りに IBCPSession:: BCPReadFmt を使用する (OLE DB)'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 97274315275f11e77c458827740f44906a524ed9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015501"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  フォーマット ファイルから列ごとにフォーマット情報を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPReadFmt** メソッドは、データ ファイルのデータ形式を指定するフォーマット ファイルからデータを読み取る場合に使用されます。 このメソッドでは、適切なバージョンのフォーマット ファイルを検出することができます。 また、フォーマット ファイルが xml 形式か、または古いスタイルのテキスト形式かを自動的に検出し、フォーマット ファイルに適した動作をします。 SQL Server BCP の OLE DB ドライバーでサポートされているフォーマットファイルのバージョンは、6.0 以降です。  
  
 **BCPReadFmt** メソッドは形式の値を読み取ると、適宜、[IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) メソッドと [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) メソッドを呼び出します。 ユーザーがフォーマット ファイルを解析し、これらのメソッドを呼び出す必要はありません。  
  
 フォーマット ファイルを保存するには、[IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) メソッドを呼び出します。 **BCPReadFmt** メソッドの呼び出しでは、保存した形式を参照することができます。 また、一括コピー ユーティリティ (**bcp**) を使用して、**BCPReadFmt** メソッドで参照できるファイルに、ユーザー定義のデータ形式を保存することもできます。  
  
 [Ibcpsession:: BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)の*EOption*パラメーターの**BCP_OPTION_DELAYREADFMT**値によって、Ibcpsession:: BCPReadFmt の動作が変更されます。  
  
## <a name="arguments"></a>引数  
 *pwszFormatFile*[in]  
 データ ファイルのフォーマット情報を含むファイルのパスとファイル名。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) インターフェイスを使用してください。  
  
 E_OUTOFMEMORY  
 メモリ不足エラー。  
  
 E_UNEXPECTED  
 メソッドの呼び出しが予期されませんでした。 たとえば、このメソッドが呼び出される前に、[IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) メソッドが呼び出されなかった場合などです。  
  
## <a name="see-also"></a>参照  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
