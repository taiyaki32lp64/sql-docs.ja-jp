---
title: BEGIN DISTRIBUTED TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DISTRIBUTED
- BEGIN_DISTRIBUTED_TRANSACTION_TSQL
- DISTRIBUTED_TSQL
- BEGIN DISTRIBUTED TRANSACTION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN DISTRIBUTED TRANSACTION statement
- distributed transactions [SQL Server], starting
- MS DTC, transaction management
- distributed transactions [SQL Server], BEGIN DISTRIBUTED TRANSACTION statement
- servers [SQL Server], distributed transactions
- starting distributed transactions
- remote servers [SQL Server], distributed transactions
- starting transactions
ms.assetid: c3bc2716-39d3-4061-8c6a-8734899231ac
author: rothja
ms.author: jroth
ms.openlocfilehash: 0faddc5b763a2728dc507d2aad17b26501846452
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125319"
---
# <a name="begin-distributed-transaction-transact-sql"></a>BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクション コーディネーター (MS DTC) によって管理される、[!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクションの開始を指定します。  
    
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
BEGIN DISTRIBUTED { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *transaction_name*  
 MS DTC ユーティリティ内で分散管理トランザクションの追跡に使用する、ユーザー定義のトランザクション名を指定します。 *transaction_name* は識別子の規則に従っている必要があり、\<= 32 文字で指定する必要があります。  
  
 @*tran_name_variable*  
 MS DTC ユーティリティ内で分散管理トランザクションの追跡に使用するトランザクション名を含む、ユーザー定義の変数名を指定します。 変数は、**char**、**varchar**、**nchar**、または **nvarchar** データ型を使用して宣言する必要があります。  
  
## <a name="remarks"></a>Remarks  
 BEGIN DISTRIBUTED TRANSACTION ステートメントを実行する [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] インスタンスは、トランザクションの発行元となり、トランザクションの完了を制御します。 このセッションで後続の COMMIT TRANSACTION または ROLLBACK TRANSACTION ステートメントを実行すると、制御側のインスタンスから MS DTC に対して、関係する全インスタンス間の分散トランザクションの完了を管理するように要求されます。  
  
 トランザクション レベルのスナップショット分離では、分散トランザクションはサポートされません。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のリモート インスタンスが分散トランザクションに参加するのは、主として、分散トランザクションに既に参加しているセッションで、リンク サーバーを参照する分散クエリが実行された場合です。  
  
 たとえば、BEGIN DISTRIBUTED TRANSACTION が ServerA で実行されると、そのセッションでは ServerB のストアド プロシージャと ServerC のストアド プロシージャが呼び出されます。 ServerC のストアド プロシージャでは ServerD に対して分散クエリが実行され、この結果、4 台のコンピューターすべてが分散トランザクションに参加します。 ServerA の[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスは、トランザクションの発行元の制御インスタンスになります。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクションに含まれているセッションでは、分散トランザクションへの明示的な参加を目的とした、別のセッションに渡すことのできるトランザクション オブジェクトは取得されません。 リモート サーバーがトランザクションに参加できるのは、リモート サーバーが分散クエリまたはリモート ストアド プロシージャ コールの対象になる場合だけです。  
  
 ローカル トランザクション内で分散クエリを実行するとき、クエリの対象である OLE DB データ ソースで ITransactionLocal がサポートされている場合は、トランザクションは自動的に分散トランザクションに昇格します。 クエリの対象である OLE DB データ ソースで ITransactionLocal がサポートされていない場合は、分散クエリで読み取り専用操作だけが許可されます。  
  
 分散トランザクションに既に参加しているセッションでは、リモート サーバーを参照するリモート ストアド プロシージャが実行されます。  
  
 **sp_configure remote proc trans** オプションを使用すると、ローカル トランザクション内のリモート ストアド プロシージャを呼び出したときに、自動的にローカル トランザクションを MS DTC 管理の分散トランザクションに昇格させるかどうかを制御できます。 接続レベルの SET オプション REMOTE_PROC_TRANSACTIONS を使用した場合は、**sp_configure remote proc trans** で設定したサーバーの既定値をオーバーライドします。このオプションをオンに設定した状態でリモート ストアド プロシージャを呼び出すと、ローカル トランザクションは分散トランザクションに昇格します。 この場合、MS DTC トランザクションを作成した接続がトランザクションの発行元になります。 COMMIT TRANSACTION では、MS DTC により調整されるコミットが開始されます。 **sp_configure remote proc trans** オプションを ON に設定した場合、ローカル トランザクション内のリモート ストアド プロシージャ コールは分散トランザクションの一部として自動的に保護されます。特別に BEGIN TRANSACTION の代わりに BEGIN DISTRIBUTED TRANSACTION を実行するようアプリケーションを書き換える必要はありません。  
  
 分散トランザクションの環境と処理の詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーターのマニュアルを参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssDE](../../includes/ssde-md.md)] のローカル インスタンスとリモート サーバーのインスタンス両方の [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースから候補者を削除します。 ローカルとリモートの両方のデータベースで、トランザクションのコミットまたはロールバックのいずれかが実行されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスが動作しているコンピューターに現在 MS DTC がインストールされていない場合、この例を実行するとエラー メッセージが出力されます。 MS DTC のインストールの詳細については、Microsoft 分散トランザクション コーディネーターのマニュアルを参照してください。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN DISTRIBUTED TRANSACTION;  
-- Delete candidate from local instance.  
DELETE AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
-- Delete candidate from remote instance.  
DELETE RemoteServer.AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
