---
title: トラブルシューティング
description: 既知の問題に対処するための出発点を示します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c9be3a8dff314f6645029fb54803ad30dc04db27
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727569"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>SQL Server での機械学習のトラブルシューティング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事は、既知の問題に対処するための出発点として使用してください。

## <a name="known-issues"></a>既知の問題

次の記事では、現在および以前のリリースに関する既知の問題について説明します。

+ [R Services の既知の問題](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 リリース ノート](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 リリース ノート](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>システム情報を収集する方法

エラーが発生した場合、または環境内の問題を理解する必要がある場合は、関連する情報を体系的に収集することが重要です。 次の記事では、セルフヘルプのトラブルシューティングまたはテクニカル サポートの依頼に役立つ情報の一覧を示します。

+ [機械学習のトラブルシューティングのためのデータ収集](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>セットアップと構成に関するガイド

SQL Server で機械学習を設定していない場合、または機能を追加する場合は、ここから開始します。

+ [SQL Server Machine Learning サービス (データベース内) のインストール](install/sql-machine-learning-services-windows-install.md)
+ [SQL Server Machine Learning Server (スタンドアロン) のインストール](install/sql-machine-learning-standalone-windows-install.md)
+ [コマンド プロンプトのセットアップ](install/sql-ml-component-commandline-install.md)
+ [オフラインのセットアップ (インターネットなし)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>構成

次の記事には、既定値と、インスタンスの機械学習の構成をカスタマイズする方法に関する情報が含まれています。

+ [SQL Server Machine Learning Services での外部スクリプトの同時実行のスケーリング](administration/modify-user-account-pool.md)   
+ [高度な分析拡張機能の構成および管理](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [リソース プールを作成する方法](r/how-to-create-a-resource-pool-for-r.md)
+ [R ワークロードの最適化](r/operationalizing-your-r-code.md)
