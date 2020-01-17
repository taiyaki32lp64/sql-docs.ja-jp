---
title: トランザクション |Microsoft Docs
description: OLE DB Driver for SQL Server でのトランザクション
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 8fc245cebdb106eb81af8c5ae1fba6a2bcc041b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015227"
---
# <a name="transactions"></a>トランザクション
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 用の OLE DB ドライバーは、ローカルトランザクションサポートを実装します。 コンシューマーは、MS DTC (Microsoft 分散トランザクション コーディネーター) を使用して、分散トランザクションまたはコーディネートされたトランザクションを使用できます。 複数のセッションにまたがってトランザクションを制御する必要があるコンシューマーの場合、OLE DB Driver for SQL Server を使用して、MS DTC によって起動および管理されるトランザクションを結合できます。  
  
 OLE DB Driver for SQL Server では、既定で自動コミット トランザクション モードが使用されます。このモードでは、コンシューマー セッションでの個々の操作が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに対する 1 つの完全なトランザクションを構成します。 OLE DB Driver for SQL Server の自動コミット モードはローカルなモードなので、自動コミット トランザクションが複数のセッションにまたがることはありません。  
  
 OLE DB Driver for SQL Server で公開される **ITransactionLocal** インターフェイスにより、コンシューマーは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに対する 1 つの接続で、明示的および暗黙的に開始されたトランザクションを使用できます。 SQL Server の OLE DB ドライバーでは、入れ子になったローカルトランザクションはサポートされていません。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ローカル トランザクションのサポート](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [分散トランザクションのサポート](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [分離レベル&#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のプログラミング](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
