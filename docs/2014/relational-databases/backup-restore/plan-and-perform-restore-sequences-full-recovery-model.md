---
title: 復元シーケンスの計画と実行 (完全復旧モデル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], planning for
- full recovery model [SQL Server], planning restore sequences
ms.assetid: 9cbefaf8-d2b6-41c9-83fc-b3807a841fe2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 08898d4c7a324a97fc0e44ef45b15dba90d42a1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921849"
---
# <a name="plan-and-perform-restore-sequences-full-recovery-model"></a>復元シーケンスの計画と実行 (完全復旧モデル)
  このトピックでは、主に完全復旧モデルが使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの復元シーケンスを計画し、実行する方法について説明します。 *復元シーケンス* は、1 つ以上の連続した [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントです。 通常、復元シーケンスでは、復元対象のデータベース、ファイル、ページのコンテンツの初期化 (データ コピー フェーズ)、ログに記録されたトランザクションのロールフォワード (再実行フェーズ)、コミットされていないトランザクションのロールバック (元に戻すフェーズ) が実行されます。  
  
 単純な復元シーケンスの場合、必要なのはデータベースの完全バックアップ、差分バックアップ、およびそれ以降のログ バックアップのみです。 このような場合は、適切な復元シーケンスの構築は簡単です。 たとえば、障害が発生した時点までデータベース全体を復元するには、まずアクティブなトランザクション ログ (ログの *末尾* ) をバックアップします。 次に、データベースの最新の完全バックアップ、最新の差分バックアップ (存在する場合) の順に復元してから、それ以降のすべてのログ バックアップを作成順に復元します。  
  
 適切な復元シーケンスの構築がもっと複雑になる場合もあります。 たとえば、複数のファイル バックアップが必要になったり、特定の時点へのデータの復元が必要になる場合があります。 非常に複雑な復元シーケンスでは、1 つ以上の復旧分岐にまたがる、分岐した復旧パスをたどることが必要になる場合もあります。  
  
> [!NOTE]  
>  *復旧パス* は、データベースをある特定の時点 (復旧ポイント) の状態にするための、連続したデータおよびログ バックアップです。 復旧パスは、データベースの一貫性を維持しつつ、その内容がどのような操作によって、時間の経過と共にどのように変化してきたかを具体的に表します。 開始ポイント (LSN、GUID) から終了ポイント (LSN、GUID) までの一連の LSN が 1 つの復旧パスとなります。 復旧パスの LSN は、開始ポイントから終了ポイントまですべてが 1 つの復旧ブランチに属する場合もあれば、複数の復旧ブランチに属する場合もあります。  
  
## <a name="to-plan-a-restore-sequence"></a>復元シーケンスを計画するには  
 復元シーケンスを開始する前に、次の手順を実行します。  
  
1.  データベースのログ末尾のバックアップを (作成できる場合は) 作成します。 詳細については、「[ログ末尾のバックアップ &#40;SQL Server&#41;](tail-log-backups-sql-server.md)」を参照してください。  
  
2.  目的の復旧ポイントを決定します。  
  
     目的の復旧ポイントとして、トランザクション ログ バックアップ内の任意の時点またはマークを選択することができます。 詳細については、「[SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」または「[マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル#41;](use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
3.  実行する復元の種類を決定します。 詳細については、「 [復元と復旧の概要 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)」を参照してください。  
  
4.  必要なバックアップを特定し、必要なメディア セットとバックアップ デバイスが使用可能であることを確認します。 詳細については、「[バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)」と「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
## <a name="to-perform-a-restore-sequence"></a>復元シーケンスを実行するには  
 復元シーケンスを実行するには、次の手順を実行します。  
  
1.  シーケンスを開始するために、データベース バックアップ、部分バックアップ、1 つ以上のファイル バックアップなど、1 つ以上のデータ バックアップを復元します。  
  
2.  必要に応じて、これらの完全バックアップを基にした最新の差分バックアップを復元します。  
  
     復元する各完全バックアップがいずれかの差分バックアップのベースであるかどうかを確認します。 その場合は、最新の差分バックアップを (復元できる場合は) 復元します。 詳細については、「 [差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)」を参照してください。  
  
3.  ログ バックアップを順番に復元することによって、データベースをロールフォワードします。最後に復旧ポイントを含むログ バックアップを復元します。 すべてのログ バックアップを適用する必要があるかどうかは、どのログ バックアップに目的の復旧ポイントが含まれているかによって、次のように異なります。  
  
    -   復旧ポイントが障害の発生時点である場合は、最後に復元したデータ バックアップ (完全バックアップまたは差分バックアップ) 以降に作成されたすべてのログ バックアップを復元する必要があります。 詳細については、「[トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)」を参照してください。  
  
    -   特定の時点への復元の場合は、最新のログ バックアップを復元する必要がないことがあります。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用する場合、データベース復旧アドバイザーによって、指定された時点に復元するために必要なバックアップだけが選択されます。 これらのバックアップは、特定の時点への復元用として推奨される復元プランを示しています。 詳細については、「[SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
## <a name="restarting-a-restore-sequence"></a>復元シーケンスの再実行  
 復元シーケンスの結果に問題がある場合、復元シーケンスを停止し、最初から再実行することができます。 たとえば、誤ってログ バックアップを多く復元しすぎて、目的の復旧ポイントを超えてしまった場合は、目的の復旧ポイントを含むログ バックアップまでの復元シーケンスを再実行する必要があります。  
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [データベースの全体復元 &#40;完全復旧モデル&#41;](complete-database-restores-full-recovery-model.md)   
 [オンライン復元 &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [ファイル復元 &#40;完全復旧モデル&#41;](file-restores-full-recovery-model.md)   
 [ページ復元 &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
