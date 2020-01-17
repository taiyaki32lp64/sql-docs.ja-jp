---
title: SQL Server ビッグ データ クラスター上の Azure Data Studio で Spark ジョブを送信する
titleSuffix: SQL Server big data clusters
description: '[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上の Azure Data Studio で Spark ジョブを送信します。'
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3c7d346148d7967543e334af07d6f06402d72a0d
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844248"
---
# <a name="submit-spark-jobs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-azure-data-studio"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上の Azure Data Studio で Spark ジョブを送信する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

ビッグ データ クラスターの主なシナリオの 1 つに、SQL Server 用の Spark ジョブを送信する機能があります。 Spark ジョブ送信機能を使用すると、SQL Server 2019 ビッグ データ クラスターへの参照を含むローカル Jar ファイルまたは Py ファイルを送信できます。 また、HDFS ファイル システムに既に配置されている Jar ファイルまたは Py ファイルを実行することもできます。 

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 ビッグ データ ツール](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
   - **kubectl**

- [Azure Data Studio をビッグ データ クラスターの HDFS/Spark ゲートウェイに接続します](connect-to-big-data-cluster.md)。

## <a name="open-spark-job-submission-dialog"></a>Spark ジョブの送信ダイアログを開く

Spark ジョブの送信ダイアログを開くには、いくつかの方法があります。 ダッシュボード、オブジェクト エクスプローラーのコンテキスト メニュー、コマンド パレットなどの方法があります。

- Spark ジョブの送信ダイアログを開くには、ダッシュボードで **[New Spark Job]\(新しい Spark ジョブ\)** をクリックします。

    ![ダッシュボードをクリックした [Submit]\(送信\) メニュー](./media/submit-spark-job/new-spark-job.png)

- または、オブジェクト エクスプローラーでクラスターを右クリックし、コンテキスト メニューから **[Submit Spark Job]\(Spark ジョブの送信\)** を選択します。

    ![ファイルを右クリックした [Submit]\(送信\) メニュー](./media/submit-spark-job/submit-spark-job-1.png)


- Jar/Py フィールドが事前に設定された状態で Spark ジョブの送信ダイアログを開くには、オブジェクト エクスプローラーで Jar/Py ファイルを右クリックし、コンテキスト メニューから **[Submit Spark Job]\(Spark ジョブの送信\)** を選択します。  

    ![クラスターを右クリックした [Submit]\(送信\) メニュー](./media/submit-spark-job/submit-spark-job.png)

- コマンド パレットから **[Submit Spark Job]\(Spark ジョブの送信\)** を使用するには、**Ctrl + Shift + P** キー (Windows の場合 ) と **Cmd + Shift + P** キー (Mac の場合) を入力します。

    ![Windows の [Submit]\(送信\) メニュー コマンド パレット](./media/submit-spark-job/submit-spark-job-3.png)

    ![Mac の [Submit]\(送信\) メニュー コマンド パレット](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Spark ジョブを送信する 

Spark ジョブの送信ダイアログは、次のように表示されます。 ジョブ名、JAR/Py ファイル パス、メイン クラス、およびその他のフィールドを入力します。 Jar/Py ファイル ソースは、ローカルまたは HDFS のものである可能性があります。 Spark ジョブに参照 Jar、Py ファイル、または追加ファイルがある場合は、 **[ADVANCED]\(詳細設定\)** タブをクリックし、対応するファイル パスを入力します。 **[Submit]\(送信\)** をクリックして Spark ジョブを送信します。

![新しい Spark ジョブ ダイアログ](./media/submit-spark-job/submit-spark-job-section.png)

![[Advanced]\(詳細設定\) ダイアログ](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Spark ジョブの送信を監視する

Spark ジョブが送信されると、Spark ジョブの送信と実行状態の情報が、左側の [Task History]\(タスク履歴\) に表示されます。 進行状況とログの詳細も、 **[OUTPUT]\(出力\)** ウィンドウの下部に表示されます。

- Spark ジョブが進行中の場合、進行状況に合わせて **[Task History]\(タスク履歴\)** パネルと **[OUTPUT]\(出力\)** ウィンドウが更新されます。

    ![進行中の Spark ジョブを監視する](./media/submit-spark-job/monitor-spark-job-submission.png)

- Spark ジョブが正常に完了すると、 **[OUTPUT]\(出力\)** ウィンドウに Spark UI と Yarn UI のリンクが表示されます。 詳細については、リンクをクリックしてください。

    ![出力の Spark ジョブ リンク](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>次の手順

SQL Server ビッグ データ クラスターと関連するシナリオの詳細については、「[SQL Server ビッグ データ クラスターとは](big-data-cluster-overview.md)」を参照してください。