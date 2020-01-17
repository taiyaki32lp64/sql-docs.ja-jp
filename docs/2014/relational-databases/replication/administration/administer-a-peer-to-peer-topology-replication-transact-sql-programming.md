---
title: ピア ツー ピア トポロジの管理 (レプリケーション Transact-SQL プログラミング) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0cabfb4cd21de54dad2be1323fd29d8bb3bf076
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629715"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>ピア ツー ピア トポロジの管理 (レプリケーション Transact-SQL プログラミング)
  ピア ツー ピア トポロジの管理は通常のトランザクション レプリケーション トポロジの管理と似ていますが、特別な考慮が必要な部分が数多くあります。 ピア ツー ピア トポロジの管理が通常のトポロジ管理と最も異なる点は、ある種の変更を行うときにシステムを *停止*する必要があることです。 システムを停止するときには、すべてのノードでパブリッシュ済みテーブルの利用を停止し、各ノードが他のすべてのノードの変更を受け取っていることを確認します。 詳細については、「[レプリケーション トポロジの停止 &#40;レプリケーション Transact-SQL プログラミング&#41;](quiesce-a-replication-topology-replication-transact-sql-programming.md)」を参照してください。  
  
> [!NOTE]  
>  ピア ツー ピア トポロジでは、ディストリビューターはプル サブスクライバーより前の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のバージョンを使用できません。  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>既存の構成にアーティクルを追加するには  
  
1.  システムを停止します。  
  
2.  トポロジ内の各ノードでディストリビューション エージェントを停止します。 詳細については、「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」または「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」を参照してください。  
  
3.  CREATE TABLE ステートメントを実行して、トポロジ内の各ノードに新しいテーブルを追加します。  
  
4.  [bcp ユーティリティ](../../../tools/bcp-utility.md)を使用して、全ノードの新しいテーブルにデータを一括コピーします。  
  
5.  [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) を実行して、トポロジ内の各ノードに新しいアーティクルを作成します。 詳しくは、「 [アーティクルを定義](../publish/define-an-article.md)」をご覧ください。  
  
    > [!NOTE]  
    >  [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) の実行後、レプリケーションによってトポロジ内のサブスクリプションにアーティクルが自動的に追加されます。  
  
6.  トポロジ内の各ノードでディストリビューション エージェントを再起動します。  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>パブリケーション データベースのスキーマを変更するには  
  
1.  システムを停止します。  
  
2.  データ定義言語 (DDL) ステートメントを実行して、パブリッシュ済みテーブルのスキーマを変更します。 サポートされるスキーマ変更の詳細については、「[パブリケーション データベースでのスキーマの変更](../publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
3.  パブリッシュ済みテーブルの利用を再開する前に、再びシステムを停止します。 これにより、新しいデータ変更がレプリケートされる前に、すべてのノードでスキーマ変更が受け取られます。  
  
## <a name="example"></a>例  
 次の例は、2 つのノードを持つ既存のピア ツー ピア レプリケーション トポロジに新しいテーブル アーティクルを追加する方法を示しています。  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createtables)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_cmdline)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createarticle)]  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理に関する FAQ](frequently-asked-questions-for-replication-administrators.md)   
 [SQL Server データベースのバックアップと復元](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [ピア ツー ピア トランザクション レプリケーション](../transactional/peer-to-peer-transactional-replication.md)  
  
  
