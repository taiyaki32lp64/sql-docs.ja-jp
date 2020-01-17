---
title: READTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- READTEXT_TSQL
- READTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- column reading [SQL Server]
- READTEXT statement
- reading columns
ms.assetid: 91b69853-1381-4306-8343-afdb73105738
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dd8ad58e96956e1ab0f7b542bab4168272b3f968
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141293"
---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**text**、**ntext**、**image** 列から **text**、**ntext**、**image** 値を読み取ります。 指定されたオフセットから開始し、指定されたバイト数を読み取ります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、[SUBSTRING](../../t-sql/functions/substring-transact-sql.md) 関数を使用してください。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>引数  
_table_ **.** _column_  
読み取り元のテーブルと列の名前です。 テーブル名と列名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。 テーブル名と列名は必ず指定してください。しかし、データベース名と所有者の指定は省略可能です。  
  
_text\_ptr_  
有効なテキスト ポインターです。 _text\_ptr_ は **binary(16)** 型である必要があります。  
  
_offset_  
データ型として **text** または **image** が使用されるときのバイト数。 **text**、**image**、**ntext** データの読み取りを開始する前に **ntext** データ型を使用してスキップするときの文字バイト数になる場合もあります。  
  
_size_ データ型として **text** または **image** が使用されるときのバイト数。 読み取るデータに **ntext** データ型が使用されるときの文字バイト数になる場合もあります。 _size_ が 0 の場合、4 KB のデータが読み取られます。  
  
HOLDLOCK  
トランザクションが終了するまでテキスト値の読み取りをロックします。 他のユーザーは値を読み取ることができますが、変更はできません。  
  
## <a name="remarks"></a>Remarks  
有効な _text\_ptr_ 値を取得するには、[TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) 関数を使用します。 TEXTPTR は指定行で **text**、**ntext**、**image** 列のポインターを返します。 TEXTPRT はまた、クエリが複数の行を返す場合の最後の行で **text**、**ntext**、**image** 列のポインターを返します。 TEXTPTR は 16 バイトのバイナリ文字列を返すため、テキスト ポインターを保持するローカル変数を宣言し、READTEXT でその変数を使用することをお勧めします。 ローカル変数の宣言の詳細については、「[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)」を参照してください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、行内テキスト ポインターが存在しても、有効ではない場合があります。 **text in row** オプションの詳細については、「[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。 テキスト ポインターを無効にする方法の詳細については、「[sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)」を参照してください。  
  
READTEXT で指定されたサイズよりも @@TEXTSIZE 関数の値の方が小さい場合は、READTEXT に代わってその関数の値が使用されます。 @@TEXTSIZE 関数は、SET TEXTSIZE ステートメントで設定される、返されるデータのバイト数の上限を指定します。 TEXTSIZE のセッション設定の設定方法の詳細については、「[SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
READTEXT 権限は、特に指定のない限り指定されたテーブルで SELECT 権限を持つユーザーに与えられます。 SELECT 権限を譲渡した場合は、READTEXT 権限を譲渡できます。  
  
## <a name="examples"></a>使用例  
次の例では、`pr_info` テーブルの `pub_info` 列の 2 文字目から 26 文字目までを読み取ります。  
  
> [!NOTE]  
>  この例を実行するには、**pubs** サンプル データベースをインストールする必要があります。  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr INNER JOIN publishers p  
      ON pr.pub_id = p.pub_id   
      AND p.pub_name = 'New Moon Books'  
READTEXT pub_info.pr_info @ptrval 1 25;  
GO  
```  
  
## <a name="see-also"></a>参照  
[@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
