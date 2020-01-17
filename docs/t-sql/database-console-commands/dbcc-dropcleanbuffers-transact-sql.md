---
title: DBCC DROPCLEANBUFFERS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a3b2d2ff81fddaae0b0ae68da9d4477819a61073
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101934"
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

バッファー プールのクリーン バッファーと、列ストア オブジェクト プールの列ストア オブジェクトをすべて削除します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文
SQL Server の構文: 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Azure SQL Warehouse と Parallel Data Warehouse の構文:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
 WITH NO_INFOMSGS  
 すべての情報メッセージを表示しないようにします。 情報メッセージは通常、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] と [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] では表示されません。  
  
 COMPUTE  
 各計算ノードからメモリ内のデータ キャッシュを消去します。  
  
 ALL  
 制御ノードから、および各計算ノードからメモリ内のデータ キャッシュを消去します。 値を指定しない場合、これが既定値になります。  
  
## <a name="remarks"></a>Remarks  
サーバーのシャットダウンと再起動を行わずに、コールド バッファー キャッシュの状態でクエリをテストする場合は、DBCC DROPCLEANBUFFERS を使用します。
バッファー プールのクリーン バッファーと列ストア オブジェクト プールの列ストア オブジェクトを削除するには、まず CHECKPOINT を使用してコールド バッファー キャッシュを作成します。 これで、現在のデータベースのすべてのダーティ ページがディスクに書き込まれ、バッファーが削除されます。 その後、DBCC DROPCLEANBUFFERS コマンドを実行してバッファー プールからバッファーを削除します。
  
## <a name="result-sets"></a>結果セット  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の DBCC DROPCLEANBUFFERS では次の結果が返されます。
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  

適用対象:SQL Server、Parallel Data Warehouse 

- **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  

適用対象:Azure SQL Data Warehouse

- DB_OWNER 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
