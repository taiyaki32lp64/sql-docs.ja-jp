---
title: IRow で 1 つの行をフェッチします。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: faf887ab5e03d2d0ca8702dc9bd35d0ba094ece4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183669"
---
# <a name="fetching-a-single-row-with-irow"></a>IRow による 1 行のフェッチ
  **IRow**インターフェイスの実装、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアント OLE DB プロバイダーは、パフォーマンスを向上させるのに簡略化されています。 **IRow** では、1 つの行オブジェクトの列に直接アクセスできます。 コマンドの実行結果が正確に 1 行になることが事前にわかっている場合、**IRow** でその行の列を取得できます。 結果セットが複数の行で構成される場合は、**IRow** では先頭の行だけが公開されます。  
  
 **IRow** 実装では、行を移動することはできません。 行内の各列には、1 つの例外の 1 つだけの時間にアクセスします。列のサイズを確認して、データをフェッチするにより、列に 1 回をアクセスできます。  
  
> [!NOTE]  
>  **IRow::Open** は、DBGUID_STREAM 型と DBGUID_NULL 型のオブジェクトを開くことだけをサポートします。  
  
 **ICommand::Execute** メソッドを使用して行オブジェクトを取得するには、IID_IRow を渡す必要があります。 複数の結果セットを処理するには、**IMultipleResults** インターフェイスを使用する必要があります。 **IMultipleResults** では、**IRow** と **IRowset** がサポートされます。 **IRowset** は、一括操作に使用されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [IRow::GetColumns の使用](using-irow-getcolumns.md)  
  
-   [IRow を使用した BLOB データのフェッチ](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>参照  
 [行セット](rowsets.md)  
  
  
