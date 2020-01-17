---
title: FORMATMESSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c9048efd86a7a4a993a9fff6bcab7f9058144f7e
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843761"
---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Sys.messages 内で、既存のメッセージから、または指定された文字列からのメッセージを構築します。 FORMATMESSAGE の機能は RAISERROR ステートメントの機能に似ています。 ただし、RAISERROR がメッセージを即時出力するのに対して、FORMATMESSAGE が返す書式設定済みのメッセージには、さらに処理を加えることができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *msg_number*  
 sys.messages に格納されているメッセージの ID です。 *msg_number* が <= 13000 である場合、またはそのメッセージが sys.messages にない場合は、NULL が返されます。  
  
 *msg_string*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 単一引用符で囲まれた、パラメーターの値のプレース ホルダーを含む文字列です。 エラー メッセージの長さは最大 2,047 文字です。 メッセージの文字数が 2,048 文字を超えると、2,044 文字までだけ表示され、メッセージが途中で切れていることを示す省略記号が追加されます。 内部的な記憶動作が原因で、書式引数は出力として表示されるより多くの文字を使用することに注意してください。  メッセージ文字列の構造と文字列内のパラメーターの使用については、「[RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)」の *msg_str* 引数の説明を参照してください。  
  
 *param_value*  
 メッセージで使用するパラメーター値です。 複数のパラメーター値を指定することもできます。 メッセージに指定されているプレースホルダー変数の順序で、値を指定する必要があります。 値の最大個数は 20 です。  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 RAISERROR ステートメントと同様、FORMATMESSAGE は、指定されたパラメーター値を、メッセージ内のプレースホルダー変数に置き換えることによって、メッセージを編集します。 エラー メッセージに指定できるプレースホルダーと編集処理の詳細については、「[RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)」を参照してください。  
  
 FORMATMESSAGE は、ユーザーが現在使用している言語のメッセージを検索します。 日本語版のメッセージがない場合は、英語版のメッセージが使用されます。  
  
 日本語版のメッセージの場合、英語版のパラメーター プレースホルダーに対応するようにパラメーター値を指定する英語版。 つまり、日本語版のパラメーター 1 は、英語版のパラメーター 1 に対応する必要があります。日本語版のパラメーター 2 は、英語版のパラメーター 2 に対応する必要があります。以降についても同様です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-example-with-a-message-number"></a>A. メッセージ番号を含む例  
 次の例では、sys.messages に格納されているレプリケーション メッセージ `20009` を "アーティクル '%s' をパブリケーション '%s' に追加できませんでした。" として使用します。FORMATMESSAGE は、パラメーター プレースホルダーの代わりに `First Variable` 値と `Second Variable` 値を使用します。 置換後の文字列 "アーティクル 'First Variable' をパブリケーション 'Second Variable' に追加できませんでした。" は、ローカル変数 `@var1` に格納されます。  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. メッセージ文字列の例  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 次の例では、入力として文字列を受け取ります。  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 戻り値: `This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. 追加のメッセージ文字列の例を書式設定  
 次の例では、さまざまな書式設定オプションを示しています。  
  
```  
SELECT FORMATMESSAGE('Signed int %i, %d %i, %d, %+i, %+d, %+i, %+d', 5, -5, 50, -50, -11, -11, 11, 11);
SELECT FORMATMESSAGE('Signed int with up to 3 leading zeros %03i', 5);  
SELECT FORMATMESSAGE('Signed int with up to 20 leading zeros %020i', 5);  
SELECT FORMATMESSAGE('Signed int with leading zero 0 %020i', -55);  
SELECT FORMATMESSAGE('Bigint %I64d', 3000000000);
SELECT FORMATMESSAGE('Unsigned int %u, %u', 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal %o, %o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal %x, %X, %X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal with prefix: %#o, %#o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal with prefix: %#x, %#X, %#X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Hello %s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %-20s!', 'TEST');  
```  
  
## <a name="see-also"></a>参照  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
  
  
