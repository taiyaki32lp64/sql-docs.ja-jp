---
title: SET REMOTE_PROC_TRANSACTIONS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REMOTE_PROC_TRANSACTIONS_TSQL
- SET REMOTE_PROC_TRANSACTIONS
- REMOTE_PROC_TRANSACTIONS
- SET_REMOTE_PROC_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- SET REMOTE_PROC_TRANSACTIONS statement
- distributed transactions [SQL Server], starting
- REMOTE_PROC_TRANSACTIONS option
- active transactions
ms.assetid: 4d284ae9-3f5f-465a-b0dd-1328a4832a03
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0d94799898517b2d75ce6a1add308f0831b112ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132817"
---
# <a name="set-remoteproctransactions-transact-sql"></a>SET REMOTE_PROC_TRANSACTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ローカル トランザクションがアクティブ状態のときにリモート ストアド プロシージャを実行した場合、[!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクション コーディネーター (MS DTC) によって管理される [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクションを開始するように指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]このオプションは、リモート ストアド プロシージャを使用する、旧バージョンのアプリケーションとの互換性のために用意されています。 リモート ストアド プロシージャを呼び出す代わりに、リンク サーバーを参照した分散クエリを使用してください。 これらは、[sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) を使って定義されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET REMOTE_PROC_TRANSACTIONS { ON | OFF }   
```  
  
## <a name="arguments"></a>引数  
 ON | OFF  
 ON の場合、ローカル トランザクションからリモート ストアド プロシージャが実行されると、[!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクションが開始されます。 OFF の場合、ローカル トランザクションからリモート ストアド プロシージャを呼び出しても、[!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクションは開始されません。  
  
## <a name="remarks"></a>Remarks  
 REMOTE_PROC_TRANSACTIONS が ON の場合、リモート ストアド プロシージャを呼び出すと分散トランザクションが開始され、トランザクションは MS DTC に参加します。 リモート ストアド プロシージャを呼び出す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、トランザクションを実行したインスタンスであり、このインスタンスによってトランザクションが制御されます。 この接続に対して引き続き COMMIT TRANSACTION または ROLLBACK TRANSACTION ステートメントを実行すると、制御側のインスタンスは MS DTC 対して、コンピューター間の分散トランザクションの完了を管理することを要求します。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクションが開始された後は、リモート サーバーとして定義されている他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対し、リモート ストアド プロシージャを呼び出すことができます。 リモート サーバーはすべて [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクションに参加することになります。MS DTC では、各リモート サーバーでトランザクションが完了したかどうかが確認されます。  
  
 REMOTE_PROC_TRANSACTIONS は接続レベルの設定であり、インスタンス レベルの **sp_configure remote proc trans** オプションをオーバーライドします。  
  
 REMOTE_PROC_TRANSACTIONS が OFF の場合、ローカル トランザクションの一部としてリモート ストアド プロシージャは呼び出されません。 リモート ストアド プロシージャによる変更は、ストアド プロシージャの完了時にコミットまたはロールバックされます。 リモート ストアド プロシージャを呼び出した接続によって実行される後続の COMMIT TRANSACTION または ROLLBACK TRANSACTION ステートメントは、ストアド プロシージャによる処理に影響を与えません。  
  
 REMOTE_PROC_TRANSACTIONS オプションは互換性のためのオプションであり、**sp_addserver** でリモート サーバーとして定義された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対してリモート ストアド プロシージャを呼び出す場合にのみ、影響を及ぼします。 このオプションは、インスタンス上でストアド プロシージャを実行する分散クエリには適用されません。このインスタンスは、**sp_addlinkedserver** でリンク サーバーとして定義されたインスタンスです。  
  
 SET REMOTE_PROC_TRANSACTIONS は、解析時ではなく実行時に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
