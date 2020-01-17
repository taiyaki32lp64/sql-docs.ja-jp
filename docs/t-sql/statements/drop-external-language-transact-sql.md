---
title: DROP EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3767bec1807b68df3eb3f82287a5c871d653a286
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892986"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

既存の外部言語を削除します。

## <a name="syntax"></a>構文

```text
DROP EXTERNAL LANGUAGE <language_name>
```

### <a name="arguments"></a>引数

**language_name**

言語は、データベース スコープのオブジェクトです。 言語名は、データベース内で一意であることが必要です。

## <a name="permissions"></a>アクセス許可

言語を削除するには、ALTER ANY EXTERNAL LANGUAGE の特権が必要です。 既定では、すべてのデータベース所有者またはオブジェクトの所有者も、外部言語を削除することができます。

> [!NOTE]
> 外部言語を削除する前に、その外部言語を参照している外部ライブラリを削除する必要があることに注意してください。

### <a name="return-values"></a>戻り値

ステートメントが成功した場合は、情報メッセージが返されます。

## <a name="remarks"></a>Remarks

外部言語を削除するには、その前に、指定した言語に対するすべての外部ライブラリを削除する必要があります。

## <a name="examples"></a>使用例

外部言語 **Java** を作成します。

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

外部言語を削除します。

```sql
DROP EXTERNAL LANGUAGE Java;
```

## <a name="see-also"></a>参照

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
