---
title: 'IBCPSession:: BCPWriteFmt (OLE DB) |Microsoft Docs'
description: 'IBCPSession:: BCPWriteFmt を使用して、フォーマットファイルを xml またはテキスト形式で保存する (OLE DB)'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPWriteFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPWriteFmt method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 42a8b450fcc5536920ead44d4f401fb2e81d2b08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994537"
---
# <a name="ibcpsessionbcpwritefmt-ole-db"></a>IBCPSession::BCPWriteFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  フォーマット ファイルに列ごとのフォーマット情報を書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPWriteFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 フォーマット ファイルでは、一括コピーで作成されるデータ ファイルのデータの形式を指定します。 [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) メソッドと [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) メソッドの呼び出しでは、データ ファイルの形式を定義します。 **BCPWriteFmt** メソッドでは、この定義を pwszFormatFile 引数で参照されるファイルに保存します。  
  
 **BCPWriteFmt** メソッドでは、XML 形式またはテキスト形式のいずれかの形式でフォーマット ファイルを保存できます。 そのためには、BCP_OPTION_XML 制御オプションを指定して [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) メソッドを使用する必要があります。  
  
 保存されたフォーマット ファイルを読み込むには、[IBCPSession::BCPReadFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) メソッドを使用します。  
  
## <a name="arguments"></a>引数  
 *pwszFormatFile*[in]  
 データ ファイルのフォーマット情報を含むファイルのパスとファイル名。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) インターフェイスを使用してください。  
  
 E_OUTOFMEMORY  
 メモリ不足エラーです。  
  
 E_UNEXPECTED  
 メソッドの呼び出しが予期されませんでした。 たとえば、このメソッドが呼び出される前に、[IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) メソッドが呼び出されなかった場合などです。  
  
## <a name="see-also"></a>参照  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../../oledb/features/performing-bulk-copy-operations.md) 
  
  
