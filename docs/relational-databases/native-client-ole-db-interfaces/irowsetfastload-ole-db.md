---
title: IRowsetFastLoad (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 39a9f660f39a27a189c81d24d4d155d8764037d1
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789398"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **IRowsetFastLoad** インターフェイスでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメモリベースの一括コピー操作のサポートが公開されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーコンシューマーは、インターフェイスを使用して、既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにデータをすばやく追加します。  
  
 セッションで SSPROP_ENABLEFASTLOAD を VARIANT_TRUE に設定した場合、その後にそのセッションから返される行セットのデータを読み取ることはできません。 SSPROP_ENABLEFASTLOAD が VARIANT_TRUE に設定されている場合、そのセッションで作成される行セットはすべて IRowsetFastLoad 型になります。 IRowsetFastLoad の行セットは行セットのフェッチをサポートしていないため、これらの行セットのデータを読み取ることはできません。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|メソッド|[説明]|  
|------------|-----------------|  
|[IRowsetFastLoad:: Commit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|挿入される行のバッチの終わりをマークし、挿入された行を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルに書き込みます。|  
|[IRowsetFastLoad:: InsertRow &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|一括コピー行セットに行を追加します。|  
  
## <a name="see-also"></a>参照  
 [インターフェイス&#40;OLE DB&#41; ](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [IRowsetFastLoad を使用したデータの一括コピー &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [IROWSETFASTLOAD と ISEQUENTIALSTREAM を使用した SQL SERVER への BLOB データの送信 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
