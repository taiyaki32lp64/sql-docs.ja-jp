---
title: エラー | Microsoft Docs
description: エラー
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9bf1985706cefc3007da56a9bf782a070e3b8edf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994960"
---
# <a name="errors"></a>エラー
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE オブジェクトや COM オブジェクトは、オブジェクト メンバー関数の HRESULT リターン コードによってエラーを報告します。 OLE と COM の HRESULT は、ビットがまとめられている構造体です。 OLE には、構造体のメンバーを取り出すマクロが用意されています。  
  
 OLE と COM は、**IErrorInfo** インターフェイスを指定します。 このインターフェイスでは、**GetDescription** などのメソッドを公開します。 これにより、クライアントは OLE サーバーや COM サーバーからエラーの詳細を取得できます。 OLE DB では、複数のエラー情報パケットを 1 回のメンバー関数の実行で返すことができるように **IErrorInfo** を拡張します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では複数のエラーを返すことができます。 アプリケーションで一度に 1 つずつサーバー エラーを取得するには、ISQLErrorInfo および IErrorRecords と組み合わせて [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) を呼び出します。  
  
 OLE DB Driver for SQL Server は、OLE DB レコードに対して機能強化された **IErrorInfo**、カスタム **ISQLErrorInfo**、およびプロバイダー固有の [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) の各エラー オブジェクト インターフェイスを公開します。  
  
 エラーのトレースの詳細については、「[データ アクセスのトレース](https://go.microsoft.com/fwlink/?LinkId=125805)」を参照してください。 で[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]追加されたエラートレースの機能強化の詳細については、「[拡張イベントログの診断情報へのアクセス](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [リターン コード](../../oledb/ole-db-errors/return-codes.md)  
  
-   [エラー インターフェイス内の情報](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server エラーの詳細](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [エラー情報の取得](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server のメッセージ結果](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のプログラミング](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
