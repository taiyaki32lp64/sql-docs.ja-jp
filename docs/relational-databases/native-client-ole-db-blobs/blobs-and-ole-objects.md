---
title: Blob と OLE オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b4e284d2086684af232c17b59675b834b26f497b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790630"
---
# <a name="blobs-and-ole-objects"></a>BLOB と OLE オブジェクト
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **ISequentialStream**インターフェイスを公開して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**、 **text**、 **image**、 **varchar (max)** 、 **nvarchar (** max)、 **varbinary (max) へのコンシューマーアクセスをサポートします。** バイナリラージオブジェクト (blob) としての xml データ型。 **ISequentialStream** の **Read** メソッドを使用すると、扱いやすい単位で大量のデータを取得できます。  
  
 この機能を示すサンプルについては、「 [ &#40;Large&#41;Data OLE DB の設定](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)」を参照してください。  
  
 コンシューマーがデータ変更のためにバインドされたアクセサーにインターフェイスポインターを提供する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、コンシューマーが実装する**IStorage**インターフェイスを使用できます。  
  
 大きな値のデータ型の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **IRowset**および DDL インターフェイスの型サイズの想定を確認します。 最大サイズが無制限に設定された**varchar**、 **nvarchar**、および**varbinary**データ型の列は、スキーマ行セットと列データ型を返すインターフェイスによって islong として表されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **varchar (max)** 、 **varbinary (max)** 、 **nvarchar (max)** 型をそれぞれ DBTYPE_STR、DBTYPE_BYTES および DBTYPE_WSTR として公開します。  
  
 これらの型を使用するには、アプリケーションに次のオプションがあります。  
  
-   データ型 DBTYPE_STR、DBTYPE_BYTES、または DBTYPE_WSTR としてバインドします。 バッファーのサイズが十分でない場合、これらのデータ型は以前のリリースでの動作と同様に (以前よりも大きな値を格納できるようになりましたが)、切り捨てが行われます。  
  
-   データ型としてバインドし、DBTYPE_BYREF も指定します。  
  
-   DBTYPE_IUNKNOWN としてバインドし、ストリーミングを使用します。  
  
 DBTYPE_IUNKNOWN にバインドすると、ISequentialStream ストリーム機能が使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、大きな値のデータ型に対して DBTYPE_IUNKNOWN として出力パラメーターをバインドすることがサポートされています。これにより、ストアドプロシージャがこれらのデータ型を、DBTYPE_IUNKNOWN としてクライアントに公開される戻り値として返すシナリオが容易になります。  
  
## <a name="storage-object-limitations"></a>ストレージ オブジェクトの制限事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、開いているストレージオブジェクトを1つだけサポートできます。 複数の **ISequentialStream** インターフェイス ポインターへの参照を取得するために、複数のストレージ オブジェクトを開こうとすると、DBSTATUS_E_CANTCREATE が返されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、読み取り専用の DBPROP_BLOCKINGSTORAGEOBJECTS プロパティの既定値は VARIANT_TRUE です。 この値は、ストレージ オブジェクトがアクティブである場合に、(ストレージ オブジェクト以外の) 一部のメソッドが失敗して E_UNEXPECTED が返されることを示します。  
  
-   コンシューマーによって実装されたストレージオブジェクトによって示されるデータの長さは、ストレージオブジェクトを参照する行アクセサーが作成されるときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーに認識される必要があります。 コンシューマー側では、アクセサーの作成に使用する DBBINDING 構造体に長さのインジケーターをバインドする必要があります。  
  
-   行に1つ以上の大きなデータ値が含まれていて DBPROP_ACCESSORDER が DBPROPVAL_AO_RANDOM ない場合、コンシューマーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーカーソルでサポートされている行セットを使用して行データを取得するか、すべての大きなデータ値を処理してから、他の行の値を取得する必要があります。 DBPROP_ACCESSORDER が DBPROPVAL_AO_RANDOM 場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、すべての xml データ型をバイナリラージオブジェクト (Blob) としてキャッシュし、任意の順序でアクセスできるようにします。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [大きなデータの取得](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [大きなデータの設定](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 出力パラメーターのストリーミング サポート](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;OLE DB&#41; ](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [大きな値の型の使用](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
