---
title: レプリケーション管理の推奨事項 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, best practices
- replication [SQL Server], administering
ms.assetid: 850e8a87-b34c-4934-afb5-a1104f118ba8
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 04cfff3e2772f945d01093bab15246924a104b2b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768839"
---
# <a name="best-practices-for-replication-administration"></a>レプリケーション管理の推奨事項
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーションを構成したら、レプリケーション トポロジの管理方法について理解することが重要です。 このトピックでは、さまざまな分野における推奨事項について説明し、また各分野の詳細情報へのリンクも提供します。 このトピックで説明するベスト プラクティスのガイダンスに従うだけでなく、次のよく寄せられる質問のトピックに目を通し、一般的な疑問や問題について理解することをお勧めします: 「[レプリケーションの管理者に関してよく寄せられる質問](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)」。  
  
 推奨事項について理解するには、以下の 2 つの分野に分けて行うのが効果的です。  
  
-   以下の情報は、すべてのレプリケーション トポロジについて実装する必要のある推奨事項を示しています。  
  
    -   バックアップと復元方法の開発およびテスト  
  
    -   レプリケーション トポロジ スクリプトの作成  
  
    -   しきい値および警告の作成  
  
    -   レプリケーション トポロジの監視  
  
    -   パフォーマンス基準の確立と必要に応じたレプリケーションの調整  
  
-   以下の情報は、レプリケーション トポロジについて、必須ではないが、考慮すべき推奨事項を示しています。  
  
    -   定期的なデータの検証  
  
    -   プロファイルを使用したエージェント パラメーターの調整  
  
    -   パブリケーションおよびディストリビューションの保有期間の調整  
  
    -   アプリケーション要件が変更された場合のアーティクルおよびパブリケーションのプロパティの変更方法についての理解  
  
    -   アプリケーション要件が変更された場合のスキーマの変更方法についての理解  
  
## <a name="develop-and-test-a-backup-and-restore-strategy"></a>バックアップと復元方法の開発およびテスト  
 すべてのデータベースは定期的にバックアップする必要があります。また、バックアップの復元機能についても定期的にテストする必要があります。これらの要件は、レプリケートされたデータベースの場合についても同様です。 以下のデータベースは定期的にバックアップする必要があります。  
  
-   パブリケーション データベース  
  
-   ディストリビューション データベース  
  
-   サブスクリプション データベース  
  
-   パブリッシャー、ディストリビューター、すべてのサブスクライバーの**msdb** データベースおよび **master** データベース  
  
 レプリケートされたデータベースでは、データのバックアップと復元に対する特別な注意が必要です。 詳細については、「 [レプリケートされたデータベースのバックアップと復元](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)」を参照してください。  
  
## <a name="script-the-replication-topology"></a>レプリケーション トポロジ スクリプトの作成  
 トポロジ内のすべてのレプリケーション コンポーンネントは、ディザスター リカバリー計画の一部としてスクリプト化され、スクリプトはタスクの繰り返しの自動化にも使用することができます。 スクリプトには、パブリケーションやサブスクリプションなどスクリプト化されたレプリケーション コンポーネントを実装するために必要な [!INCLUDE[tsql](../../../includes/tsql-md.md)] システム ストアド プロシージャが格納されます。 スクリプトはウィザード (パブリケーションの新規作成ウィザードなど) で作成することができ、コンポーネントの作成後、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して作成することもできます。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または **sqlcmd**を使用すると、スクリプトの表示、変更、および実行を行うことができます。 スクリプトをバックアップ ファイルと共に保存して、レプリケーション トポロジの再構成が必要な場合に使用できます。 詳細については、「 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)」を参照してください。  
  
 プロパティが変更された場合は、コンポーネントのスクリプトを再作成する必要があります。 トランザクション レプリケーションでカスタム ストアド プロシージャを使用している場合は、各プロシージャのコピーをスクリプトと共に保存しておく必要があります。プロシージャが変更された場合は、プロシージャのコピーも更新する必要があります (スキーマやアプリケーション要件が変更されると、通常、プロシージャが更新されます)。 カスタム プロシージャの詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
## <a name="establish-performance-baselines-and-tune-replication-if-necessary"></a>パフォーマンス基準の確立と必要に応じたレプリケーションの調整  
 レプリケーションを構成する前に、レプリケーションのパフォーマンスに影響を及ぼす要因について理解しておくことをお勧めします。  
  
