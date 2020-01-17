---
title: メンテナンス プラン | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- SQL12.AG.MAINTPLAN.LEGACY.F1
helpviewer_keywords:
- maintenance plans [SQL Server], about database maintenance plans
- maintenance plans [SQL Server], database compatibility level displayed in designer
- maintenance plans [SQL Server]
ms.assetid: 5982ca65-74fe-44e3-aef9-00a65a0db169
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0643c6fbf8e9a6aa649d4d335117bcb4f5b35208
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206853"
---
# <a name="maintenance-plans"></a>メンテナンス プラン
  メンテナンス プランでは、データベースを最適化したり、データベースを定期的にバックアップしたり、データベースの不整合をなくしたりするために必要なタスクのワークフローを作成します。 メンテナンス プラン ウィザードでも主要なメンテナンス プランを作成できますが、プランを手動で作成するとより柔軟性が高くなります。  
  
## <a name="benefits-of-maintenance-plans"></a>メンテナンス プランの利点  
 [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)]では、メンテナンス プランによって、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エージェント ジョブが実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パッケージが作成されます。 メンテナンス プランは、手動で実行することも、定期的に自動実行することもできます。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] メンテナンス プランには、次の機能が用意されています。  
  
-   さまざまな一般的なメンテナンス タスクを使用するワークフローの作成。 カスタム [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを独自に作成することもできます。  
  
-   概念的な階層。 各プランでは、ワークフローの作成や編集を行えます。 各プランのタスクはサブプランにグループ化できます。サブプランは、異なるタイミングで実行されるようにスケジュールを設定できます。  
  
-   マスター サーバーやターゲット サーバーの環境で使用できるマルチサーバーのプランのサポート。  
  
-   プランの履歴をリモート サーバーのログに記録する際のサポート。  
  
-   Windows 認証と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のサポート。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="maintenace-plan-functionality"></a>メンテナンス プラン機能  
 メンテナンス プランは、次のタスクを実行するように作成できます。  
  
-   新しい FILL FACTOR を使用してインデックスを再構築し、データ ページとインデックス ページのデータを再編成します。 この再構築によって、データ量と空き領域がすべてのデータベース ページに均等に分配されます。 また、その後の拡張を高速化できます。 詳細については、「[インデックスの FILL FACTOR の指定](../indexes/specify-fill-factor-for-an-index.md)」を参照してください。  
  
-   空のデータベース ページを削除してデータ ファイルを圧縮します。  
  
-   インデックス統計を更新して、クエリ オプティマイザーで保持されているテーブル内のデータ値の分布に関する情報を常に最新の状態に保ちます。 その結果、データベース内のデータに関してクエリ オプティマイザーが使用できる情報が多くなるため、データにアクセスする最適な方法がクエリ オプティマイザーによってより適切に判断されます。 インデックス統計は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって定期的に自動更新されますが、このオプションを使用すると、インデックス統計をすぐに更新できます。  
  
-   データベース内のデータとデータ ページの内部一貫性チェックを実行して、システムまたはソフトウェアの問題が原因でデータが壊れていないかどうかを確認します。  
  
-   データベースとトランザクション ログ ファイルをバックアップします。 データベースとログのバックアップは、指定した期間、保管できます。 これにより、バックアップの履歴を作成して、最後にデータベースをバックアップした時点より前の時点への復元が必要になった場合に使用できます。 また、差分バックアップも行えます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行します。 これにより、さまざまなアクションを実行するジョブと、それらのジョブを実行するメンテナンス プランを作成できます。  
  
 メンテナンス タスクで生成される結果は、レポートとしてテキスト ファイルに書き込むことや、`sysmaintplan_log` 内のメンテナンス プラン用のテーブルである `sysmaintplan_logdetail` や `msdb` に書き込むことができます。 ログ ファイル ビューアーで結果を参照するには、 **[メンテナンス プラン]** を右クリックし、 **[履歴の表示]** をクリックします。  
  
## <a name="related-tasks"></a>Related Tasks  
 メンテナンス プランの基礎知識については、次の各トピックを参照してください。  
  
|||  
|-|-|  
|**[説明]**|**トピック**|  
|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用してメンテナンス プランを作成する方法について説明します。|[メンテナンス プランの作成](create-a-maintenance-plan.md)|  
|メンテナンス プラン デザイン画面を使用してメンテナンス プランを作成する方法について説明します。|[メンテナンス プランの作成 &#40;メンテナンス プラン デザイン画面&#41;](create-a-maintenance-plan-maintenance-plan-design-surface.md)|  
|オブジェクト エクスプローラーで利用できるメンテナンス プランの機能について説明します。|[[メンテナンス プラン] ノード &#40;オブジェクト エクスプローラー&#41;](../../ssms/object/object-explorer.md)|  
  
  
