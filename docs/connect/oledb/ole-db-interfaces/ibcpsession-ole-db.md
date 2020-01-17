---
title: IBCPSession (OLE DB) |Microsoft Docs
description: IBCPSession インターフェイス (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 73f8fd440903c525856475200921f97a25d9b27b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015511"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **IBCPSession** インターフェイスでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のファイルベースの一括コピー操作のサポートが公開されます。 **Ibcpsession**インターフェイスは、セッションと同じレベルにある SQL Server の OLE DB ドライバーで公開されます。 OLE DB Driver for SQL Server では、データ ソース オブジェクトは Session オブジェクトのファクトリであり、一括コピー操作は接続プロパティ SSPROP_ENABLEBULKCOPY で指定されます。 また、SSPROP_ENABLEFASTLOAD プロパティは true に設定する必要があります。  
  
 **IDBCreateSession::CreateSession** メソッドを呼び出すと、**BulkCopySession** オブジェクトが作成されます。 その後、作成された **IBCPSession** オブジェクトの **IBCPSession** インターフェイスとほぼ同じシグネチャを使用して、**IBCPSession** オブジェクト経由で公開されるファイルベースのすべての一括コピー メソッドを呼び出せるようになります。  
  
> [!NOTE]  
>  OLE DB Driver for SQL Server では、[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) インターフェイス経由でのメモリベースの一括コピー操作がサポートされます。  
  
 OLE DB ドライバーを使用した一括コピー操作の SQL Server の詳細については、「[一括コピー操作の実行](../../oledb/features/performing-bulk-copy-operations.md)」を参照してください。  
  
 **Ibcpsession**インターフェイスの使用方法を示すサンプルについては、「 [Ibcpsession:: bcpdone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|方法|[説明]|  
|------------|-----------------|  
|[IBCPSession:: BCPColFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|プログラム変数と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列のバインドを作成します。|  
|[IBCPSession:: BCPColumns &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブル内の列にバインドされるフィールド数を設定します。|  
|[IBCPSession:: BCPControl &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|一括コピー操作のオプションを設定します。|  
|[IBCPSession:: BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信される残りの行をコミットします。|  
|[IBCPSession:: BCPExec &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|一括コピー操作を実行します。|  
|[IBCPSession:: BCPInit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|一括コピー構造を初期化し、エラー チェックを実行して、データ ファイルとフォーマット ファイルの名前が正しいことを確認します。その後、それらのファイルを開きます。|  
|[IBCPSession:: BCPReadFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|フォーマット ファイルから列ごとにフォーマット情報を読み取ります。|  
|[IBCPSession:: BCPWriteFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|フォーマット ファイルに列ごとのフォーマット情報を書き込みます。|  
  
## <a name="see-also"></a>参照  
 [インターフェイス&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
  
  
