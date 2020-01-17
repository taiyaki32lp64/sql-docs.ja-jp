---
title: データ ソース オブジェクト (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], data source objects
- SQL Server Native Client, data source objects
- SQLNCLI, data source objects
- SQL Server Native Client OLE DB provider, data source objects
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- CLSID
ms.assetid: c1d4ed20-ad3b-4e33-a26b-38d7517237b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b602695720e0d6567e44e4fbe8fd06b6d496a6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63130598"
---
# <a name="data-source-objects-ole-db"></a>データ ソース オブジェクト (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client などのデータ ストアへのリンクを確立するために使用される OLE DB インターフェイスのセットの用語のデータ ソースを使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 最初のタスクは、プロバイダーのデータ ソース オブジェクトのインスタンスを作成、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client のコンシューマーです。  
  
 すべての OLE DB プロバイダーは、そのプロバイダー自体のクラス ID (CLSID) を宣言します。 CLSID、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、C/C++ GUID CLSID_SQLNCLI10 (シンボル SQLNCLI_CLSID は、正しいを解決するを参照する sqlncli.h ファイル progid)。 コンシューマーは、CLSID を指定して OLE **CoCreateInstance** 関数を使用し、データ ソース オブジェクトのインスタンスを作成します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、インプロセス サーバーです。 インスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダー オブジェクトは、実行可能ファイルのコンテキストを示すために、CLSCTX_INPROC_SERVER マクロを使用して作成されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのデータ ソース オブジェクトは、コンシューマーに既存の接続を許可する OLE DB 初期化インターフェイスを公開します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
 すべての接続を使用して作成、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが自動的にこれらのオプションを設定します。  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 この例では、クラス id マクロを使用して作成、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのデータ ソース オブジェクトとの参照を取得、 **IDBInitialize**インターフェイス。  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 インスタンスが正常に作成すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのデータ ソース オブジェクト、コンシューマー アプリケーションは、データ ソースを初期化し、セッションを作成して続行できます。 OLE DB セッションは、データへのアクセスや操作を可能にするインターフェイスを提供します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、その最初の接続の指定インスタンスに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正常なデータ ソースの初期化の一部として。 いずれかのデータ ソース初期化インターフェイスで参照が保持されている間、または **IDBInitialize::Uninitialize** メソッドが呼び出されるまで、その最初の接続が維持されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [データ ソースのプロパティ &#40;OLE DB&#41;](data-source-properties-ole-db.md)  
  
-   [データ ソース情報のプロパティ](data-source-information-properties.md)  
  
-   [初期化プロパティと承認プロパティ](initialization-and-authorization-properties.md)  
  
-   [セッション](sessions.md)  
  
-   [セッション プロパティ](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [保存されるデータ ソース オブジェクト](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
