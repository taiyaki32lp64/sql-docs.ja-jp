---
title: PRINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc83aca49b6147835353538d809be121756ecda6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072398"
---
# <a name="print-transact-sql"></a>PRINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  ユーザー定義メッセージをクライアントに返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>引数  
 *msg_str*  
 文字列または Unicode 文字列の定数です。 詳細については、「[定数 &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)」を参照してください。  
  
 **@** *local_variable*  
 任意の有効な文字型の変数を指定します。 **@** _local\_variable_ は、**char**、**nchar**、**varchar**、または **nvarchar** であるか、これらのデータ型に暗黙的に変換できる必要があります。  
  
 *string_expr*  
 文字列を返す式を指定します。 連結したリテラル値、関数、および変数を含むことができます。 詳細については、「[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 メッセージ文字列は、Unicode 以外の文字列の場合は 8,000 バイトまで指定でき、Unicode 文字列の場合は 4,000 バイトまで指定できます。 これより長い文字列は切り詰められます。 **Varchar (max)** と **nvarchar (max)** データ型は、**varchar(8000)** および **nvarchar(4000)** ではなくなったデータ型に切り詰められます。  
  
 RAISERROR を使用してメッセージを返すこともできます。 RAISERROR には、PRINT にはない次のような利点があります。  
  
-   RAISERROR は、エラー メッセージ文字列への引数の置き換えをサポートします。この置き換えでは、C 言語標準ライブラリの printf 関数をモデルにしたメカニズムを使用します。  
  
-   RAISERROR では、テキスト メッセージに加えて、一意のエラー番号、重大度、および状態コードを指定できます。  
  
-   RAISERROR は、sp_addmessage システム ストアド プロシージャを使用して作成したユーザー定義メッセージを返すために使用できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-conditionally-executing-print-if-exists"></a>A. 条件付きで PRINT を実行する (IF EXISTS)  
 次の例では、`PRINT` ステートメントを使用して条件に応じてメッセージを返します。  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. 文字列を構築して表示する  
 次の例では、`GETDATE` 関数の結果を `nvarchar` データ型に変換し、リテラル テキストと連結して `PRINT` で返します。  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. 条件付きで PRINT を実行する  
 次の例では、`PRINT` ステートメントを使用して条件に応じてメッセージを返します。  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

