---
title: database_scoped_configurations (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da115c8d4cf48cfbcd6190c88a83bee4e61ae5a1
ms.sourcegitcommit: 27c267bf2a3cfaf2abcb5f3777534803bf4cffe5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240768"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>database_scoped_configurations (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

構成ごとに1行の値を格納します。 

|列名|データ型|Description|
|-----------------|---------------|-----------------|
|**configuration_id**|**int**|構成オプションの ID。|
|**name**|**nvarchar(60)**|構成オプションの名前。 使用可能な構成の詳細については、「 [ALTER DATABASE &#40;スコープ&#41;構成 transact-sql](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)」を参照してください。|
|**value**|**sqlvariant**|プライマリレプリカのこの構成オプションに設定された値。|
|**value_for_secondary**|**sqlvariant**|セカンダリレプリカのこの構成オプションに設定された値。|
|**is_value_default**|**bit** |値が既定値に設定されているかどうかを指定します。|

## <a name="Permissions"></a> アクセス許可

ロール **public** のメンバーシップが必要です。

## <a name="remarks"></a>備考

**Value_for_secondary**の値として NULL が返された場合、セカンダリがプライマリに設定されていることを意味します。
 
データベース スコープ構成設定はデータベースで継承されます。 つまり、特定のデータベースが復元されたり、アタッチされたりしたとき、既存の構成設定が残ります。

## <a name="see-also"></a>「

[ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
