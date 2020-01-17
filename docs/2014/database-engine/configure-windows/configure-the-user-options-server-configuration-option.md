---
title: user options サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- global default for all users [SQL Server]
- users [SQL Server], global defaults
- user options option [SQL Server]
ms.assetid: cfed8f86-6bcf-4b90-88eb-9656e22d5dc5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b0588bbc8c21c9946ac72a2db92c593e48973dfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787074"
---
# <a name="configure-the-user-options-server-configuration-option"></a>user options サーバー構成オプションの構成
  このトピックでは、 **または** を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] user options [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **user options** オプションは、すべてのユーザーに対するグローバルな既定値を指定します。 ユーザーの作業セッション中に、一連の既定のクエリ処理オプションが設定されます。 **user options** オプションを使用すると、SET オプションの既定値を変更できます (サーバーの既定の設定が適切でない場合)。  
  
 各ユーザーは、SET ステートメントを使用してこれらの既定値をオーバーライドできます。 新しいログインについては **user options** を動的に構成できます。 **user options**の設定を変更した場合、新しい設定は新しいログイン セッションで使用され、現在のログイン セッションには影響しません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **user connections 構成オプションを構成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [user options 構成オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   次の表は、 **user options**の構成値と説明の一覧です。 すべての構成値が他の構成値と両立するわけではありません。 たとえば、ANSI_NULL_DFLT_ON と ANSI_NULL_DFLT_OFF を同時に設定することはできません。  
  
    |値|構成|説明|  
    |-----------|-------------------|-----------------|  
    |1|DISABLE_DEF_CNST_CHK|中間制約チェックまたは遅延制約チェックを制御します。|  
    |2|IMPLICIT_TRANSACTIONS|dblib ネットワーク ライブラリ接続の場合、ステートメントの実行時にトランザクションを暗黙的に開始するかどうかを制御します。 IMPLICIT_TRANSACTIONS の設定は、ODBC または OLEDB 接続には影響を与えません。|  
    |4|CURSOR_CLOSE_ON_COMMIT|コミット実行後のカーソルの動作を制御します。|  
    |8|ANSI_WARNINGS|集計警告の切り詰めと NULL を制御します。|  
    |16|ANSI_PADDING|固定長変数の埋め込みを制御します。|  
    |32|ANSI_NULLS|等価演算を使用する場合に NULL 処理を制御します。|  
    |64|ARITHABORT|クエリ実行中にオーバーフローまたは 0 除算のエラーが発生した場合に、クエリを終了します。|  
    |128|ARITHIGNORE|クエリ実行中にオーバーフローまたは 0 除算エラーが発生した場合に、NULL を返します。|  
    |256|QUOTED_IDENTIFIER|式を評価するときに、単一引用符と二重引用符を区別します。|  
    |512|NOCOUNT|各ステートメントの最後に返される、何行処理されたかを示すメッセージを表示しないようにします。|  
    |1024|ANSI_NULL_DFLT_ON|ANSI 互換の NULL 値の許可属性を使用するようにセッションの動作を変更します。 新しい列で、NULL 値を許可するかどうかが明示的に定義されていない場合は、NULL 値を許可するように定義されます。|  
    |2048|ANSI_NULL_DFLT_OFF|ANSI 互換の NULL 値の許可属性を使用しないようにセッションの動作を変更します。 新しい列で、NULL 値を許可するかどうかが明示的に定義されていない場合は、NULL 値が許可されません。|  
    |4096|CONCAT_NULL_YIELDS_NULL|NULL 値を文字列と連結した場合に、NULL を返します。|  
    |8192|NUMERIC_ROUNDABORT|式の精度が低下した場合にエラーを生成します。|  
    |16384|XACT_ABORT|Transact-SQL ステートメントで実行時エラーが発生した場合、トランザクションをロールバックします。|  
  
-   **user options** のビット位置は、@@OPTIONS のビット位置と同じです。 接続にはそれぞれの構成環境を表す @@OPTIONS 関数があります。 \ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにログインすると、ユーザーは **user options** の現在の値が @@OPTIONS に代入される既定の環境を受け取ります。 **user options** について SET ステートメントを実行すると、そのセッションの @@OPTIONS 関数の対応する値に適用されます。 この設定の変更後に作成された接続は、すべて新しい値を受け取ります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>user connections 構成オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[接続]** ノードをクリックします。  
  
3.  **[既定の接続オプション]** ボックスで、1 つ以上の属性を選択し、すべての接続済みユーザーの既定のクエリ処理オプションを構成します。  
  
     既定では、ユーザー オプションは構成されていません。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>user connections 構成オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 次の例は、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して、ANSI_WARNINGS サーバー オプションの設定を変更する `user options` を構成する方法を示しています。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'user options', 8 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
##  <a name="FollowUp"></a>補足情報: user options 構成オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [SET ステートメント &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)  
  
  
