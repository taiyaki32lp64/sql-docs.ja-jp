---
title: データベース エンジン エラーの重大度 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0984d0003f6a20c410b91f99dc6fd1b4ae3f545
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844325"
---
# <a name="database-engine-error-severities"></a>データベース エンジン エラーの重大度
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]によってエラーが発生した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に発生した問題の種類がエラーの重大度によって示されます。  
  
## <a name="levels-of-severity"></a>重大度レベル  
 次の表は、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]によって発生したエラーの重大度レベルについて示しています。  
  
|重大度レベル|[説明]|  
|--------------------|-----------------|  
|0-9|ステータス情報を返すか、重大ではないエラーを報告する情報メッセージです。 重大度 0 ～ 9 のシステム エラーが [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって発生することはありません。|  
|10|ステータス情報を返すか、重大ではないエラーを報告する情報メッセージです。 互換性の理由から、呼び出し側アプリケーションにエラー情報を返す前に [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって重大度 10 から重大度 0 に変換されます。|  
|11-16|ユーザーが訂正できるエラーを示します。|  
|11|指定したオブジェクトまたはエンティティが存在しないことを示します。|  
|12|特別のクエリ ヒントのためロックを使用しないクエリに対する特別な重大度です。 一貫性を保証するロックが使用されないため、これらのステートメントによって実行される読み取り操作でデータの一貫性が損なわれる場合があります。|  
|13|トランザクションのデッドロック エラーを示します。|  
|14|権限の拒否などのセキュリティに関係するエラーを示します。|  
|15|[!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドの構文エラーを示します。|  
|16|ユーザーが訂正できる一般的なエラーを示します。|  
|17-19|ユーザーが訂正できないソフトウェアのエラーを示します。 システム管理者に問題を報告してください。|  
|17|ステートメントにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリソース (メモリ、ロック、またはデータベース用ディスク領域) を使い果たしたか、システム管理者が設定した制限を超えたことを示します。|  
|18|[!INCLUDE[ssDE](../../includes/ssde-md.md)] ソフトウェアの問題を示します。ただし、ステートメントによって実行は完了し、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスへの接続は維持されます。 重大度レベル 18 のメッセージが発生した場合は、必ずシステム管理者に報告してください。|  
|19|構成できない [!INCLUDE[ssDE](../../includes/ssde-md.md)] の制限を超えたため、現在のバッチ プロセスが終了させられたことを示します。 重大度レベル 19 以上のエラー メッセージは、現在のバッチの実行を停止します。 重大度レベル 19 のエラーの発生はまれですが、発生した場合はシステム管理者またはご購入先で修正する必要があります。 重大度レベル 19 のメッセージが発生した場合は、システム管理者に問い合わせてください。 重大度レベル 19 ～ 25 のエラー メッセージは、エラー ログに書き込まれます。|  
|20-24|システムの問題を示します。これらは重大なエラーで、ステートメントまたはバッチを実行する [!INCLUDE[ssDE](../../includes/ssde-md.md)] タスクは実行できなくなります。 タスクは何が起きたのかを記録し、その後終了します。 ほとんどの場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスへのアプリケーション接続も終了します。 この問題が発生すると、問題によっては、アプリケーションの再接続ができない場合があります。<br /><br /> この範囲のエラー メッセージは、同じデータベースのデータにアクセスするすべてのプロセスに影響し、データベースまたはオブジェクトに損傷があったことを示します。 重大度レベル 19 ～ 24 のエラー メッセージは、エラー ログに書き込まれます。|  
|20|ステートメントに問題が発生したことを示します。 この問題は現在のタスクにのみ影響するので、データベース自体が損傷している可能性はありません。|  
|21|現在のデータベース内のすべてのタスクに影響する問題が発生したことを示します。ただし、データベース自体が損傷している可能性はありません。|  
|22|メッセージに示されたテーブルまたはインデックスが、ソフトウェアまたはハードウェアの問題によって損傷していることを示します。<br /><br /> 重大度レベル 22 のエラーはまれにしか発生しません。 このエラーが発生した場合は、DBCC CHECKDB を実行して、データベース内の他のオブジェクトも損傷しているかどうかを判断します。 問題がバッファー キャッシュ内だけで発生し、ディスク自体には問題がないこともあります。 問題がない場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを再起動することで解決できます。 作業を続行するには、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに再接続する必要があります。それ以外の場合は、DBCC を使用して問題を修復します。 場合によっては、データベースの復元が必要です。<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを再起動しても問題が解決しない場合は、ディスクに問題があります。 エラー メッセージで示されているオブジェクトを破棄することで、問題が解決する場合があります。 たとえば、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが、非クラスター化インデックス内で長さ 0 の行を見つけたことをメッセージが報告している場合、インデックスをいったん削除し、再構築します。|  
|23|ハードウェアまたはソフトウェアの問題によって、データベース全体の整合性に疑いがあることを示します。<br /><br /> 重大度レベル 23 のエラーはまれにしか発生しません。 このエラーが発生した場合は、DBCC CHECKDB を実行し、損傷の範囲を調べます。 問題がキャッシュ内でのみ発生し、ディスク自体には問題がないこともあります。 問題がない場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを再起動することで解決できます。 作業を続行するには、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに再接続する必要があります。それ以外の場合は、DBCC を使用して問題を修復します。 場合によっては、データベースの復元が必要です。|  
|24|メディアの障害を示します。 システム管理者がデータベースを復元する必要がある場合があります。 また、場合によっては、ハードウェア ベンダーに相談する必要もあります。|  
  
## <a name="user-defined-error-message-severity"></a>ユーザー定義のエラー メッセージの重大度  
 **sp_addmessage** を使用して、重大度 1 ～ 25 のユーザー定義のエラー メッセージを **sys.messages** カタログ ビューに追加することができます。 これらのユーザー定義のエラー メッセージは、RAISERROR で使用することができます。 詳細については、「[sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)」を参照してください。  
  
 RAISERROR を使用して、重大度レベル 1 ～ 25 のユーザー定義のエラー メッセージを生成することができます。 RAISERROR は、 **sys.messages** カタログ ビューに格納されているユーザー定義のエラー メッセージを参照することも、メッセージを動的に作成することもできます。 エラーの発生中に、**sys.messages** にあるユーザー定義エラー メッセージを使用する場合、RAISERROR で指定された重大度は、**sys.messages** で指定された重大度をオーバーライドします。 詳細については、「[RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)」を参照してください。  
  
## <a name="error-severity-and-trycatch"></a>エラーの重大度と TRY...CATCH  
 TRY...CATCH コンストラクトでは、データベース接続を終了しない、重大度が 10 を超えるすべての実行エラーが検出されます。  
  
 重大度 0 から 10 のエラーは情報メッセージであるため、TRY...CATCH コンストラクトの CATCH ブロックからのジャンプは実行されません。  
  
 接続が終了すると実行は中断されるため、データベース接続を終了させるエラー (通常の場合、重大度 20 ～ 25 のエラー) は CATCH ブロックでは処理されません。  
  
 詳細については、「 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)に発生した問題の種類がエラーの重大度によって示されます。  
  
## <a name="retrieving-error-severity"></a>エラーの重大度の取得  
 システム関数 ERROR_SEVERITY を使用して、TRY...CATCH コンストラクトの CATCH ブロックを実行したエラーの重大度を取得することができます。 CATCH ブロックの範囲外で呼び出された場合、ERROR_SEVERITY は NULL を返します。 詳細については、「[ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン エラーについて](../../relational-databases/errors-events/understanding-database-engine-errors.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
