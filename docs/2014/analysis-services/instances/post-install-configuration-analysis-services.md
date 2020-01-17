---
title: インストール後の構成 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7f4417b2-0efb-4361-a79e-fa56e43ee054
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a339ee307ed7a10f2ff7d2b1ce51d2e2177ee37
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079654"
---
# <a name="post-install-configuration-analysis-services"></a>インストール後の構成 (Analysis Services)
  Analysis Services のインストール後、サーバーを一般的な用途で使用できるように動作させるためには、追加の構成が必要です。 このセクションでは、インストールを完了するための追加の作業について説明します。 接続要件によっては、認証も構成する必要がある場合があります (「 [Analysis Services への接続](connect-to-analysis-services.md)」を参照)。  
  
 後で、データベースの配置の準備ができたら、追加の作業が必要になります。 つまり、データベースのロール メンバーシップをデータへのユーザー アクセスを許可するように構成し、データベースのバックアップおよび復旧の方法を設計すると共に、データを定期的に更新するためにスケジュールされた処理ワークロードが必要であるかどうかを判断することが求められます。 データベースの配置と管理の詳細については、これらのリンクにあります。[多次元モデル データベース&#40;SSAS&#41; ](../multidimensional-models/multidimensional-model-databases-ssas.md)と[表形式モデル データベース&#40;SSAS 表形式&#41;](../tabular-models/tabular-model-databases-ssas-tabular.md)します。  
  
## <a name="instance-configuration"></a>インスタンスの構成  
 Analysis Services はレプリケート可能なサービスであり、サービスの複数のインスタンスを 1 台のサーバーにインストールできます。 追加の各インスタンスは、SQL Server セットアップを使用して名前付きインスタンスとして個別にインストールされ、用途に合わせて構成されます。 たとえば、開発用サーバーでは、フライト レコーダーを実行したり、実稼働ワークロードをサポートするサーバーでは変更するようなデータ ストレージ用の既定値を使用したりします。 また、他のサービスによって共有されるハードウェアに Analysis Services インスタンスをインストールする場合は、システム構成の調整が必要です。 同じハードウェア上で複数のデータ集中型のアプリケーションをホストする場合、すべてのアプリケーションを通じて使用可能なリソースを最適化するために、メモリしきい値を減少させるサーバー プロパティの構成が必要になることがあります。  
  
## <a name="post-installation-tasks"></a>インストール後の作業  
  
|リンク|タスクの説明|  
|----------|----------------------|  
|[Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](configure-the-windows-firewall-to-allow-analysis-services-access.md)|Analysis Services インスタンスによって使用される TCP ポートを通じて要求がルーティングされるように、Windows ファイアウォールの受信の規則を作成します。 この作業は必須です。 受信のファイアウォール規則を定義するまでは、リモート コンピューターから Analysis Services にアクセスすることはできません。|  
|[サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md)|インストール中に、Analysis Services インスタンスの Administrator ロールに少なくとも 1 つのユーザー アカウントを追加する必要があります。 管理権限は、外部リレーショナル データベースのデータの処理など、多くの日常的なサーバー操作で必要です。 Administrator ロールのメンバーを追加または変更するには、このトピックの情報を参照してください。|  
|[サービス アカウントの構成 (Analysis Services)](configure-service-accounts-analysis-services.md)|インストール時に、Analysis Services サービス アカウントが準備され、適切な権限が割り当てられて、プログラムの実行可能ファイルとデータベース ファイルへの制御されたアクセスが許可されました。 インストール後のタスクとして、追加のタスクを実行するときにサービス アカウントの使用を許可するかどうかを検討してください。 処理とクエリ両方のワークロードを、サービス アカウントで実行できます。 これらの操作は、サービス アカウントが適切な権限を持つ場合にのみ成功します。|  
|[サーバー グループへの Analysis Services インスタンスの登録](register-an-analysis-services-instance-in-a-server-group.md)|SQL Server Management Studio (SSMS) では、SQL Server インスタンスを整理するために、サーバー グループを作成することができます。 複数のサーバー インスタンスから成るスケーラブルな配置は、サーバー グループを使うと管理が簡単になります。 SSMS で Analysis Services のインスタンスをグループにまとめるには、このトピックの情報を参照してください。|  
|[Analysis Services インスタンスのサーバー モードの決定](determine-the-server-mode-of-an-analysis-services-instance.md)|インストール中に、サーバー上で実行されるモデルの種類 (多次元またはテーブル) を決めるサーバー モードを選択します。 サーバー モードが不明な場合は、どちらのモードがインストールされたかを判断するために、このトピックの情報を参照してください。|  
|[Analysis Services インスタンスの名前変更](rename-an-analysis-services-instance.md)|わかりやすい名前を付けると、サーバー モードが異なる複数のインスタンスや、組織の部門やチームに主に使用されるインスタンスを区別するために役立ちます。 インスタンス名をインストールが管理しやすい名前に変更する方法については、このトピックの情報を参照してください。|  
  
## <a name="next-steps"></a>次の手順  
 クライアント ライブラリを使用して Microsoft アプリケーションまたはカスタム アプリケーションから Analysis Services に接続する方法について学習します。 ソリューションの要件によっては、Kerberos 認証用にサービスを構成する必要がある場合もあります。 ドメインの境界を超える必要のある接続では、HTTP アクセスが必要です。 次の手順に関する指示については、「 [Connect to Analysis Services](connect-to-analysis-services.md) 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 のインストール](../../../2014/database-engine/install-windows/installation-for-sql-server.md)   
 [多次元モードおよびデータ マイニング モードでの Analysis Services のインストール](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [表形式モードで Analysis Services をインストールします。](install-windows/install-analysis-services.md)   
 [PowerPivot for SharePoint 2013 のインストール](install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
