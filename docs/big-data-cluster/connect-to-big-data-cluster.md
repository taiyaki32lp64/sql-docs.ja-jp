---
title: マスターおよび HDFS ビッグ データ クラスターに接続する
description: SQL Server ビッグ データ クラスターの SQL Server マスター インスタンスと HDFS/Spark ゲートウェイに接続する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0c5ba08a492be621e4b1f8871bdfcb49983af26d
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882392"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、Azure Data Studio から [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]に接続する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

- 展開済みの [SQL Server 2019 ビッグ データ クラスター](deployment-guidance.md)。
- [SQL Server 2019 ビッグ データ ツール](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
   - **kubectl**
   - **azdata**

## <a id="master"></a> クラスターに接続する

Azure Data Studio を使用してビッグ データ クラスターに接続するには、クラスター内の SQL Server マスター インスタンスへの新しい接続を作成します。 次にその方法を示します。

1. SQL Server マスター インスタンス エンドポイントを探します。

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > エンドポイントを取得する方法の詳細については、「[エンドポイントを取得する](deployment-guidance.md#endpoints)」を参照してください。

1. Azure Data Studio で、**F1 キー** >  **[新しい接続]** から新しい接続を作成します。

1. **[接続の種類]** で **[Microsoft SQL Server]** を選択します。

1. SQL Server マスター インスタンスに対して見つかったエンドポイント名を **[サーバー名]** テキスト ボックスに入力します (例: **\<IP_Address\>,31433**)。 

1. 認証の種類を選択します。 ビッグ データ クラスターで実行されている SQL Server マスター インスタンスの場合は、**Windows 認証**と **SQL ログイン**のみがサポートされます。 

1. SQL ログインを使用している場合、SQL ログインの **[ユーザー名]** と **[パスワード]** を入力します。

   > [!TIP]
   > 既定では、ユーザー名 **SA** は、ビッグ データ クラスターの展開の間に無効になります。 新しい sysadmin ユーザーは、展開前または展開時に設定される、**AZDATA_USERNAME** 環境変数に対応する名前と **AZDATA_PASSWORD** 環境変数に対応するパスワードを使用して、展開中にプロビジョニングされます。

1. ターゲットの **[データベース名]** を、使用しているリレーショナル データベースのいずれかに変更します。

   ![マスター インスタンスに接続する](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. **[接続]** をクリックすると、**サーバー ダッシュボード**が表示されます。

Azure Data Studio の 2019 年 2 月リリースでは、SQL Server マスター インスタンスに接続することで、HDFS/Spark ゲートウェイを操作することもできます。 これは、次のセクションで説明する HDFS および Spark 用に別の接続を使用する必要がないことを意味します。

- オブジェクト エクスプローラーに、新しいノートブックの作成や Spark ジョブの送信などのビッグ データ クラスター タスクの右クリック サポートを備えた、新しい **[Data Services]** ノードが追加されました。 
- **[Data Services]** ノードには **HDFS** フォルダーも含まれていて、HDFS のコンテンツを調べ、HDFS に関連する共通タスク (外部テーブルの作成やノートブックを開いて HDFS のコンテンツを分析するなど) を実行できます。
- 接続の**サーバー ダッシュボード**には、拡張機能がインストールされている場合、**SQL Server ビッグ データ クラスター**と **SQL Server 2019** のタブも含まれています。

   ![Azure Data Studio の [Data Services] ノード](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)」を参照してください。
