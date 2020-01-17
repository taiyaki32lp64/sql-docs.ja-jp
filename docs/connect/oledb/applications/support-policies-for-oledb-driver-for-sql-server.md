---
title: OLE DB Driver for SQL Server のサポート ポリシー | Microsoft Docs
description: OLE DB Driver for SQL Server のサポート ポリシー
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b02789c787266a3370e3c5c9bfae50ea337d19db
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381859"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server のサポート ポリシー
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  この記事では、さまざまなデータアクセスコンポーネントを OLE DB Driver for SQL Server と共に使用する方法について説明します。  

## <a name="server-support"></a>サーバー サポート  
 OLE DB Driver for SQL Server では、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、および [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] を介した [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] への接続がサポートされています。

## <a name="supported-operating-system-versions"></a>サポートされるオペレーティング システムのバージョン  
 次の表に、SQL Server 用の OLE DB ドライバーをサポートしているオペレーティングシステムを示します。  

| サポートされるオペレーティング システム |  |
|--------------------------------------|---------------------------------|   
| Microsoft Windows 8.1 + [2014 年4月更新](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [4 月2014更新プログラム](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>ADO サポート ポリシー  
 ADO アプリケーションでは、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降の機能を必要としない場合に、Windows に付属している SQLOLEDB OLE DB プロバイダーを使用できます。  

 ADO アプリケーションでは、SQL Server に OLE DB ドライバーを使用できますが、その場合は接続文字列に `DataTypeCompatibility=80` を指定する必要があります。 `DataTypeCompatibility=80` が接続文字列に含まれている場合は、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] の機能しか使用できません。  

## <a name="ole-db-support-policies"></a>OLE DB サポート ポリシー  
アプリケーションは Windows オペレーティング システムに付属している OLE DB プロバイダー (SQLOLEDB) を使用することができます。 ただし、これはメンテナンスモードであり、更新されていません。 代わりに、OLE DB Driver for SQL Server (MSOLEDBSQL) を使用してください。

## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server を使用したアプリケーションの構築](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