-   サーバーおよびネットワークのハードウェア  
  
-   データベースの設計  
  
-   ディストリビューターの構成  
  
-   パブリケーションの設計およびオプション  
  
-   フィルターの設計および使用方法  
  
-   サブスクリプション オプション  
  
-   スナップショット オプション  
  
-   エージェント パラメーター  
  
-   メンテナンス  
  
 レプリケーションの構成を終えたら、パフォーマンス基準を策定することをお勧めします。パフォーマンス基準を策定することによって、アプリケーションおよびトポロジにおける通常のワークロードに対するレプリケーションの動作方法について判断できるようになります。 レプリケーション モニターおよびシステム モニターを使用し、以下に示すレプリケーション パフォーマンスの 5 つのディメンションについて標準となる数値を決定してください。  
  
-   待機時間 : レプリケーション トポロジにおいて、データの変更内容が各ノード間に反映されるまでの時間。  
  
-   スループット : 長期間にわたってシステムが維持できるレプリケーションの総利用状況 (一定期間内に配信されたコマンドで測定されます)。  
  
-   コンカレンシー数 : システムにおいて同時に実行可能なレプリケーションのプロセス数。  
  
-   同期の実行時間 : 同期処理が完了するまでに必要な時間。  
  
-   リソース消費量 : レプリケーション プロセスの結果として使用されるハードウェアおよびネットワークのリソース。  
  
 トランザクション レプリケーションに最も関連するのは待機時間およびスループットです。トランザクション レプリケーションを使用するシステムでは、一般的に短い待機時間と高いスループットが要求されるためです。 マージ レプリケーションに最も関連するのはコンカレンシー数と同期の実行時間です。マージ レプリケーションを使用するシステムでは多数のサブスクライバーが存在することが多く、これらのサブスクライバーに対してパブリッシャーが同時に多数の同期を行うことがあるためです。  
  
 基準となる数値を設定したら、レプリケーション モニターでしきい値を設定します。 詳細については、「[Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」 (レプリケーション モニターのしきい値と警告の設定) と「[Use Alerts for Replication Agent Events](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)」 (レプリケーション エージェント イベントに対する警告の使用) を参照してください。 パフォーマンスに関する問題が発生した場合は、上記のパフォーマンスの向上に関するトピックに目を通し、問題の解決に役立つ変更を適用することをお勧めします。  
  
## <a name="create-thresholds-and-alerts"></a>しきい値および警告の作成  
 レプリケーション モニターを使用すると、ステータスやパフォーマンスに関連したさまざまなしきい値を設定できます。 トポロジに対する適切なしきい値を設定することをお勧めします。しきい値に到達した場合は警告が表示されます。また、オプションで電子メール アカウントやポケットベルなどのデバイスに警告を送信することもできます。 詳細については、「 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)」を参照してください。  
  
 レプリケーションでは、しきい値の監視に関連する警告に加えて、レプリケーション エージェント アクションに対応する定義済みの警告を多数利用できます。 これらの警告を使用することで、管理者はレプリケーション トポロジの状態について常時把握することができます。 警告について説明したトピックに目を通し、管理ニーズに合った警告を使用することをお勧めします (必要に応じて新しい警告を追加することもできます)。 詳細については、「[レプリケーション エージェント イベントに対する警告の使用](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)」を参照してください。  
  
## <a name="monitor-the-replication-topology"></a>レプリケーション トポロジの監視  
 レプリケーション トポロジを配置し、しきい値と警告の構成を終えたら、レプリケーションを定期的に監視することをお勧めします。 レプリケーション トポロジの監視は、レプリケーションの配置における重要な側面です。 レプリケーション処理は分散環境で行われるため、レプリケーションに関連するすべてのコンピューターについてその利用状況と状態を追跡することが不可欠です。 レプリケーションの監視には以下のツールを使用できます。  
  
-   レプリケーション モニターは、レプリケーションの監視に最も重要なツールです。レプリケーション モニターを使用すると、レプリケーション トポロジ全体の状態を監視できます。 詳細については、「 [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication.md)」を参照してください。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] およびレプリケーション管理オブジェクト (RMO) には、レプリケーション監視用のインターフェイスが用意されています。 詳細については、「 [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication.md)」を参照してください。  
  
