---
title: DROP WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 5db3c50e4b0a21e2e1acf9512995870b62375dd8
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632833"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

既存のユーザー定義のワークロード管理分類子を削除します。  要求が実行されている場合、または要求キュー内で中断状態にある場合、要求の分類は維持されるので、分類子をすぐに削除することができます。 重要度が異なる分類子を削除および再作成することは、既に分類済みの要求に影響しません。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>構文  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>引数

*classifier_name*  
ワークロード分類子を識別する名前を指定します。
  
## <a name="permissions"></a>アクセス許可

CONTROL DATABASE アクセス許可が必須です。  
  
## <a name="examples"></a>使用例

次の例では、`wgcELTROLE` という名前のワークロード分類子が削除されます。  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> 送信された要求に一致する分類子が存在しない場合、それは既定のワークロード グループに分類されます。  既定のワークロード グループは、smallrc リソース クラスです。
  
## <a name="see-also"></a>参照

[CREATE WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[SQL Data Warehouse のワークロード分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
