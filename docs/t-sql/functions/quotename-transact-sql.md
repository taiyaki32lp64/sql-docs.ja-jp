---
title: QUOTENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUOTENAME_TSQL
- QUOTENAME
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 761e6f43f1199d4eb16060cd769a30ebba220ef8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914255"
---
# <a name="quotename-transact-sql"></a>QUOTENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Unicode 文字列に区切り記号を追加して返すことで、入力文字列から区切り記号で囲まれた有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子を作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>引数  
 '*character_string*'  
 Unicode 文字データの文字列を指定します。 *character_string* は **sysname** 128 文字までに制限されます。 128 文字を超える文字を入力すると、NULL が返されます。  
  
 '*quote_character*'  
 区切り記号として使用する 1 つの文字を指定します。 単一引用符 ( **'** )、左または右の角かっこ ( **[]** )、二重引用符 ( **"** )、左または右のかっこ ( **()** )、大なりまたは小なり記号 ( **><** )、左または右の中かっこ ( **{}** )、またはバッククォート ( **\`** ) を指定できます。 使用できない文字が指定された場合は、NULL が返されます。 *quote_character* を指定しない場合は、角かっこが使用されます。  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar(258)**  
  
## <a name="examples"></a>使用例  
 次の例では、文字列 `abc[]def` を受け取り、`[` 文字と `]` 文字を使用して、区切り記号で囲まれた有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子を作成します。  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 文字列 `abc[]def` 内の右角かっこが 2 つ続いてエスケープ文字を表していることに注意してください。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、文字列 `abc def` を受け取り、`[` 文字と `]` 文字を使用して、区切り記号で囲まれた有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子を作成します。  
  
```  
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [PARSENAME &#40;Transact-SQL&#41;](../../t-sql/functions/parsename-transact-sql.md)  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

