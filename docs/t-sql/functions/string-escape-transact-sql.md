---
title: STRING_ESCAPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 7e9b189d6b06aaf3b85815ed6d889756d466bff8
ms.sourcegitcommit: a92fa97e7d3132ea201e4d86c76ac39cd564cd3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2019
ms.locfileid: "75325504"
---
# <a name="string_escape-transact-sql"></a>STRING_ESCAPE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

テキストの特殊文字をエスケープし、エスケープ文字付きのテキストを返します。 **STRING_ESCAPE** は SQL Server 2016 で導入された決定的関数です。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>引数

 *text*  
 エスケープする必要があるオブジェクトを表す **nvarchar**[expression](../../t-sql/language-elements/expressions-transact-sql.md) 式です。  
  
 *type*  
 適用される規則をエスケープします。 現在サポートされている値は `'json'` です。  
  
## <a name="return-types"></a>戻り値の型

 エスケープされた特殊文字と制御文字を含む **nvarchar (max)** テキスト。 現在、**STRING_ESCAPE** は次の表に示すように JSON 特殊文字のみをサポートします。  
  
|特殊文字|エンコードされたシーケンス|  
|-----------------------|----------------------|  
|引用符 (")|\\"|  
|逆斜線 (\\)| \\\\ |  
|斜線 (/)|\\/|  
|バックスペース|\b|  
|改ページ|\f|  
|改行|\n|  
|キャリッジ リターン|\r|  
|水平タブ|\t|  
  
|制御文字|エンコードされたシーケンス|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>解説  
  
## <a name="examples"></a>例  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  JSON 形式の規則に従ってテキストをエスケープする

 次のクエリでは、JSON の規則を使用して特殊文字をエスケープし、エスケープされたテキストを返します。  
  
```sql
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>B. JSON オブジェクトの書式設定

 次のクエリでは、数値変数と文字列変数から JSON テキストを作成し、変数内の任意の JSON 特殊文字をエスケープします。  
  
```
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>参照

 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
