---
title: テーブル値パラメーター (OLE DB) |Microsoft Docs
description: テーブル値パラメーター (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 3f942130244aaf08d533ac4a1abdc1752971209d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015270"
---
# <a name="table-valued-parameters-ole-db"></a>テーブル値パラメーター (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  ここでは、SQL Server 用の OLE DB ドライバーでのテーブル値パラメーターのサポートについて説明します。 詳細については、「[テーブル値パラメーター &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)」を参照してください。 サンプルについては、「[テーブル値パラメーター &#40;の&#41;使用 OLE DB](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 現時点では、複数行データを、パラメーター セット (**ICommand::Execute** の DBPARAMS パラメーター) と共にプロシージャのパラメーターとしてサーバーに送信できます。 パラメーター セットを使用する場合、セットの各要素は、個別のリモート プロシージャ コール (RPC) の要求でサーバーに送信する必要があります。 テーブル値パラメーターの機能は似ていますが、サーバーとの統合はより緊密になっています。 これにより、RPC 要求の数が減少し、サーバーでセットベースの操作が可能になります。  
  
 テーブル値パラメーターは OLE DB**行セット**オブジェクトとして SQL Server の OLE DB ドライバーでサポートされています。 どの**行セット** オブジェクトも、コンシューマー (つまり、OLE DB Driver for SQL Server を使用するクライアント アプリケーション) によってテーブル値パラメーターのプレースホルダーとして指定されます。 テーブル値パラメーターは、他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パラメーターの型と同じように扱われます。 SQL Server の OLE DB ドライバーは、作成、検出、仕様、バインド、およびスキーマの各インターフェイスを提供します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [テーブル値パラメーターの行セットの作成](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [テーブル値パラメーターの型探索](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [テーブル値パラメーターを含むコマンドの実行](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [テーブル値パラメーターへのデータの挿入](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [OLE DB テーブル値パラメーター向けに変更されたスキーマ行セット](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB テーブル値パラメーターの型のサポート](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB テーブル値パラメーターの型のサポート (メソッド)](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB テーブル値パラメーターの型のサポート (プロパティ)](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のプログラミング](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
