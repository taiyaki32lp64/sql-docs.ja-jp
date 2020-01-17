---
title: sys.sp_cdc_enable_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_enable_db_TSQL
- sp_cdc_enable_db
- sys.sp_cdc_enable_db
- sys.sp_cdc_enable_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_enable_db
- change data capture [SQL Server], enabling databases
- sp_cdc_enable_db
ms.assetid: 176d83b3-493d-43cd-800e-aa123c3bdf17
author: rothja
ms.author: jroth
ms.openlocfilehash: 87cb8f207d85220b88ef00d65fd4704b21becf63
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106504"
---
# <a name="sysspcdcenabledb-transact-sql"></a>sys.sp_cdc_enable_db (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースのデータのキャプチャの変更を有効にします。 データベース内のテーブルの変更データ キャプチャを有効にするには、まずそのデータベースに対してこの手順を実行する必要があります。 変更データ キャプチャ レコードが挿入、更新、および削除の各アクティビティは、変更の詳細を使いやすいリレーショナル形式で使用できるように、有効なテーブルに適用します。 ターゲット環境に変更を適用するために必要なメタデータと共に、変更された行の追跡対象のソース テーブルの列構造を反映した列の情報がキャプチャされます。  
  
> [!IMPORTANT]
>  変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_enable_db  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 変更データ キャプチャを有効にすることはできません[システム データベース](../../relational-databases/databases/system-databases.md)またはディストリビューション データベースです。  
  
 sys.sp_cdc_enable_db を実行すると、メタデータ テーブルや DDL トリガーなど、データベース全体のスコープを持つ変更データ キャプチャ オブジェクトが作成されます。 また、cdc スキーマおよび cdc データベース ユーザーが作成され、内のデータベース エントリの is_cdc_enabled 列を設定、 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)カタログ ビューを 1 にします。  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では変更データ キャプチャです。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_db;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.sp_cdc_disable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
