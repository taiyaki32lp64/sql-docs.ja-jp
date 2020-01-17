---
title: TEXTPTR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTPTR_TSQL
- TEXTPTR
dev_langs:
- TSQL
helpviewer_keywords:
- TEXTPTR function
- viewing text pointer values
- text-pointer values
- displaying text pointer values
ms.assetid: 2672b8cb-f747-46f3-9358-9b49b3583b8e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d0e511e34b782c444bcdf6c778bb89dfebd4fab4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099035"
---
# <a name="text-and-image-functions---textptr-transact-sql"></a>テキスト関数とイメージ関数 - TEXTPTR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **text**、**ntext**、または **image** 列に対応するテキスト ポインターの値を **varbinary** 形式で返します。 取得したテキスト ポインターの値は、READTEXT、WRITETEXT、および UPDATETEXT ステートメントで使用します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代替機能を使用することはできません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
TEXTPTR ( column )  
```  
  
## <a name="arguments"></a>引数  
 *column*  
 使われる **text**、**ntext**、または **image** の列です。  
  
## <a name="return-types"></a>戻り値の型  
 **varbinary**  
  
## <a name="remarks"></a>Remarks  
 行内テキストがあるテーブルの場合、TEXTPTR では、処理するテキストのハンドルが返されます。 テキストの値が NULL である場合も、有効なテキスト ポインターを取得できます。  
  
 ビューの列に対して TEXTPTR 関数を使用することはできません。 それはテーブルの列に対してのみ使用できます。 ビューの列に対して TEXTPTR 関数を使用するには、[ALTER DATABASE 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)を使用して互換性レベルを 80 に設定する必要があります。 テーブルに行内テキストがなく、**text**、**ntext**、または **image** 列が UPDATETEXT ステートメントで初期化されていない場合、TEXTPTR は NULL ポインターを返します。  
  
 テキスト ポインターが存在するかどうかをテストするには、TEXTVALID を使用します。 有効なテキスト ポインターがないと、UPDATETEXT、WRITETEXT、READTEXT は使用できません。  
  
 これらの関数とステートメントは、**text**、**ntext**、**image** データを操作する場合にも役立ちます。  
  
|関数またはステートメント|[説明]|  
|---------------------------|-----------------|  
|PATINDEX<b>('</b> _%pattern%_ **' ,** _expression_ **)**|**text** または **ntext** 列で指定された文字列の文字位置を返します。|  
|DATALENGTH<b>(</b>_expression_ **)**|**text**、**ntext**、**image** 列のデータの長さを返します。|  
|[SET TEXTSIZE]|SELECT ステートメントで返される **text**、**ntext**、または **image** データの制限値をバイト単位で返します。|  
|SUBSTRING<b>(</b>_text_column_, _start_, _length_ **)**|指定された *start* オフセットと *length* で指定される **varchar** 文字列を返します。 長さは 8 KB 未満で指定してください。|  
  
## <a name="examples"></a>使用例  
  
> [!NOTE]  
>  次の例を実行するには、**pubs** データベースをインストールする必要があります。  
  
### <a name="a-using-textptr"></a>A. TEXTPTR を使用する  
 次の例では、`TEXTPTR` 関数を使用して、`pubs` データベースの `pub_info` テーブル内の `New Moon Books` に関連付けられている **image** 列 `logo` を検索します。 テキスト ポインターは、ローカル変数 `@ptrval.` に格納されます。  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(logo)  
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books';  
GO  
```  
  
### <a name="b-using-textptr-with-in-row-text"></a>B. TEXTPTR を行内テキストと使用する  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、行内テキスト ポインターは、次の例に示すように、トランザクション内で使用する必要があります。  
  
```  
CREATE TABLE t1 (c1 int, c2 text);  
EXEC sp_tableoption 't1', 'text in row', 'on';  
INSERT t1 VALUES ('1', 'This is text.');  
GO  
BEGIN TRAN;  
   DECLARE @ptrval VARBINARY(16);  
   SELECT @ptrval = TEXTPTR(c2)  
   FROM t1  
   WHERE c1 = 1;  
   READTEXT t1.c2 @ptrval 0 1;  
COMMIT;  
```  
  
### <a name="c-returning-text-data"></a>C. テキスト データを返す  
 次の例では、`pub_info` テーブルから `pub_id` 列、および `pr_info` 列の 16 バイトのテキスト ポインターを選択します。  
  
```  
USE pubs;  
GO  
SELECT pub_id, TEXTPTR(pr_info)  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id                                      
------ ----------------------------------   
0736   0x6c0000000000feffb801000001000100   
0877   0x6d0000000000feffb801000001000300   
1389   0x6e0000000000feffb801000001000500   
1622   0x700000000000feffb801000001000900   
1756   0x710000000000feffb801000001000b00   
9901   0x720000000000feffb801000001000d00   
9952   0x6f0000000000feffb801000001000700   
9999   0x730000000000feffb801000001000f00   
  
(8 row(s) affected)  
```  
  
 次の例では、TEXTPTR を使用せずにテキストの最初の `8000` バイトを返す方法を示します。  
  
```  
USE pubs;  
GO  
SET TEXTSIZE 8000;  
SELECT pub_id, pr_info  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id pr_info                                                                                                                                                                                                                                                           
------ -----------------------------------------------------------------  
0736   New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!                                                                                                             
0877   This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washington, D.C.  
  
This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washi   
1389   This is sample text data for Algodata Infosystems, publisher 1389 in the pubs database. Algodata Infosystems is located in Berkeley, California.  
  
9999   This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in Paris, France.  
  
This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in   
  
(8 row(s) affected)  
```  
  
### <a name="d-returning-specific-text-data"></a>D. 特定のテキスト データを返す  
 次の例では、`pubs` データベースの `pub_info` テーブル内の `pub_id``0736` に関連付けられた `text` 列 (`pr_info`) を検索します。 まず、ローカル変数 `@val` が宣言されます。 次に、テキスト ポインター (長いバイナリ文字列) が `@val` に挿入され、`READTEXT` ステートメントにパラメーターとして指定されます。 これによって、5 番目のバイト (オフセットは 4) から開始して、10 バイトのデータが返されます。  
  
```  
USE pubs;  
GO  
DECLARE @val varbinary(16);  
SELECT @val = TEXTPTR(pr_info)   
FROM pub_info  
WHERE pub_id = '0736';  
READTEXT pub_info.pr_info @val 4 10;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pr_info                                                                                                                                                                                                                                                           
-----------------------------------------------------------------------  
 is sample  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [テキスト関数とイメージ関数 &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
