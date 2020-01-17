---
title: 'IBCPSession:: BCPColumns (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
ms.assetid: c338abe8-9e30-4853-a7c6-b1a6c00095e1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b5385d32ef349284f261a457391581b6e28da03
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789705"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル内の列にバインドされるフィールド数を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、内部的に [IBCPSession::BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) を呼び出して、フィールド データの既定値を設定します。 これらの既定値は、[IBCPSession::BCPInit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) を使用してテーブル名を指定するときに、プロバイダーが内部的に取得する SQL Server の列情報を基に設定されます。  
  
> [!NOTE]  
>  有効なファイル名を指定して **BCPInit** を呼び出した後でのみ、このメソッドを呼び出すことができます。  
  
 既定とは異なる形式のユーザー ファイルを使用する場合にのみ、このメソッドを呼び出す必要があります。 ユーザー ファイルの既定の形式の詳細については、**BCPInit** メソッドを参照してください。  
  
 独自のファイル形式を完全に定義するために、**BCPColumns** メソッドを呼び出した後、ユーザー ファイル内の列ごとに **BCPColFmt** メソッドを呼び出す必要があります。  
  
## <a name="arguments"></a>引数  
 *nColumns*[in]  
 ユーザー ファイル内のフィールドの総数です。 ユーザー ファイルから SQL Server テーブルへのデータの一括コピーを準備していて、ユーザー ファイル内のすべてのフィールドをコピーしない場合でも、*nColumns* 引数にユーザー ファイル内のフィールドの総数を設定する必要があります。 その後、スキップするフィールドを **BCPColFmt** を使って指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) インターフェイスを使用してください。  
  
 E_UNEXPECTED  
 メソッドの呼び出しが予期されませんでした。 たとえば、このメソッドを呼び出す前に、**BCPInit** メソッドが呼び出されなかった場合などです。 また、1 回の一括コピー操作でこのメソッドが複数回呼び出されたときもこのリターン コードが返されます。  
  
 E_OUTOFMEMORY  
 メモリ不足エラーです。  
  
## <a name="see-also"></a>参照  
 [Ibcpsession &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
