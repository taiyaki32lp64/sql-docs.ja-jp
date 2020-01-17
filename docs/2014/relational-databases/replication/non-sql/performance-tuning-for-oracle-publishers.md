---
title: Oracle パブリッシャーのパフォーマンス チューニング | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d735fc81e38354630eb4486bbf6ca2bdae570e6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022234"
---
# <a name="performance-tuning-for-oracle-publishers"></a>Oracle パブリッシャーのパフォーマンス チューニング
  Oracle のパブリッシング アーキテクチャは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のパブリッシング アーキテクチャに似ています。したがって、「 [Enhance General Replication Performance](../administration/enhance-general-replication-performance.md)」で紹介されているチューニング全般の推奨事項に従うことが、Oracle レプリケーションのパフォーマンスをチューニングするための第一歩となります。  
  
 それに加えて、Oracle パブリッシャーには、パフォーマンスに関連するオプションが 2 つあります。  
  
-   適切な公開オプションを指定するには。Oracle または Oracle Gateway。  
  
-   パブリッシャーの変更を適切な間隔で処理するようにトランザクション セット ジョブを構成します。  
  
## <a name="specifying-the-appropriate-publishing-option"></a>適切なパブリッシング オプションの指定  
 [Oracle (ゲートウェイ)] を選択すると、[Oracle (完全)] より高いパフォーマンスが得られますが、このオプションは、複数のトランザクション パブリケーションで同じテーブルをパブリッシュする場合は使用できません。 テーブルを表示できるのは、最大で 1 つのトランザクション パブリケーションと、任意の数のスナップショット パブリケーションになります。 複数のトランザクション パブリケーションで同じテーブルをパブリッシュする必要がある場合は、[Oracle (完全)] を選択します。 このオプションは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターで Oracle パブリッシャーを識別する際に指定します。 詳細については、「 [Create a Publication from an Oracle Database](../publish/create-a-publication-from-an-oracle-database.md)」を参照してください。  
  
## <a name="configuring-the-transaction-set-job"></a>トランザクション セット ジョブの構成  
 パブリッシュされた Oracle テーブルに対する変更は、トランザクション セットと呼ばれるグループで処理されます。 トランザクションの一貫性を確保するために、各トランザクション セットはディストリビューション データベースで 1 つのトランザクションとしてコミットされます。 トランザクション セットが大きくなりすぎると、1 つのトランザクションとして効率的に処理できなくなります。  
  
 既定では、トランザクション セットはログ リーダー エージェントによってのみ作成されます。 変更が頻繁に行われているときにログ リーダー エージェントが実行されていなかったり、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターから Oracle パブリッシャーに接続できなかったりすると、トランザクション セットが極端に大きくなる可能性があります。 この問題を防ぐには、ログ リーダー エージェントが実行されていなかったり Oracle パブリッシャーに接続できなかったりしてもトランザクション セットが定期的に作成されるようにします。  
  
 トランザクション セットは、Xactset ジョブ (レプリケーションによってインストールされる Oracle データベース ジョブ) で作成できます。Xactset ジョブは、ログ リーダー エージェントと同じメカニズムを使ってトランザクション セットを作成します。 このジョブが実行されるたびに、新しいトランザクション セットが作成されます。 次にログ リーダー エージェントが実行されたときに、それまでに作成されたトランザクション セットが処理されます。 既存のトランザクション セットがすべて処理された後にまだ保留中の変更がある場合は、ログ リーダー エージェントが 1 つ以上のトランザクション セットを追加で作成して処理します。  
  
 トランザクション セット ジョブを構成するには、「[Configure the Transaction Set Job for an Oracle Publisher](../administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)」 (Oracle パブリッシャー用にトランザクション セット ジョブを構成する方法 (レプリケーション Transact-SQL プログラミング)) を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Configure an Oracle Publisher (Oracle パブリッシャーの構成)](configure-an-oracle-publisher.md)   
 [Oracle パブリッシングの概要](oracle-publishing-overview.md)  
  
  
