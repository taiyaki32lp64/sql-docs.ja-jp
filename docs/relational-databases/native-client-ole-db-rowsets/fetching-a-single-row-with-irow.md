---
title: IRow | を使用した単一の行のフェッチMicrosoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c73bb76df097d259422f2c5626ecfb08668036c6
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761747"
---
# <a name="fetching-a-single-row-with-irow"></a>IRow による 1 行のフェッチ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでの**IRow**インターフェイスの実装は、パフォーマンスを向上させるために簡略化されています。 **IRow** では、1 つの行オブジェクトの列に直接アクセスできます。 コマンドの実行結果が正確に 1 行になることが事前にわかっている場合、**IRow** でその行の列を取得できます。 結果セットが複数の行で構成される場合は、**IRow** では先頭の行だけが公開されます。  
  
 **IRow** 実装では、行を移動することはできません。 行内の各列には 1 回だけアクセスされます。ただし、例外が 1 つあります。最初に列サイズを確認し、次にデータをフェッチする場合は、列に 2 回アクセスできます。  
  
> [!NOTE]  
>  **IRow::Open** は、DBGUID_STREAM 型と DBGUID_NULL 型のオブジェクトを開くことだけをサポートします。  
  
 **ICommand::Execute** メソッドを使用して行オブジェクトを取得するには、IID_IRow を渡す必要があります。 複数の結果セットを処理するには、**IMultipleResults** インターフェイスを使用する必要があります。 **IMultipleResults** では、**IRow** と **IRowset** がサポートされます。 **IRowset** は、一括操作に使用されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [IRow::GetColumns の使用](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [IRow を使用した BLOB データのフェッチ](https://msdn.microsoft.com/library/badbd6ac-20aa-4891-a14f-48d38e7f30de)  
  
## <a name="see-also"></a>参照  
 [行セット](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