-   レプリケーションのパフォーマンスの監視には、システム モニターも役立ちます。 詳細については、「 [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md)」を参照してください。  
  
## <a name="validate-data-periodically"></a>定期的なデータの検証  
 レプリケーションでは検証は必須ではありませんが、トランザクション レプリケーションおよびマージ レプリケーションを行う場合には定期的に検証することをお勧めします。 検証を行うことによって、サブスクライバーのデータがパブリッシャーのデータに一致していることを検証できます。 検証が正常に行われるのは、パブリッシャーの変更内容がその時点ですべてサブスクライバーにレプリケートされていて (サブスクライバーでの更新がサポートされている場合は、サブスクライバーからパブリッシャーへも変更内容がレプリケートされ)、2 つのデータベースが同期している場合です。  
  
 パブリケーション データベースのバックアップ スケジュールに従って検証を行うことを推奨します。 たとえば、パブリケーション データベースを週に 1 回完全バックアップする場合は、検証もバックアップの終了後、週に 1 回行います。 詳細については、「[レプリケートされたデータの検証](../../../relational-databases/replication/validate-data-at-the-subscriber.md)」を参照してください。  
  
## <a name="use-agent-profiles-to-change-agent-parameters-if-necessary"></a>エージェント プロファイルによるエージェント パラメーターへの必要に応じた変更  
 エージェント プロファイルを使用すると、レプリケーション エージェントのパラメーターを簡単に設定できます。 エージェントのコマンド ラインでパラメーターを指定することもできますが、通常は定義済みのエージェント プロファイルを使用するか、パラメーターの値の変更が必要な場合新規プロファイルを作成します。 たとえば、マージ レプリケーションを使用中にサブスクライバーの接続をブロードバンドからダイヤルアップに変更する場合、マージ エージェントに対して **低速リンク** プロファイルの使用を検討してください。このプロファイルでは、低速通信リンクにより適したパラメーターのセットが使用されます。 詳しくは、「 [レプリケーション エージェント プロファイル](../../../relational-databases/replication/agents/replication-agent-profiles.md)」をご覧ください。  
  
## <a name="adjust-publication-and-distribution-retention-periods-if-necessary"></a>パブリケーションおよびディストリビューションの保有期間の必要に応じた調整  
 トランザクション レプリケーションとマージ レプリケーションでは、ディストリビューション データベースでのトランザクションの保有期間、およびサブスクリプションの同期頻度を決定する保有期間が使用されます。 最初は既定の設定を使用することをお勧めしますが、トポロジを監視して、設定を調整する必要があるかどうかを確認することをお勧めします。 たとえば、マージ レプリケーションの場合、パブリケーションの保有期間 (既定では 14 日間) によって、システム テーブルにおけるメタデータの保有期間が決定されます。 サブスクリプションを常に 5 日以内に同期する場合は、この期間を短くすることを検討してください。こうすることにより、メタデータが削減され、パフォーマンスの向上につながる場合があります。 詳細については、「 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)」を参照してください。  
  
## <a name="understand-how-to-modify-publications-if-application-requirements-change"></a>アプリケーション要件が変更された場合のスキーマの変更方法についての理解  
 パブリケーションの作成後、アーティクルの追加や削除、またはパブリケーションおよびアーティクルのプロパティの変更が必要になる場合があります。 ほとんどの変更はパブリケーションの作成後に行うことができますが、場合によっては、パブリケーションのスナップショットの新規生成やパブリケーションに対するサブスクリプションの再初期化が必要になります。 詳細については、「[パブリケーションおよびアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)」と「[既存のパブリケーションでのアーティクルの追加および削除](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)」を参照してください。  
  
## <a name="understand-how-to-make-schema-changes-if-application-requirements-change"></a>アプリケーション要件が変更された場合のスキーマの変更方法についての理解  
 アプリケーションの運用後、スキーマの変更が必要になる場合が多々あります。 レプリケーション トポロジでは、多くの場合、このような変更をすべてのサブスクライバーに反映する必要があります。 レプリケーションは、パブリッシュされたオブジェクトに対するさまざまなスキーマ変更をサポートしています。 パブリッシュされた適切なオブジェクトに対して、以下に示すスキーマ変更を [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャーで実行した場合、既定ではすべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サブスクライバーにその変更が反映されます。  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 詳細については、「[パブリケーション データベースでのスキーマの変更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理に関する FAQ](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
  
