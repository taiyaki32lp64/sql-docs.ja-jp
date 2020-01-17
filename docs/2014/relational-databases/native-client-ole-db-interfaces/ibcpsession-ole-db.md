---
title: IBCPSession (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 142f6ac339e437877c485588333fabb04e0bd66b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241347"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
  **IBCPSession** インターフェイスでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のファイルベースの一括コピー操作のサポートが公開されます。 **IBCPSession**でインターフェイスが公開されている、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セッションとして同じレベルでの Native Client OLE DB プロバイダー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、データ ソース オブジェクトは、セッション オブジェクトのファクトリと、一括コピー操作は、接続プロパティ SSPROP_ENABLEBULKCOPY で指定されます。 また、SSPROP_ENABLEFASTLOAD プロパティは true に設定する必要があります。  
  
 **IDBCreateSession::CreateSession** メソッドを呼び出すと、**BulkCopySession** オブジェクトが作成されます。 その後、作成された **IBCPSession** オブジェクトの **IBCPSession** インターフェイスとほぼ同じシグネチャを使用して、**IBCPSession** オブジェクト経由で公開されるファイルベースのすべての一括コピー メソッドを呼び出せるようになります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー経由のメモリベースの一括コピー操作をサポートしている、 [IRowsetFastLoad](irowsetfastload-ole-db.md)インターフェイス。  
  
 使用しての詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの一括コピー操作を参照してください[一括コピー操作を実行する](../native-client/features/performing-bulk-copy-operations.md)します。  
  
 使用する方法を示すサンプルについては、 **IBCPSession**インターフェイスは、「 [IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|方法|説明|  
|------------|-----------------|  
|[Ibcpsession::bcpcolfmt &#40;OLE DB&#41;](ibcpsession-bcpcolfmt-ole-db.md)|プログラム変数と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列のバインドを作成します。|  
|[Ibcpsession::bcpcolumns &#40;OLE DB&#41;](ibcpsession-bcpcolumns-ole-db.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル内の列にバインドされるフィールド数を設定します。|  
|[Ibcpsession::bcpcontrol &#40;OLE DB&#41;](ibcpsession-bcpcontrol-ole-db.md)|一括コピー操作のオプションを設定します。|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信される残りの行をコミットします。|  
|[:Bcpexec &#40;OLE DB&#41;](ibcpsession-bcpexec-ole-db.md)|一括コピー操作を実行します。|  
|[Ibcpsession::bcpinit &#40;OLE DB&#41;](ibcpsession-bcpinit-ole-db.md)|一括コピー構造を初期化し、エラー チェックを実行して、データ ファイルとフォーマット ファイルの名前が正しいことを確認します。その後、それらのファイルを開きます。|  
|[Ibcpsession::bcpreadfmt &#40;OLE DB&#41;](ibcpsession-bcpreadfmt-ole-db.md)|フォーマット ファイルから列ごとにフォーマット情報を読み取ります。|  
|[Ibcpsession::bcpwritefmt &#40;OLE DB&#41;](ibcpsession-bcpwritefmt-ole-db.md)|フォーマット ファイルに列ごとのフォーマット情報を書き込みます。|  
  
## <a name="see-also"></a>関連項目  
 [インターフェイス&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
