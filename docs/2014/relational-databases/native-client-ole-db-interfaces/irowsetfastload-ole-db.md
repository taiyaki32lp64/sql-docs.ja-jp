---
title: IRowsetFastLoad (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35cee52e9a85989123bcb10d998d37ce86a28601
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209814"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
  `IRowsetFastLoad`インターフェイスのサポートを公開する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリベースの一括コピー操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーでは、インターフェイスを使用して、迅速にデータを追加すると、既存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル。  
  
 セッションで SSPROP_ENABLEFASTLOAD を VARIANT_TRUE に設定した場合、その後にそのセッションから返される行セットのデータを読み取ることはできません。 SSPROP_ENABLEFASTLOAD が VARIANT_TRUE に設定されている場合、そのセッションで作成される行セットはすべて IRowsetFastLoad 型になります。 IRowsetFastLoad の行セットは行セットのフェッチをサポートしていないため、これらの行セットのデータを読み取ることはできません。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|方法|説明|  
|------------|-----------------|  
|[Irowsetfastload::commit &#40;OLE DB&#41;](irowsetfastload-commit-ole-db.md)|挿入される行のバッチの終わりをマークし、挿入された行を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルに書き込みます。|  
|[Irowsetfastload::insertrow &#40;OLE DB&#41;](irowsetfastload-insertrow-ole-db.md)|一括コピー行セットに行を追加します。|  
  
## <a name="see-also"></a>関連項目  
 [インターフェイス&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [IRowsetFastLoad を使用したデータの一括コピー &#40;OLE DB&#41;](../native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [IROWSETFASTLOAD と ISEQUENTIALSTREAM を使用した SQL SERVER への BLOB データの送信 &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
