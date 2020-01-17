---
title: FILESTREAM のサポート (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ff05424d9b8726f21c8c4aa2facd42b87961cc2
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73760876"
---
# <a name="filestream-support-ole-db"></a>FILESTREAM のサポート (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 以降では OLE DB、拡張された FILESTREAM 機能がサポートされています。 この機能の詳細については、「 [FILESTREAM のサポート](../../../relational-databases/native-client/features/filestream-support.md)」を参照してください。 サンプルについては、「 [Filestream と OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md)」を参照してください。  
  
 2 GB を超える**varbinary (max)** 値を送受信するために、アプリケーションではパラメーターと結果のバインドで**DBTYPE_IUNKNOWN**を使用します。 パラメーターの場合、プロバイダーは ISequentialStream の IUnknown:: QueryInterface と ISequentialStream を返す結果を呼び出す必要があります。  
  
 OLE DB の場合、ISequentialStream 値に関連するチェックは緩和されます。 *Wtype*が**DBBINDING**構造体で**DBTYPE_IUNKNOWN**場合、 *dwpart*から**DBPART_LENGTH**を省略するか、データの長さ (オフセット*oblength* ) を設定して、長さのチェックを無効にすることができます。バッファー) ~ 0 までです。 この場合、プロバイダーは値の長さをチェックせず、ストリームで利用可能なすべてのデータを要求し、返します。 この変更は、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (以降の) サーバーに接続する場合に限り、すべてのラージ オブジェクト (LOB) 型と XML に適用されます。 これにより、既存のアプリケーションや下位レベルのサーバーとの一貫性や下位互換性を維持しつつ、より柔軟な開発が可能になります。  
  
 この変更は、データを転送するすべてのインターフェイス (主に IRowset:: GetData、ICommand:: Execute、および IRowsetFastLoad:: InsertRow) に影響します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
