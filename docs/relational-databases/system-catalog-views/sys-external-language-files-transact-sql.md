---
title: sys.external_language_files (TRANSACT-SQL) - SQL Server |Microsoft Docs
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
ms.openlocfilehash: 0d1325311ef0b708f5a3abd5f4494e099863efc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65995090"
---
# <a name="sysexternal_language_files-transact-sql"></a>sys.external_language_files (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このカタログ ビューでは、データベース内の外部の言語拡張機能ファイルの一覧を示します。 **R** と **Python** は予約済みの名前であり、それらの特定の名前で外部言語を作成することはできません。

外部の言語が、file_spec から作成されると、拡張機能自体とそのプロパティがこのビューで表示します。 このビューは、OS ごとに、言語ごとに 1 つのエントリが含まれます。

## <a name="sysexternal_languages"></a>sys.external_languages

カタログ ビューの sys.external_language_files には、データベース内の各外部言語拡張機能の行が一覧表示します。 パラメーター

|列名 |データ型 | 説明|
|------|------|------|
|external_language_id |int | 外部の言語の ID|
|コンテンツ|varbinary(max) |外部の言語拡張機能のファイルの内容|
|file_name|nvarchar(266)|言語拡張機能のファイルの名前|
|プラットフォーム|TINYINT|SQL Server がインストールされているホスト プラットフォームの ID|
|platform_desc |nvarchar(60)|ホストのプラットフォームの名前です。 有効な値は、'WINDOWS'、'LINUX' です。|
|パラメーター|nvarchar (4000)|外部の言語のパラメーター|
|environment_variables |nvarchar (4000)|外部の言語環境変数|

## <a name="see-also"></a>関連項目  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [外部の言語を作成します。](../../t-sql/statements/create-external-language-transact-sql.md)  
