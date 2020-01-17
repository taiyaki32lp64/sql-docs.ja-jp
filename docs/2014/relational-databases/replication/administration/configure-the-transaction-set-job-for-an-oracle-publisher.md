---
title: Oracle パブリッシャー (レプリケーション TRANSACT-SQL プログラミング) のトランザクション セット ジョブの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48282f08df588f54b6f03a0b99c58a2f0cf039ac
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793545"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Oracle パブリッシャー用のトランザクション セット ジョブの構成 (レプリケーション Transact-SQL プログラミング)
  **Xactset** ジョブは、Oracle パブリッシャーで実行されているレプリケーションがトランザクション セットを生成するために作成する Oracle データベース ジョブです。Oracle パブリッシャーにログ リーダー エージェントが接続されていない場合に使用されます。 このジョブは、レプリケーションのストアド プロシージャを使用し、ディストリビューターからプログラムによって有効化したり構成することができます。 詳細については、「[Performance Tuning for Oracle Publishers](../non-sql/performance-tuning-for-oracle-publishers.md)」 (Oracle パブリッシャーのパフォーマンス チューニング) を参照してください。  
  
### <a name="to-enable-the-transaction-set-job"></a>トランザクション セット ジョブを有効にするには  
  
1.  Oracle パブリッシャーで、 **job_queue_processes** 初期化パラメーターに、Xactset ジョブを実行できるだけの十分な値を設定します。 このパラメーターの詳細については、Oracle パブリッシャー用データベースのマニュアルを参照してください。  
  
2.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql) を実行します。 Oracle パブリッシャーの名前を指定 **\@パブリッシャー**、値の`xactsetbatching`の **\@propertyname**の値と`enabled`の **\@propertyvalue**します。  
  
3.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql) を実行します。 Oracle パブリッシャーの名前を指定 **\@パブリッシャー**、@property`xactsetjobinterval`の **\@propertyname**、およびジョブの実行間隔を分単位での **\@propertyvalue**します。  
  
4.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql) を実行します。 Oracle パブリッシャーの名前を指定 **\@パブリッシャー**、値の`xactsetjob`の **\@propertyname**の値と`enabled`の **\@propertyvalue**します。  
  
### <a name="to-configure-the-transaction-set-job"></a>トランザクション セット ジョブを構成するには  
  
1.  (省略可能) ディストリビューターで [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql) を実行します。 Oracle パブリッシャーの名前を指定 **\@パブリッシャー**します。 これにより、パブリッシャーの **Xactset** ジョブのプロパティが返されます。  
  
2.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql) を実行します。 Oracle パブリッシャーの名前を指定 **\@パブリッシャー**を設定する Xactset ジョブ プロパティの名前 **\@propertyname**、新しい設定と **\@propertyvalue**します。  
  
3.  (省略可) 設定対象の各 Xactset ジョブ プロパティについて、手順 2. を繰り返します。 変更するときに、`xactsetjobinterval`プロパティを有効にすると新しい間隔、Oracle パブリッシャーでジョブを再起動する必要があります。  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>トランザクション セット ジョブのプロパティを表示するには  
  
1.  ディストリビューターで [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql)を実行します。 Oracle パブリッシャーの名前を指定 **\@パブリッシャー**します。  
  
### <a name="to-disable-the-transaction-set-job"></a>トランザクション セット ジョブを無効にするには  
  
1.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql) を実行します。 Oracle パブリッシャーの名前を指定 **\@パブリッシャー**、値の`xactsetjob`の **\@propertyname**の値と`disabled`の **\@propertyvalue**します。  
  
## <a name="example"></a>例  
 次の例では、 `Xactset` ジョブを有効にし、実行間隔を 3 分に設定しています。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>関連項目  
 [Oracle パブリッシャーのパフォーマンス チューニング](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
