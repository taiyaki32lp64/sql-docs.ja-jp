---
title: WRITETEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WRITETEXT_TSQL
- WRITETEXT
dev_langs:
- TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c10e7259062316454e4e0ecf430f6fdb87c53caf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948102"
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既存の **text**、**ntext**、または **image** 列の最小限ログに記録する対話型の更新を許可します。 WRITETEXT は、影響のある列内の既存のすべてのデータを上書きします。 WRITETEXT をビュー内の **text** 列、**ntext** 列、**image** 列に対して使用することはできません。  
  
> [!IMPORTANT]
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、large-value データ型と [UPDATE](../../t-sql/queries/update-transact-sql.md) ステートメントの **.** WRITE 句を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
WRITETEXT [BULK]  
  { table.column text_ptr }  
  [ WITH LOG ] { data }  
```  
  
## <a name="arguments"></a>引数  
 BULK  
 アップロード ツールによるバイナリ データ ストリームのアップロードを有効にします。 ストリームは、TDS プロトコル レベルでツールが提供する必要があります。 データ ストリームが存在しない場合、クエリ プロセッサは BULK オプションを無視します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ベースのアプリケーションでの BULK オプションの使用はお勧めしません。 このオプションは将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では変更または削除される可能性があります。  
  
 *table* **.column**  
 更新するテーブルと **text**、**ntext**、または **image** 型の列の名前。 テーブル名と列名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。 データベース名と所有者名の指定は省略可能です。  
  
 *text_ptr*  
 **text**、**ntext**、または **image** データへのポインターを保存する値です。 *text_ptr* は **binary(16)** にする必要があります。テキスト ポインターを作成するには、**text**、**ntext**、または **image** 列に対して NULL 以外のデータを使用する [INSERT](../../t-sql/statements/insert-transact-sql.md) ステートメントまたは [UPDATE](../../t-sql/queries/update-transact-sql.md) ステートメントを実行します。  
  
 WITH LOG  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では無視されます。 ログ記録は、データベースで有効になっている復旧モデルによって異なります。  
  
 *data*  
 格納する実際の **text**、**ntext**、または **image** データです。 *data* には、リテラルまたはパラメーターを指定することができます。 WRITETEXT を使用して対話的に挿入可能なテキスト長の最大値は、**text**、**ntext**、および **image** データで約 120 KB です。  
  
## <a name="remarks"></a>Remarks  
 WRITETEXT を使用して **text**、**ntext**、および **image** データを置き換え、UPDATETEXT を使用して **text**、**ntext**、および **image** データを変更します。 UPDATETEXT は、**text**、**ntext**、または **image** 列の全体ではなく一部のみを変更するため柔軟性があります。  
  
 最高のパフォーマンスが得られるよう、8,040 バイトの倍数の単位で **text**、**ntext**、および **image** データを挿入または更新することをお勧めします。  
  
 データベース復旧モデルが単純復旧モデルまたは一括ログ復旧モデルである場合は、新しいデータを挿入または追加するときに、WRITETEXT を使用する **text**、**ntext**、および **image** 操作は最小限しかログに記録されません。  
  
> [!NOTE]  
>  既存の値を更新するときには、最小限のログ記録は使用されません。  
  
 WRITETEXT が正しく機能するためには、その列は既に有効なテキスト ポインターを含んでいる必要があります。  
  
 テーブルに行内テキストがない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、明示的または暗黙的な NULL 値が INSERT によって **text** 列に挿入されているときに **text** 列の初期化を省略することによって領域を節約しますが、そのような NULL に対するテキスト ポインターは取得できません。 **text** 列を初期化して NULL にするには、UPDATE ステートメントを使用します。 テーブルに行内テキストがある場合、テキスト列を初期化して NULL にする必要はなく、常にテキスト ポインターを取得できます。  
  
 ODBC SQLPutData 関数は、WRITETEXT に比べ高速で、使用する動的メモリの量も少なくなります。 この関数は、最大 2 GB までの **text**、**ntext**、または **image** データを挿入できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**text**、**ntext**、または **image** データへの行内テキスト ポインターが存在しても、無効になる場合があります。 text in row オプションについては、「[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。 テキスト ポインターを無効にする方法の詳細については、「[sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 指定したテーブルの UPDATE 権限が必要です。 UPDATE 権限が転送されるときに、この権限は譲渡できます。  
  
## <a name="examples"></a>使用例  
 次の例では、テキスト ポインターをローカル変数 `@ptrval` に置き、`WRITETEXT` が指す行に `@ptrval` で新しいテキスト文字列を入れます。  
  
> [!NOTE]  
>  この例を実行するには、pubs サンプル データベースをインストールする必要があります。  
  
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
WRITETEXT pub_info.pr_info @ptrval 'New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!';  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
