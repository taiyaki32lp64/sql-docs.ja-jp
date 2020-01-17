---
title: メタデータの検出 |Microsoft Docs
description: OLE DB Driver for SQL Server でのメタデータの検出
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9891e5708110be83a4ef33cb2a142accaf93ffe2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989063"
---
# <a name="metadata-discovery"></a>メタデータの検出
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ではメタデータ検出機能が強化されているため、OLE DB Driver for SQL Server アプリケーションでは、クエリの実行によって返された列またはパラメーター メタデータがクエリの実行前に指定したメタデータ形式と同じであるか、その形式と互換性があることを確認できます。 クエリの実行後に返されたメタデータにクエリの実行前に指定したメタデータ形式との互換性がない場合は、エラーが発生します。  
  
 bcp 関数と IBCPSession および IBCPSession2 インターフェイスでは、遅延読み取り (遅延メタデータ検出) を指定して、クエリ出力操作でメタデータ検出を回避できます。 その結果、パフォーマンスが向上し、メタデータ検出のエラーを回避できます。  
  
 OLE DB Driver for SQL Server を使用してアプリケーションを開発し、[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] より前のバージョンのサーバーに接続する場合、メタデータ検出機能はそのバージョンのサーバーに対応したものとなります。  
  
## <a name="remarks"></a>Remarks   
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] では次の OLE DB メンバー関数が機能強化され、メタデータ検出機能が向上しています。  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters:: GetParameterInfo (詳細については、 [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md)を参照してください)  
  
 IBCPSession::BCPSetBulkMode を使用してメタデータ形式を指定したときのパフォーマンスも向上しています。  
  
 で[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]は、次の2つのストアドプロシージャが追加されるため、OLE DB Driver for SQL Server でのメタデータ検出機能が向上しています。  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server の機能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
