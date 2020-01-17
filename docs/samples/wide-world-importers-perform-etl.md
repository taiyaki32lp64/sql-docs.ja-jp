---
title: WideWorldImportersDW - ETL ワークフロー |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f33d36cccbbea6f37139410f9d3d6e03f740ee96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067622"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL ワークフロー
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用して、 *WWI_Integration* WideWorldImporters データベースからデータの変化に応じて WideWorldImportersDW データベースにデータを移行する ETL パッケージ。 パッケージが定期的に実行されます (通常は毎日)。

パッケージは、(Integration Services 内の別の変換) ではなく T-SQL での一括操作を調整する SQL Server Integration Services を使用して高パフォーマンスを保証します。

ディメンションが最初に、読み込まれ、その後ファクト テーブルが読み込まれます。 パッケージは、障害発生後に、いつでも実行できます。

ワークフローのようになります。

 ![WideWorldImporters ETL ワークフロー](media/wide-world-importers/wideworldimporters-etl-workflow.png)

ワークフローは、適切な終了時刻を決定する式タスクを開始します。 終了時刻は、現在の時刻数分からです。 (このアプローチは、現在の時刻に直接データを要求するよりも堅牢です)。時間からのミリ秒が切り捨てられます。

日付のディメンション テーブルを設定することにより、メインの処理を開始します。 処理により、テーブルの現在の年のすべての日付が設定されていること。

次に、一連のデータ フロー タスクは、各ディメンションを読み込みます。 次に、各ファクトを読み込まれるとします。

## <a name="prerequisites"></a>前提条件

- SQL Server 2016 (またはそれ以降) に WideWorldImporters と WideWorldImportersDW データベースを (同じまたは異なる SQL Server インスタンスで)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Integration Services カタログを作成することを確認します。 SQL Server Management Studio オブジェクト エクスプ ローラーで、Integration Services カタログを作成するには、右**Integration Services**、し、**カタログの追加**します。 既定のオプションのままにします。 SQLCLR が有効にして、パスワードを入力を求められます。


## <a name="download"></a>ダウンロード

サンプルの最新リリースでは、次を参照してください。 [wide world importers リリース](https://go.microsoft.com/fwlink/?LinkID=800630)します。 ダウンロード、*毎日 ETL.ispac* Integration Services パッケージ ファイル。

ソース コードをサンプル データベースを再作成をするには、次を参照してください。 [wide world-importers 社](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)します。

## <a name="install"></a>インストール

1. Integration Services パッケージを展開します。
   1. Windows エクスプ ローラーで開き、*毎日 ETL.ispac*パッケージ。 これは、SQL Server Integration Services 配置ウィザードを起動します。
   2. **ソースの選択**を指定するパスとプロジェクトの配置の既定値に従います、*毎日 ETL.ispac*パッケージ。
   3. **先の選択**、Integration Services カタログをホストするサーバーの名前を入力します。
   4. という名前の新しいフォルダーで、たとえば、Integration Services カタログで、パスを選択*WideWorldImporters*します。
   5. 選択**デプロイ**ウィザードを終了します。

2. ETL プロセスの SQL Server エージェント ジョブを作成します。
   1. Management Studio で、右クリックして**SQL Server エージェント**、し、**新規** > **ジョブ**します。
   2. たとえば、名前を入力*WideWorldImporters ETL*します。
   3. 追加、**ジョブ ステップ**型の**SQL Server Integration Services パッケージ**します。
   4. サーバーが、Integration Services カタログを選択し、、*毎日の ETL*パッケージ。
   5. **構成** > **接続マネージャー**ソースとターゲットへの接続が正しく構成されていることを確認します。 既定では、ローカル インスタンスに接続します。
   6. 選択**OK**ジョブを作成します。

3. 実行またはジョブのスケジュールを設定します。
