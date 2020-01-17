---
title: sys.external_languages (TRANSACT-SQL) - SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1cef52f066a07032240d17f88297b02ba3f7e5fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65995120"
---
# <a name="sysexternal_languages-transact-sql"></a>sys.external_languages (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このカタログ ビューでは、データベースの外部の言語の一覧を示します。 **R** と **Python** は予約済みの名前であり、それらの特定の名前で外部言語を作成することはできません。

## <a name="sysexternal_languages"></a>sys.external_languages

カタログ ビューの sys.external_languages には、データベースの外部の言語ごとに 1 行が一覧表示します。

|列名 |データ型 | 説明|
|------|------|------|
|external_language_id |int | 外部の言語の ID|
|language |sysname |外部の言語の名前。 データベース内で一意です。 R と Python がインスタンスあたりの予約済みの名前|
|create_date |datetime2 |作成の日付と時刻|
|principal_id |int |この外部ライブラリを所有するプリンシパルの ID|

## <a name="see-also"></a>関連項目  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [外部の言語を作成します。](../../t-sql/statements/create-external-language-transact-sql.md) 
