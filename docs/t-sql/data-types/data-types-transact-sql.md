---
title: データ型 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a03da24fe18f0d910f5054d8cfb321c42d633db8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113740"
---
# <a name="data-types-transact-sql"></a>データ型 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、列、ローカル変数、式、パラメーターのそれぞれに、関連するデータ型があります。 データ型は、整数データ、文字データ、通貨データ、日時データ、バイナリ文字列など、オブジェクトが保持できるデータの種類を示す属性です。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、システム データ型のセットが用意されており、ここに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用可能なデータ型がすべて定義されています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] または [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] で、ユーザー独自のデータ型を定義することもできます。 別名データ型は、システムが提供するデータ型に基づいています。 別名データ型について詳しくは、「[CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)」をご覧ください。 ユーザー定義型の特性は、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] でサポートされるプログラミング言語の 1 つを使用して作成するクラスのメソッドと演算子によって決まります。
  
データ型、照合順序、有効桁数、小数点以下桁数、または長さが異なる 2 つの式を演算子で結合する場合、結果の特性は次のように決まります。
-   結果のデータ型は、入力式のデータ型のうち優先順位が高いほうになります。 詳細については、「[データ型の優先順位 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)」を参照してください。  
-   結果の照合順序は、データ型が **char**、**varchar**、**text**、**nchar**、**nvarchar**、または **ntext** の場合は、照合順序の優先順位の規則によって決まります。 詳細については、「[照合順序の優先順位 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)」を参照してください。  
-   結果の有効桁数、小数点以下桁数、長さは、入力式の精度、桁数、長さによって決まります。 詳しくは、「[有効桁数、小数点以下桁数、および長さ &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)」をご覧ください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ISO との互換性を保つためにデータ型のシノニムが用意されています。 詳しくは、「[データ型のシノニム &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md)」をご覧ください。
  
## <a name="data-type-categories"></a>データ型のカテゴリ
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型は、次のカテゴリに分類されます。
  
|||  
|-|-|  
|真数|Unicode 文字列|  
|概数|バイナリ文字列|  
|日付と時刻|その他のデータ型|  
|文字列||  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では一部のデータ型は、格納の特性に基づいて次のグループに分けられます。
-   大きな値データ型: **varchar(max)** 、**nvarchar(max)**  
-   ラージ オブジェクト データ型: **text**、**ntext**、**image**、**varbinary(max)** 、**xml**  
  
    > [!NOTE]  
    >  sp_help は、大きな値および **xml** を受け取るデータ型の長さとして -1 を返します。  
  
### <a name="exact-numerics"></a>真数
  
|||  
|-|-|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|[smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)||  
  
### <a name="approximate-numerics"></a>概数
  
|||  
|-|-|  
|[float](../../t-sql/data-types/float-and-real-transact-sql.md)|[real](../../t-sql/data-types/float-and-real-transact-sql.md)|  
  
### <a name="date-and-time"></a>日付と時刻
  
|||  
|-|-|  
|[date](../../t-sql/data-types/date-transact-sql.md)|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|[time](../../t-sql/data-types/time-transact-sql.md)|  
  
### <a name="character-strings"></a>文字列
  
|||  
|-|-|  
|[char](../../t-sql/data-types/char-and-varchar-transact-sql.md)|[varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|[text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="unicode-character-strings"></a>Unicode 文字列
  
|||  
|-|-|  
|[nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|[nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
|[ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="binary-strings"></a>バイナリ文字列
  
|||  
|-|-|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|[image](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="other-data-types"></a>その他のデータ型
  
|||  
|-|-|  
|[cursor](../../t-sql/data-types/cursor-transact-sql.md)|[rowversion](../../t-sql/data-types/rowversion-transact-sql.md)|  
|[hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)|  
|[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)|[xml](../../t-sql/xml/xml-transact-sql.md)|  
|[空間 geometry 型](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) |[空間 geography 型](../../t-sql/spatial-geography/spatial-types-geography.md)|  
|[テーブル](../../t-sql/data-types/table-transact-sql.md) | |
  
## <a name="see-also"></a>参照
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[関数 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  
