---
title: xp_logevent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77275ee539a6367d7e2e04d03354155a5eff721d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116639"
---
# <a name="xplogevent-transact-sql"></a>xp_logevent (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ユーザー定義のメッセージを記録、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ ファイルと、Windows イベント ビューアでします。 クライアントにメッセージを送信せずにアラートを送信する、xp_logevent を使用できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>引数  
 *error_number*  
 50,000 より大きい、ユーザー定義のエラー番号を指定します。 最大値は 2,147, 483,647 (2 ^31-1)。  
  
 **'** *メッセージ* **'**  
 最大 2048 バイトまでの文字列を指定します。  
  
 **'** *重大度* **'**  
 次の 3 つの文字列のいずれかです。情報、警告、またはエラー。 *重大度*は省略可能で、既定値は INFORMATIONAL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 xp_logevent では、付属のコード例では、次のエラー メッセージが返されます。  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>コメント  
 メッセージを送信するときに[!INCLUDE[tsql](../../includes/tsql-md.md)]プロシージャ、トリガー、バッチ、および、xp_logevent ではなく RAISERROR ステートメントを使用します。 xp_logevent がクライアントのメッセージ ハンドラーの呼びまたはを設定していない@ERRORします。 Windows イベント ビューアーとのメッセージを書き込む、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内のエラー ログ ファイル[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、RAISERROR ステートメントを実行します。  
  
## <a name="permissions"></a>アクセス許可  
 Master データベースの db_owner 固定データベース ロールのメンバーシップ、または sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、Windows イベント ビューアー内のメッセージに渡される変数で、メッセージを記録します。  
  
```  
DECLARE @@TABNAME varchar(30), @@USERNAME varchar(30), @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>関連項目  
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [汎用拡張ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
