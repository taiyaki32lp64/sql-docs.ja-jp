---
title: xp_sqlmaint (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9948767ca0eca5721207079f978987142653e9c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091907"
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  呼び出し、 **sqlmaint**ユーティリティを含む文字列**sqlmaint**スイッチ。 **Sqlmaint**ユーティリティは、1 つまたは複数のデータベースでメンテナンス操作のセットを実行します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>引数  
 **'** *switch_string* **'**  
 含む文字列、 **sqlmaint**ユーティリティ スイッチです。 スイッチとその値は、空白で区切る必要があります。  
  
 **-でしょうか。** スイッチで有効でない**xp_sqlmaint**します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 [なし] : エラーが返されます、 **sqlmaint**ユーティリティが失敗します。  
  
## <a name="remarks"></a>コメント  
 この手順は、SQL Server の認証でログオンしたユーザーによって呼び出される場合、 **-u"***login_id***"** と **-p"***パスワード***"** スイッチ前に付加されます*switch_string*実行前にします。 Windows 認証では、ユーザーがログインしている場合*switch_string*への変更なしで渡される**sqlmaint**します。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`xp_sqlmaint`呼び出し`sqlmaint`整合性チェックを実行するレポート ファイルを作成および更新`msdb.dbo.sysdbmaintplan_history`します。  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>関連項目  
 [sqlmaint ユーティリティ](../../tools/sqlmaint-utility.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
