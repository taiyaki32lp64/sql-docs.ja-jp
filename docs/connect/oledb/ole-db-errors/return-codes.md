---
title: リターンコード |Microsoft Docs
description: リターン コード
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: pelopes
ms.openlocfilehash: a1deedd8903f69268ebc5e7f5caafaa79a7f7b18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994926"
---
# <a name="return-codes"></a>リターン コード
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  最も基本的なレベルでは、メンバー関数は成功するか失敗するかのどちらかです。 それよりもやや詳細なレベルでは、関数は成功しても、その成功はアプリケーション開発者が意図した状態ではない場合があります。  
  
 OLE DB のリターン コードの詳細については、「[リターン コード (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631)」を参照してください。  
  
 SQL Server メンバー関数の OLE DB ドライバーが S_OK を返すと、関数は成功します。  
  
 OLE DB Driver for SQL Server のメンバー関数が S_OK を返さない場合は、OLE/COM HRESULT をアンパックする FAILED マクロと IS_ERROR マクロにより、関数全体が成功したか失敗したかを判断できます。  
  
 FAILED または IS_ERROR が TRUE を返した場合、OLE DB Driver for SQL Server のコンシューマーは、メンバー関数の実行が失敗したことを確認できます。 FAILED または IS_ERROR が FALSE を返し、HRESULT が S_OK と等しくない場合、SQL Server コンシューマーの OLE DB ドライバーは、何らかの意味で関数が成功したことを保証します。 コンシューマーは OLE DB Driver for SQL Server のエラー インターフェイスから返される、関数の成功に関する詳細情報を取得できます。 また、関数が明らかに失敗している (FAILED マクロが TRUE を返した) 場合、OLE DB Driver for SQL Server のエラー インターフェイスから拡張エラー情報を取得できます。  
  
 SQL Server コンシューマー用の OLE DB ドライバーでは、通常、"情報での成功" という HRESULT が返さ DB_S_ERRORSOCCURRED ます。 通常、DB_S_ERRORSOCCURRED を返すメンバー関数では、コンシューマーに状態値を提供するパラメーターが 1 つ以上定義されています。 コンシューマーは状態値パラメーターに返される情報以外のエラー情報を取得できない場合があるので、状態値が提供された場合にこの値を取得できるアプリケーション ロジックを実装することをお勧めします。  
  
 SQL Server メンバー関数の OLE DB ドライバーは、成功コード S_FALSE を返しません。 SQL Server メンバー関数のすべての OLE DB ドライバーは、成功を示すために常に S_OK を返します。  
  
## <a name="see-also"></a>参照  
 [エラー](../../oledb/ole-db-errors/errors.md)  
  
  
