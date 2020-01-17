---
title: DBCC SHRINKLOG (Parallel Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d2cf30f4f01a30d8171e58cce3052e45fefa6179
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930316"
---
# <a name="dbcc-shrinklog-parallel-data-warehouse"></a>DBCC SHRINKLOG (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

現在の [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベースの "*アプライアンス全体*" でトランザクション ログのサイズを減らします。 トランザクション ログの圧縮するのには、データを最適化します。 時間の経過と共に、データベースのトランザクション ログは、断片化され非効率的になります。 断片化を軽減し、ログのサイズを小さくするには、DBCC SHRINKLOG を使用します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>引数  
SIZE = { *target_size* [ MB | **GB** | TB ]  } | **DEFAULT**.  
*target_size* は、DBCC SHRINKLOG が完了した後、すべての計算ノード全体のトランザクション ログの望ましいサイズです。 0 より大きい整数です。  
ログのサイズは、メガバイト (MB)、ギガバイト (GB)、またはテラバイト (TB) で測定されます。 すべてのコンピューティング ノードの上のトランザクション ログの合計サイズです。  
既定では、DBCC SHRINKLOG によりトランザクション ログはデータベースのメタデータに格納されているログ サイズに縮小されます。 メタデータのログ サイズは、[CREATE DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) または [ALTER DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) の LOG_SIZE パラメーターによって決まります。 DBCC SHRINKLOG は、`SIZE=DEFAULT` が指定されている場合、または `SIZE` 句が省略されている場合、トランザクション ログのサイズを既定サイズに縮小します。
  
WITH NO_INFOMSGS  
情報メッセージは、DBCC SHRINKLOG の結果に表示されません。  
  
## <a name="permissions"></a>アクセス許可  
ALTER SERVER STATE アクセス許可が必要です。
  
## <a name="general-remarks"></a>全般的な解説  
DBCC SHRINKLOG では、データベースのメタデータに格納されているログのサイズは変更されません。 メタデータには引き続き CREATE DATABASE または ALTER DATABASE ステートメントで指定された LOG_SIZE パラメーターが含まれます。
  
## <a name="examples"></a>使用例 
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. トランザクション ログを CREATE DATABASE で指定された元のサイズに圧縮します。  
Addresses データベースが作成されたとき、Addresses データベースのトランザクション ログは 100 MB に設定されたものとします。 つまり、Addresses の CREATE DATABASE ステートメントは LOG_SIZE = 100 MB に設定されていました。 ここでは、ログが 150 MB に増えたので、100 MB に戻すものとします。
  
次の各ステートメントでは、Addresses データベースのトランザクション ログを 100 MB の既定サイズに圧縮します。 100 MB にログを圧縮するとデータ損失が発生する場合、DBCC SHRINKLOG は、データが失われない、100 MB より大きい最小サイズにログを縮小します。
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
