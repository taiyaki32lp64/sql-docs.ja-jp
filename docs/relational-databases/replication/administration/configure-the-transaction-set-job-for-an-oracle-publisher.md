---
title: トランザクション セット ジョブの構成 (Oracle パブリッシャー)
description: Oracle パブリッシャーが SQL Server サブスクライバーにパブリッシュする場合にトランザクション セット ジョブを構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 8f25f3d9c9a69d3a8f87e8a4eb1886f31092940f
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322056"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher"></a>Oracle パブリッシャー用のトランザクション セット ジョブの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Xactset** ジョブは、Oracle パブリッシャーで実行されているレプリケーションがトランザクション セットを生成するために作成する Oracle データベース ジョブです。Oracle パブリッシャーにログ リーダー エージェントが接続されていない場合に使用されます。 このジョブは、レプリケーションのストアド プロシージャを使用し、ディストリビューターからプログラムによって有効化したり構成することができます。 詳細については、「[Performance Tuning for Oracle Publishers](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)」 (Oracle パブリッシャーのパフォーマンス チューニング) を参照してください。  
  
### <a name="to-enable-the-transaction-set-job"></a>トランザクション セット ジョブを有効にするには  
  
1.  Oracle パブリッシャーで、 **job_queue_processes** 初期化パラメーターに、Xactset ジョブを実行できるだけの十分な値を設定します。 このパラメーターの詳細については、Oracle パブリッシャー用データベースのマニュアルを参照してください。  
  
2.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) を実行します。 **\@publisher** に Oracle パブリッシャーの名前を、 **\@propertyname** に **xactsetbatching** を、 **\@propertyvalue** に **enabled** を指定します。  
  
3.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) を実行します。 **\@publisher** に Oracle パブリッシャーの名前を、 **\@propertyname** に **xactsetjobinterval** を、 **\@propertyvalue** にジョブの実行間隔 (分) を指定します。  
  
4.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) を実行します。 **\@publisher** に Oracle パブリッシャーの名前を、 **\@propertyname** に **xactsetjob** を、 **\@propertyvalue** に **enabled** を指定します。  
  
### <a name="to-configure-the-transaction-set-job"></a>トランザクション セット ジョブを構成するには  
  
1.  (省略可能) ディストリビューターで [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) を実行します。 **\@publisher** に Oracle パブリッシャーの名前を指定します。 これにより、パブリッシャーの **Xactset** ジョブのプロパティが返されます。  
  
2.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) を実行します。 **\@publisher**、 **\@propertyname**、 **\@propertyvalue** に、それぞれ Oracle パブリッシャーの名前、設定する Xactset ジョブ プロパティの名前、新しい設定を指定します。  
  
3.  (省略可) 設定対象の各 Xactset ジョブ プロパティについて、手順 2. を繰り返します。 **xactsetjobinterval** プロパティを変更した場合は、Oracle パブリッシャーでジョブを再起動しないと新しい間隔が反映されません。  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>トランザクション セット ジョブのプロパティを表示するには  
  
1.  ディストリビューターで [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md)を実行します。 **\@publisher** に Oracle パブリッシャーの名前を指定します。  
  
### <a name="to-disable-the-transaction-set-job"></a>トランザクション セット ジョブを無効にするには  
  
1.  ディストリビューターで、[sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) を実行します。 **\@publisher** に Oracle パブリッシャーの名前を、 **\@propertyname** に **xactsetjob** を、 **\@propertyvalue** に **disabled** を指定します。  
  
## <a name="example"></a>例  
 次の例では、 `Xactset` ジョブを有効にし、実行間隔を 3 分に設定しています。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## <a name="see-also"></a>参照  
 [Oracle パブリッシャーのパフォーマンス チューニング](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
