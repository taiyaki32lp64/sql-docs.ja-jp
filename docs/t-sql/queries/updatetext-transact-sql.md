---
title: UPDATETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b858cc4930cdfe9792e08c991c3ebdf8f319d0f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948222"
---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既存の **text**、**ntext**、または **image** フィールドを更新します。 **text**、**ntext**、または **image** 型の列の一部だけを適切に変更するには、UPDATETEXT を使用します。 **text**、**ntext**、または **image** 型のフィールド全体を更新して置き換えるには、WRITETEXT を使用します。  
  
> [!IMPORTANT]
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、large-value データ型と [UPDATE](../../t-sql/queries/update-transact-sql.md) ステートメントの **.** WRITE 句を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATETEXT [BULK] { table_name.dest_column_name dest_text_ptr }  
  { NULL | insert_offset }  
     { NULL | delete_length }  
     [ WITH LOG ]  
     [ inserted_data  
    | { table_name.src_column_name src_text_ptr } ]  
```  
  
## <a name="arguments"></a>引数  
 BULK  
 アップロード ツールによるバイナリ データ ストリームのアップロードを有効にします。 ストリームは、TDS プロトコル レベルでツールが提供する必要があります。 データ ストリームが存在しない場合、クエリ プロセッサは BULK オプションを無視します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ベースのアプリケーションでの BULK オプションの使用はお勧めしません。 このオプションは将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では変更または削除される可能性があります。  
  
 *table_name* **.** *dest_column_name*  
 更新するテーブルと **text**、**ntext**、または **image** 型の列の名前。 テーブル名と列名は、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 データベース名と所有者名の指定は省略可能です。  
  
 *dest_text_ptr*  
 更新する **text**、**ntext**、または **image** 型のデータを指す、テキスト ポインター値を指定します。テキスト ポインター値は TEXTPTR 関数から返されます。 *dest_text_ptr* は、 **binary(** 16 **)** にする必要があります。  
  
 *insert_offset*  
 更新の開始位置を 0 を起点として指定します。 **text** または **image** 型の列の場合、*insert_offset* には、既存の列の開始位置から新しいデータの開始位置までにスキップするバイト数を指定します。 **Ntext** 列の場合、*insert_offset* は文字数です (各 **ntext** 文字は 2 バイトを使用します)。 この 0 を起点とした開始位置から始まる既存の **text**、**ntext**、または **image** 型の各データは、新しいデータの分だけ右に移動します。 値 0 を指定した場合、新しいデータは既存のデータの先頭に挿入されます。 NULL の場合、新しいデータは既存のデータの最後に追加されます。  
  
 *delete_length*  
 既存の**text**、**ntext**、または **image** 型の列で、*insert_offset* で指定した位置から後にある、削除するデータの長さを指定します。 *delete_length* 値は、**text** および **image** 型の列ではバイト単位で指定され、**ntext** 型の列では文字数で指定されます。 各 **ntext** 文字は 2 バイトを使用します。 値 0 を指定した場合、データは削除されません。 NULL の場合、既存の **text** 型または **image** 型の列で、*insert_offset* の位置から終わりまでのすべてのデータが削除されます。  
  
 WITH LOG  
 ログ記録は、データベースで有効になっている復旧モデルによって異なります。  
  
 *inserted_data*  
 既存の **text**、**ntext**、または **image** 型の列で *insert_offset* の位置に挿入されるデータです。 これは 1 つの **char**、**nchar**、**varchar**、**nvarchar**、**binary**、**varbinary**、**text**、**ntext**、または **image** 値です。 *inserted_data* は、リテラルまたは変数を設定することができます。  
  
 *table_name.src_column_name*  
 挿入するデータのソースとして使用する、テーブルおよび **text**、**ntext**、または **image** 型の列の名前を指定します。 テーブル名と列名は、識別子の規則に従っている必要があります。  
  
 *src_text_ptr*  
 挿入するデータのソースとして使用できる、**text**、**ntext**、または **image** 型の各列を指すテキスト ポインターの値を指定します。テキスト ポインターの値は TEXTPTR 関数から返されます。  
  
> [!NOTE]  
>  *scr_text_ptr* 値は *dest_text_ptr* 値と同じにすることはできません。  
  
## <a name="remarks"></a>Remarks  
 新しく挿入するデータには、1 つの *inserted_data* 定数、テーブル名、列名、またはテキスト ポインターを使用できます。  
  
|アクションの更新|UPDATETEXT パラメーター|  
|-------------------|---------------------------|  
|既存のデータの置換|NULL 以外の *insert_offset* 値、0 以外の *delete_length* 値、および挿入する新しいデータを指定します。|  
|既存のデータの削除|NULL 以外の *insert_offset* 値、0 以外の *delete_length* を指定します。 挿入する新しいデータは指定しないでください。|  
|新しいデータの挿入|*insert_offset* 値、0 の *delete_length* 値、および挿入する新しいデータを指定します。|  
  
 最適なパフォーマンスを得るには、8,040 バイトの倍数単位で **text**、**ntext**、および **image** 型データを挿入または更新することをお勧めします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**text**、**ntext**、または **image** データへの行内テキスト ポインターが存在しても、無効になる場合があります。 text in row オプションについては、「[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。 テキスト ポインターを無効にする方法の詳細については、「[sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)」を参照してください。  
  
 **text** 列を NULL に初期化するには、WRITETEXT を使用します。UPDATETEXT を使用すると、**text** 列が空の文字列に初期化されます。  
  
## <a name="permissions"></a>アクセス許可  
 指定したテーブルの UPDATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、テキスト ポインターをローカル変数 `@ptrval` に代入した後、`UPDATETEXT` を使用してスペル ミスを更新します。  
  
> [!NOTE]  
>  この例を実行するには、pubs データベースをインストールする必要があります。  
  
```  
USE pubs;  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
DECLARE @ptrval binary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr, publishers p  
      WHERE p.pub_id = pr.pub_id   
      AND p.pub_name = 'New Moon Books'  
UPDATETEXT pub_info.pr_info @ptrval 88 1 'b';  
GO  
ALTER DATABASE pubs SET RECOVERY FULL;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
