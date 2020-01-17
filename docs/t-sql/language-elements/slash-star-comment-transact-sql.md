---
title: スラッシュ アスタリスク (ブロック コメント) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- /*...*/_TSQL
- Comment
- /*...*/
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- /*...*/ (comment)
- remarks [SQL Server]
- comments [SQL Server]
ms.assetid: 4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c
author: rothja
ms.author: jroth
ms.openlocfilehash: c1bee651b2dd74564ebaff47add5acd4b62c5018
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121680"
---
# <a name="slash-star-block-comment-transact-sql"></a>スラッシュ アスタリスク (ブロック コメント) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


  ユーザーが入力したテキストを示します。 サーバーが、/* と \*/ で囲まれたテキストを評価することはありません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
/*  
text_of_comment  
*/  
```  
  
## <a name="arguments"></a>引数  
 *text_of_comment*  
 コメントのテキストです。 1 つ以上の文字列です。  
  
## <a name="remarks"></a>Remarks  
 コメントは、単独行に指定したり、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの中に指定できます。 複数行のコメントは、/* と \*/ で示す必要があります。 複数行のコメントで使用されることが多いスタイル規則では、最初の行は /\* で始め、その後に続く行は \*\* で始め、最後は \*/ で終了します。  
  
 コメントの長さには制限がありません。  
  
 入れ子になったコメントを使用できます。 /* 文字パターンが既存のコメント内のどこかに出現した場合、入れ子になったコメントの始まりであると見なされるため、終わりのコメント マーク \*/ が必要です。 終了のコメント マークが存在しない場合は、エラーが生成されます。  
  
 たとえば、次のコードではエラーが生成されます。  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/   
SELECT @@VERSION;  
GO   
```  
  
 このエラーを回避するには、次のように変更してください。  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/ */  
SELECT @@VERSION;  
GO  
  
```  
  
## <a name="examples"></a>使用例  
 次の例では、コード セクションの作業内容を説明するコメントを使用しています。  
  
```  
USE AdventureWorks2012;  
GO  
/*  
This section of the code joins the Person table with the Address table,   
by using the Employee and BusinessEntityAddress tables in the middle to   
get a list of all the employees in the AdventureWorks2012 database   
and their contact information.  
*/  
SELECT p.FirstName, p.LastName, a.AddressLine1, a.AddressLine2, a.City, a.PostalCode  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e ON p.BusinessEntityID = e.BusinessEntityID   
JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
JOIN Person.Address AS a ON ea.AddressID = a.AddressID;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [-- &#40;コメント&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [フロー制御言語 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

