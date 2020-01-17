---
title: ログ配布について (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary servers [SQL Server]
- log shipping [SQL Server], jobs
- copy jobs [SQL Server]
- primary databases [SQL Server]
- log shipping [SQL Server], monitoring
- log shipping [SQL Server], about log shipping
- alert jobs [SQL Server]
- availability [SQL Server]
- jobs [SQL Server], log shipping
- monitor servers [SQL Server]
- restore jobs [SQL Server]
- log shipping [SQL Server]
- backup jobs [SQL Server]
- primary servers [SQL Server]
ms.assetid: 55da6b94-3a4b-4bae-850f-4bf7f6e918ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a66125c6e241c75d473fa170d3de5ef9755b28e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774554"
---
# <a name="about-log-shipping-sql-server"></a>ログ配布について (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログ配布を使用すると、トランザクション ログ バックアップを、 *プライマリ サーバー* インスタンスの *プライマリ データベース* から、別の *セカンダリ サーバー* インスタンスの 1 つ以上の *セカンダリ データベース* に自動的に送信できます。 トランザクション ログ バックアップはセカンダリ データベースごとに個別に適用されます。 オプションで用意する 3 台目のサーバー インスタンス ( *監視サーバー*) では、バックアップ操作と復元操作の履歴と状態が記録されます。また、これらの操作がスケジュールどおりに実行されなかった場合に警告を通知することもできます。  
  
 **このトピックの内容**  
  
-   [利点](#Benefits)  
  
-   [用語と定義](#TermsAndDefinitions)  
  
-   [ログ配布の概要](#ComponentsAndConcepts)  
  
-   [相互運用性](#Interoperability)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="Benefits"></a> 利点  
  
-   1 つのプライマリ データベースと 1 つ以上のセカンダリ データベース (それぞれが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の個別のインスタンスに存在) で構成される災害復旧ソリューションを提供します。  
  
-   復元ジョブの間のセカンダリ データベースへの制限付きの読み取り専用アクセスをサポートします。  
  
-   プライマリ サーバーでプライマリ データベースのログをバックアップする時点と、セカンダリ サーバーがそのログ バックアップを復元 (適用) する時点との間に生じる遅延時間をユーザーが指定できます。 たとえば、プライマリ データベースでデータが誤って変更された場合などに、長い遅延が役立ちます。 誤った変更にすぐに気付いた場合、遅延があれば、変更が反映される前に、セカンダリ データベースにあるまだ変更されていないデータを取得できます。  
  
##  <a name="TermsAndDefinitions"></a> 用語と定義  
 プライマリ データベース  
 実稼働サーバーである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス。  
  
 プライマリ サーバー  
 別のサーバーにバックアップするプライマリ サーバーのデータベース。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用したログ配布構成の管理は、すべてプライマリ データベースから実行されます。  
  
 セカンダリ データベース  
 プライマリ データベースのウォーム スタンバイ コピーを保持しておく [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス。  
  
 セカンダリ データベース (secondary database)  
 プライマリ データベースのウォーム スタンバイ コピー。 セカンダリ データベースは、RECOVERING と STANDBY のどちらかの状態にすることができます。この状態では、データベースを制限付きの読み取り専用アクセスで使用できます。  
  
 監視サーバー  
 ログ配布に関する次の詳細情報をすべて追跡する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のオプションのインスタンス。  
  
-   プライマリ データベースのトランザクション ログが最後にバックアップされた日時  
  
-   セカンダリ サーバーでバックアップ ファイルが最後にコピーおよび復元された日時  
  
-   バックアップ障害の警告に関する情報  
  
> [!IMPORTANT]  
>  監視サーバーは、一度構成すると、最初にログ配布を削除しない限り変更できません。  
  
 バックアップ ジョブ (backup job)  
 バックアップ操作の実行、ローカル サーバーと監視サーバーへの履歴ログの記録、および古いバックアップ ファイルと履歴情報の削除を行う [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ。 ジョブ カテゴリの "ログ配布のバックアップ" は、ログ配布を有効にしたときにプライマリ サーバー インスタンスで作成されます。  
  
 コピー ジョブ (copy job)  
 プライマリ サーバーからセカンダリ サーバーの構成可能なコピー先にバックアップ ファイルをコピーし、セカンダリ サーバーと監視サーバーの履歴ログを記録する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ。 ジョブ カテゴリの "ログ配布のコピー" は、データベースでログ配布を有効にしたときに各セカンダリ サーバーのログ配布構成で作成されます。  
  
 復元ジョブ (restore job)  
 コピーされたバックアップ ファイルをセカンダリ データベースに復元する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ。 この操作により、ローカル サーバーと監視サーバーの履歴ログが記録され、古いファイルと履歴情報が削除されます。 ジョブ カテゴリの "ログ配布のログ復元" は、データベースでログ配布を有効にしたときにセカンダリ サーバー インスタンスで作成されます。  
  
 警告ジョブ (alert job)  
 バックアップと復元操作が指定したしきい値の範囲内で完了しない場合に、プライマリ データベースとセカンダリ データベースに対する警告を通知する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ。 ジョブ カテゴリの "ログ配布の警告" は、データベースでログ配布を有効にしたときに監視サーバー インスタンスで作成されます。  
  
> [!TIP]  
>  警告 1 件につき警告番号を指定する必要があります。 また、警告が発生するとオペレーターに通知されるよう警告を構成してください。  
  
##  <a name="ComponentsAndConcepts"></a> ログ配布の概要  
 ログ配布は、次に示す 3 つの操作から構成されます。  
  
1.  プライマリ サーバー インスタンスでトランザクション ログをバックアップする。  
  
2.  セカンダリ サーバー インスタンスにトランザクション ログ ファイルをコピーする。  
  
3.  セカンダリ サーバー インスタンスでログ バックアップを復元する。  
  
 ログは、複数のセカンダリ サーバー インスタンスに配布できます。 その場合、操作 2. と操作 3. が各セカンダリ サーバー インスタンスに対して繰り返し実行されます。  
  
 ログ配布構成は、自動的にはプライマリ サーバーからセカンダリ サーバーにフェールオーバーされません。 プライマリ データベースが使用できなくなった場合は、任意のセカンダリ データベースを手動でオンラインにできます。  
  
 セカンダリ データベースをレポート作成に使用できます。  
  
 さらに、ログ配布構成の警告を構成できます。  
  
### <a name="a-typical-log-shipping-configuration"></a>通常のログ配布構成  
 次の図に、プライマリ サーバー インスタンス、3 台のセカンダリ サーバー インスタンス、および監視サーバー インスタンスを使用するログ配布構成を示します。 この図に示されているバックアップ ジョブ、コピー ジョブ、および復元ジョブの実行手順は、次のようになります。  
  
1.  プライマリ サーバー インスタンスがバックアップ ジョブを実行し、プライマリ データベースのトランザクション ログをバックアップします。 このサーバー インスタンスは、次にログ バックアップをプライマリ ログ バックアップ ファイルに配置し、バックアップ フォルダーに送信します。  この図では、バックアップ フォルダーは共有ディレクトリ ("*バックアップ共有*") にあります。  
  
2.  3 台のセカンダリ サーバー インスタンスは、それぞれのコピー ジョブを実行し、プライマリ ログ バックアップ ファイルをローカルのコピー先フォルダーにコピーします。  
  
3.  各セカンダリ サーバー インスタンスは、それぞれの復元ジョブを実行し、ログ バックアップをローカルのコピー先フォルダーからローカル セカンダリ データベースに復元します。  
  
 プライマリ サーバー インスタンスおよびセカンダリ サーバー インスタンスは、それぞれの履歴および状態を監視サーバー インスタンスに送信します。  
  
 ![バックアップ ジョブ、コピー ジョブ、復元ジョブを示す構成](../media/ls-typical-configuration.gif "バックアップ ジョブ、コピー ジョブ、復元ジョブを示す構成")  
  
##  <a name="Interoperability"></a> 相互運用性  
 ログ配布は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の次の機能またはコンポーネントと共に使用できます。  
  
-   [AlwaysOn 可用性グループへのログ配布を移行する前提条件&#40;SQL Server&#41;](../availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
-   [データベース ミラーリングとログ配布 &#40;SQL Server&#41;](../database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [ログ配布とレプリケーション &#40;SQL Server&#41;](log-shipping-and-replication-sql-server.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] とデータベース ミラーリングは、相互に排他的です。 これらの機能のいずれかに対して構成されたデータベースを他の機能用に構成することはできません。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [SQL Server 2014 へのログ配布のアップグレード&#40;TRANSACT-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [ログ配布の構成 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [ログ配布構成へのセカンダリ データベースの追加 &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [ログ配布構成からのセカンダリ データベースの削除 &#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [ログ配布の削除 &#40;SQL Server&#41;](remove-log-shipping-sql-server.md)  
  
-   [ログ配布レポートの表示 &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [ログ配布の監視 &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [役割の交代後のログインとジョブの管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](../availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
