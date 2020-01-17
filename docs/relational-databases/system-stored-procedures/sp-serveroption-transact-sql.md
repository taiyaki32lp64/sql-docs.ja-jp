---
title: sp_serveroption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_serveroption_TSQL
- sp_serveroption
dev_langs:
- TSQL
helpviewer_keywords:
- 7343 (Database Engine error)
- sp_serveroption
ms.assetid: 47d04a2b-dbf0-4f15-bd9b-81a2efc48131
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1fcd6f158908893ce5eb86c24a3bb3882867bc2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104382"
---
# <a name="spserveroption-transact-sql"></a>sp_serveroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  リモート サーバーおよびリンク サーバーのサーバー オプションを設定します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>引数  
`[ @server = ] 'server'` オプションを設定する対象のサーバーの名前です。 *server* のデータ型は **sysname**で、既定値はありません。  
  
`[ @optname = ] 'option_name'` 指定したサーバーに設定するオプションです。 *option_name*は**varchar (** 35 **)** 、既定値はありません。 *option_name*値は次のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**collation compatible**|リンク サーバーに対する分散クエリの実行に影響を与えます。 このオプションに **true** を設定した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、文字セットと照合順序 (並べ替え順) に関して、リンク サーバー内のすべての文字がローカル サーバーと互換性があると仮定します。 これにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からプロバイダーに文字を含む列の比較を送信できるようになります。 このオプションが設定されていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では文字列を含む列の比較の評価は常にローカルで行われます。<br /><br /> このオプションは、リンク サーバーに対応するデータ ソースがローカル サーバーと同じ文字セットと並べ替え順を持っていることが確認できている場合のみ設定します。|  
|**collation name**|**use remote collation** が **true**、かつ、データ ソースが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースでない場合に、リモート データ ソースが使用する照合順序の名前を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]がサポートしている照合順序名のいずれかを指定する必要があります。<br /><br /> このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外の OLE DB データ ソースにアクセスし、その照合順序が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序のいずれかと一致する場合に使用します。<br /><br /> リンク サーバーは、そのサーバー内のすべての列で使用される単一の照合順序をサポートしている必要があります。 リンク サーバーが、単一のデータ ソース内で複数の照合順序をサポートしている、またはリンク サーバーの照合順序が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序のいずれかと一致するかどうかが判断できない場合は、このオプションを設定しないでください。|  
|**connect timeout**|リンク サーバーに接続するためのタイムアウトの値（秒単位）。<br /><br /> 値が **0** の場合は、**sp_configure** の規定値を使用します。|  
|**data access**|分散クエリ アクセスに対してリンク サーバーを有効または無効にします。 **sp_addlinkedserver** を介して追加された **sys.server** エントリにのみ使用可能です。|  
|**dist**|ディストリビューターです。|  
|**lazy schema validation**|リモート テーブルのスキーマをチェックするかどうかを指定します。<br /><br /> **true** の場合、クエリの先頭でのリモート テーブルのチェックをスキップします。|  
|**pub**|パブリッシャーです。|  
|**query timeout**|リンク サーバーに対するクエリのタイムアウト値です。<br /><br /> 値が **0** の場合は、**sp_configure** の規定値を使用します。|  
|**rpc**|特定のサーバーから RPC を有効にします。|  
|**rpc out**|特定のサーバーへの RPC を有効にします。|  
|**sub**|サブスクライバー。|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**use remote collation**|リモート列とローカル サーバーのどちらの照合順序を使用するかを指定します。<br /><br /> **true** の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースに対してはリモート列の照合順序を使用し、**以外のデータ ソースに対しては**collation name[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で指定した照合順序を使用します。<br /><br /> **false** の場合、分散クエリは常にローカル サーバーの既定の照合順序を使用します。**collation name** とリモート列の照合順序は無視されます。 既定値は **false** です。 **false** の値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 で使用される照合順序セマンティクスと互換性があります。|  
|**remote proc transaction promotion**|このオプションを使用して、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) トランザクションにより、サーバー間のプロシージャのアクションを保護します。 このオプションが TRUE (またはON) の場合はリモート ストアド プロシージャを呼び出す分散トランザクションを開始し、トランザクションは MS DTC に参加します。 リモート ストアド プロシージャを呼び出す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、トランザクションを実行したインスタンスであり、このインスタンスによってトランザクションが制御されます。 この接続に対して引き続き COMMIT TRANSACTION または ROLLBACK TRANSACTION ステートメントを実行すると、制御側のインスタンスは MS DTC 対して、コンピューター間の分散トランザクションの完了を管理することを要求します。<br /><br /> [!INCLUDE[tsql](../../includes/tsql-md.md)]分散トランザクションが開始された後は、リンク サーバーとして定義されている他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対し、リモート ストアド プロシージャを呼び出すことができます。 リンク サーバーはすべて [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散トランザクション、および MS DTC により、各リンク サーバーに対して、トランザクションが完了したことです。<br /><br /> このオプションが FALSE (または OFF) に設定されている場合、ローカル トランザクションは、リンク サーバー上のリモート プロシージャ コールの呼び出し中に分散トランザクションに昇格されません。<br /><br /> サーバー間のプロシージャ コールを行う前にトランザクションが既に分散トランザクションである場合、このオプションに効力はありません。 リンク サーバーに対するプロシージャ コールは、同じ分散トランザクションで実行されます。<br /><br /> サーバー間のプロシージャ コールを行う前場合に、の接続でアクティブなトランザクションがないし、このオプションに影響がありません。 プロシージャは、アクティブなトランザクションなしのリンク サーバーに対してし実行します。<br /><br /> このオプションの既定値は TRUE (ON) です。|  
  
`[ @optvalue = ] 'option_value'` 指定するかどうか、 *option_name*を有効にする (**TRUE**または**で**) か無効 (**FALSE**または**オフ**). *option_value*は**varchar (** 10 **)** 、既定値はありません。  
  
 *option_value*には、**connect timeout** および **query timeout** オプションの場合、負でない整数を指定できます。 **collation name** オプションの場合、*option_value* には照合順序名または NULL を指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **collation compatible** オプションが TRUE に設定されている場合、**collation name** は自動的に NULL に設定されます。 **collation name** が NULL 以外の値に設定されている場合、**collation compatible** は自動的に FALSE に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER ANY LINKED SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスに対応するリンク サーバー `SEATTLE3` を、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスと互換性のある照合順序になるよう構成します。  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>関連項目  
 [分散クエリ ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropdistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
