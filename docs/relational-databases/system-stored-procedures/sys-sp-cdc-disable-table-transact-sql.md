---
title: sys.sp_cdc_disable_table (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_disable_table
- sp_cdc_disable_table
- sys.sp_cdc_disable_table_TSQL
- sp_cdc_disable_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_table
- sys.sp_cdc_disable_table
- change data capture [SQL Server], disabling tables
ms.assetid: da2156c0-504e-4d76-b9a0-4448becf9bda
author: rothja
ms.author: jroth
ms.openlocfilehash: 693c449679433b733cfc3a45e2bbedf3f1d92185
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106509"
---
# <a name="sysspcdcdisabletable-transact-sql"></a>sys.sp_cdc_disable_table (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  変更データ キャプチャの現在のデータベース内の指定したソース テーブルとキャプチャ インスタンスを無効にします。 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @source_schema = ] 'source\_schema'` ソース テーブルが含まれているスキーマの名前です。 *source_schema*は**sysname**、既定値はありません、NULL にすることはできません。  
  
 *source_schema*現在のデータベースに存在する必要があります。  
  
`[ @source_name = ] 'source\_name'` 変更データ キャプチャが無効にするのには、ソース テーブルの名前です。 *source_name*は**sysname**、既定値はありません、NULL にすることはできません。  
  
 *source_name*現在のデータベースに存在する必要があります。  
  
`[ @capture_instance = ] 'capture\_instance' | 'all'` 指定したソース テーブルで無効にするキャプチャ インスタンスの名前です。 *capture_instance*は**sysname** NULL にすることはできません。  
  
 'All' を指定した場合、すべてのキャプチャ インスタンスに対して定義されている*source_name*は無効になります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sys.sp_cdc_disable_table**削除、変更データ キャプチャは、指定したソース テーブルとキャプチャ インスタンスに関連付けられているテーブルおよびシステム関数を変更します。 変更データ キャプチャのシステム テーブルとセットから指定されたキャプチャ インスタンスに関連付けられたすべての行を削除、 **is_tracked_by_cdc**列、テーブル内のエントリ、 [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)カタログ ビュー0 を返します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **db_owner**固定データベース ロール。  
  
## <a name="examples"></a>使用例  
 次の例を無効に変更データ キャプチャを`HumanResources.Employee`テーブル。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
