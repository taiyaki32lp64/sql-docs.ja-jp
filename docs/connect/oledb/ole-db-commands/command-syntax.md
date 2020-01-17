---
title: コマンド構文 |Microsoft Docs
description: コマンドの構文とストアドプロシージャ
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 15d6d221c9e3435a3ba4c3f58c7d6b6e55314f29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016123"
---
# <a name="command-syntax"></a>コマンドの構文
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server は、DBGUID_SQL マクロで指定されたコマンド構文を認識します。 OLE DB Driver for SQL Server の場合、指定子は、ODBC SQL、ISO、および[!INCLUDE[tsql](../../../includes/tsql-md.md)]の混在が有効な構文であることを示します。 たとえば、次の SQL ステートメントでは、ODBC SQL のエスケープ シーケンスを使用して、LCASE 文字列関数を指定しています。  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 関数は、大文字をすべて小文字に変換した文字列を返します。 ISO の文字列関数 LOWER も同じ操作を実行します。つまり、次の SQL ステートメントは、上記の ODBC ステートメントと同義の ISO ステートメントになります。  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 OLE DB Driver for SQL Server では、どちらの形式のステートメントも、コマンドのテキストとして指定された際には、正常に処理されます。  
  
## <a name="stored-procedures"></a>ストアド プロシージャ  
 OLE DB Driver for SQL Server のコマンドを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ストアド プロシージャを実行するときには、コマンド テキストで ODBC CALL エスケープ シーケンスを使用します。 この操作を行うと、OLE DB Driver for SQL Server では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のリモート プロシージャ コールのメカニズムを使用して、コマンド処理が最適化されます。 たとえば次のような場合、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメント形式ではなく、ODBC SQL ステートメントをコマンド テキストとして使用することをお勧めします。  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>参照  
 [[コマンド]](../../oledb/ole-db-commands/commands.md)  
  
  
