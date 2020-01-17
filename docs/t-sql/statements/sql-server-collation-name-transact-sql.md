---
title: SQL Server 照合順序名 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e867584c9c9a0e50022d0964a1772ac2c3a1b1e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099985"
---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 照合順序名 (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の照合順序名を指定する単一の文字列です。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Windows 照合順序をサポートします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が Windows 照合順序をサポートする前に開発された、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序と呼ばれる、限られた数 (<80) の照合順序をサポートしています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序は旧バージョンとの互換性を維持するためにサポートされていますが、新規の開発作業に使用しないでください。 Windows 照合順序の詳細については、[Windows 照合順序名](../../t-sql/statements/windows-collation-name-transact-sql.md)に関するページをご覧ください。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
<SQL_collation_name> :: =
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>

<ComparisonStyle> ::=
_CaseSensitivity_AccentSensitivity | _BIN
```

## <a name="arguments"></a>引数

*SortRules* 辞書順での並べ替えを指定した場合に適用される、並べ替え規則を持つアルファベットまたは言語を示す文字列です。 たとえば、Latin1_General や Polish などが挙げられます。

**Pref** 大文字優先を指定します。 比較が大文字と小文字の場合でも、その他の区別がないときは、文字の大文字バージョンが並べ替えられてから小文字バージョンが並べ替えられます。

*Codepage* 照合順序で使用されるコード ページを識別する 1 から 4 桁の番号を指定します。 **CP1** はコード ページ 1252 を示します。他のすべてのコード ページの場合は、完全なコード ページ番号を指定します。 たとえば、**CP1251** はコード ページ 1251 を示し、**CP850** はコード ページ 850 を示します。

*CaseSensitivity*
**CI** を指定すると大文字小文字は区別されず、**CS** を指定すると大文字小文字が区別されます。

*AccentSensitivity*
**AI** を指定するとアクセントは区別されず、**AS** を指定するとアクセントが区別されます。

**BIN** 使用するバイナリ並べ替え順を指定します。

## <a name="remarks"></a>Remarks

現在のサーバーでサポートされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の一覧を表示するには、次のクエリを実行します。

```sql
SELECT * FROM sys.fn_helpcollations()
WHERE name LIKE 'SQL%';
```

> [!NOTE]
> 並べ替え順 ID 80 では、コード ページ 1250 およびバイナリ順の任意の Window 照合順序を使用します。 例:Albanian_BIN、Croatian_BIN、Czech_BIN、Romanian_BIN、Slovak_BIN、Slovenian_BIN。

## <a name="see-also"></a>参照

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [定数](../../t-sql/data-types/constants-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [テーブル](../../t-sql/data-types/table-transact-sql.md)
- [sys.fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
