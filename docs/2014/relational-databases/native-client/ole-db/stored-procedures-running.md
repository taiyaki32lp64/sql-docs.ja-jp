---
title: ストアド プロシージャ (OLE DB) の実行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0102fa66e65fa11f47eec9f49cd1fa90fb11f877
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638758"
---
# <a name="running-stored-procedures-ole-db"></a>ストアド プロシージャの実行 (OLE DB)
  ステートメントの実行時、データ ソースに対して (クライアント アプリケーション内で直接ステートメントを実行または準備せずに) ストアド プロシージャを呼び出すと、次のような利点があります。  
  
-   高いパフォーマンス。  
  
-   ネットワーク オーバーヘッドの軽減。  
  
-   一貫性の向上  
  
-   正確性の向上  
  
-   機能の追加。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは 3 つのメカニズムをサポートしているを[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データを返すストアド プロシージャを使用します。  
  
-   プロシージャ内のすべての SELECT ステートメントで結果セットを生成する。  
  
-   プロシージャが出力パラメーターによってデータを返すことができる。  
  
-   プロシージャに整数のリターン コードを含めることができる。  
  
 アプリケーションでは、ストアド プロシージャからのこれらすべての出力を処理できる必要があります。  
  
 結果の処理中には、さまざまな OLE DB プロバイダーからさまざまなタイミングで出力パラメーターと戻り値が返されます。 場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、出力パラメーターおよびリターン コードが指定されていないまで、コンシューマーが取得またはストアド プロシージャによって返される結果セットが取り消されました。 これらのリターン コードと出力パラメーターは、サーバーからの最後の TDS パケットで返されます。  
  
 プロバイダーでは、DBPROP_OUTPUTPARAMETERAVAILABILITY プロパティを使用して、出力パラメーターと戻り値を返すタイミングを報告します。 このプロパティは、DBPROPSET_DATASOURCEINFO プロパティ セットに含まれています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROP_OUTPUTPARAMETERAVAILABILITY プロパティを DBPROPVAL_OA_ATROWRELEASE を示すリターン コードと出力パラメーターは返されないこと、結果セットが処理または解放されるまでに設定します。  
  
## <a name="see-also"></a>参照  
 [ストアド プロシージャ](stored-procedures.md)  
  
  
