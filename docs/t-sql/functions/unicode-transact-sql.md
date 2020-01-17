---
title: UNICODE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UNICODE
- UNICODE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first character of input expression [SQL Server]
- UNICODE function
- Unicode [SQL Server], UNICODE function
ms.assetid: 5e3c40b2-8401-4741-9f2a-bae70eaa4da6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 29a9476f5835df326aa34d8ccfc4cc6d22ea7e3f
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670612"
---
# <a name="unicode-transact-sql"></a>UNICODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Unicode 標準に定義された、入力式の先頭文字の整数値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
UNICODE ( 'ncharacter_expression' )  
```  
  
## <a name="arguments"></a>引数  
**'** *ncharacter_expression* **'**  
**nchar** または **nvarchar** 式です。  
  
## <a name="return-types"></a>戻り値の型  
**int**  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] より前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、UNICODE 関数で 000000 ～ 00FFFF の範囲の UCS-2 コードポイントが返されます。これにより、Unicode Basic Multilingual Plane (BMP) で 65,535 文字を表現できます。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降、[補助文字 (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) が有効になっている照合順序を使用すると、UNICODE では 000000 から 10FFFF の範囲の UTF-16 コードポイントが返されます。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]の Unicode サポートの詳細については、[照合順序および Unicode サポートに関するページ](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn)を参照してください。 
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-unicode-and-the-nchar-function"></a>A. UNICODE 関数と NCHAR 関数を使用する  
 次の例では、`UNICODE` と `NCHAR` の各関数を使用して、文字列 `Åkergatan` 24 の先頭文字を表す UNICODE 値と実際の先頭文字 `Å` を出力します。  
  
```sql  
DECLARE @nstring nchar(12);  
SET @nstring = N'Åkergatan 24';  
SELECT UNICODE(@nstring), NCHAR(UNICODE(@nstring));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
197         Å  
```  
  
### <a name="b-using-substring-unicode-and-convert"></a>B. SUBSTRING、UNICODE、CONVERT を使用する  
 次の例では、`SUBSTRING`、`UNICODE`、および `CONVERT` の各関数を使用して、文字列 `Åkergatan 24` の各文字の文字番号、Unicode 文字、および UNICODE 値を出力します。  
  
```sql  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(12);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.   
-- Notice that there is an N before the start of the string, which   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'Åkergatan 24';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= LEN(@nstring)  
-- While these are still characters in the character string,  
   BEGIN;  
   SELECT @position,   
      CONVERT(char(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1));  
   SELECT @position = @position + 1;  
   END;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ----------------- -----------   
1           Å                 197           
  
----------- ----------------- -----------   
2           k                 107           
  
----------- ----------------- -----------   
3           e                 101           
  
----------- ----------------- -----------   
4           r                 114           
  
----------- ----------------- -----------   
5           g                 103           
  
----------- ----------------- -----------   
6           a                 97            
  
----------- ----------------- -----------   
7           t                 116           
  
----------- ----------------- -----------   
8           a                 97            
  
----------- ----------------- -----------   
9           n                 110           
  
----------- ----------------- -----------   
10                            32            
  
----------- ----------------- -----------   
11          2                 50            
  
----------- ----------------- -----------   
12          4                 52  
```  
  
## <a name="see-also"></a>参照  
 [ASCII &#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [CHAR &#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

