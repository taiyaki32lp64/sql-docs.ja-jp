---
title: SSMS を利用して Azure で SSIS パッケージのスケジュールを設定する | Microsoft Docs
description: SQL Server Management Studio (SSMS) の Schedule コマンドを利用し、Azure SQL Database にデプロイされた SSIS パッケージのスケジュールを設定する方法について説明します。
ms.date: 09/23/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: c553e650dcbcfabc8ad2d18ce490221c0d2439ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054604"
---
# <a name="schedule-the-execution-of-ssis-packages-deployed-in-azure-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) を利用し、Azure でデプロイされた SSIS パッケージの実行スケジュールを設定します

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server Management Studio (SSMS) を使用して、Azure SQL Database にデプロイされた SSIS パッケージのスケジュールを設定することができます。 オンプレミス SQL Server と SQL Database Managed Instance にはファースト クラス SSIS ジョブ スケジューラーとしてそれぞれ、SQL Server エージェントと Managed Instance Agent があります。 一方、SQL Database には、ファースト クラス SSIS ジョブ スケジューラーが組み込まれていません。 この記事で説明する SSMS 機能は SQL Server エージェントに似た、おなじみのインターフェイスを備えており、SQL Database にデプロイされているパッケージをそのインターフェイスでスケジュール設定できます。

SQL Database を使用して SSIS カタログ (`SSISDB`) をホストする場合、この SSMS 機能を使用し、SSIS パッケージのスケジュール設定に必要な Data Factory のパイプライン、アクティビティ、トリガーを生成できます。 その後、Data Factory でそれらのオブジェクトを任意で編集したり、拡張したりできます。

SSMS を使用してパッケージのスケジュールを設定するとき、SSIS では 3 つのデータ ファクトリ オブジェクトが自動的に新しく作成されます。その名前は、選択したパッケージの名前とタイムスタンプに基づきます。 たとえ゛は、SSIS パッケージの名前が **MyPackage** であれば、SSMS によって、次のようなデータ ファクトリ オブジェクトが新しく作成されます。

| Object | [オブジェクト名] |
|---|---|
| パイプライン | **Pipeline_MyPackage_2018-05-08T09_00_00Z** |
| SSIS パッケージ アクティビティの実行 | **Activity_MyPackage_2018-05-08T09_00_00Z** |
| トリガー | **Trigger_MyPackage_2018-05-08T09_00_00Z** |
|||

## <a name="prerequisites"></a>Prerequisites

この記事で説明する機能には、SQL Server Management Studio バージョン 17.7 以降が必要になります。 最新バージョンの SSMS を入手するには、「[SQL Server Management Studio (SSMS) のダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。

## <a name="schedule-a-package-in-ssms"></a>SSMS でパッケージのスケジュールを設定する

1. SSMS のオブジェクト エクスプローラーで、SSISDB データベースを選択し、フォルダーを選択し、プロジェクトを選択し、パッケージを選択します。 パッケージを右クリックし、 **[スケジュール]** を選択します。

    ![スケジュールを設定するパッケージを選択します。](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image1-schedule.png)

2. **[新しいスケジュール]** ダイアログ ボックスが開きます。 **[新しいスケジュール]** ダイアログ ボックスの **[全般]** ページで、新しくスケジュールを設定したジョブの名前と説明を入力します。

    ![[新しいスケジュール] ダイアログ ボックスの [全般] ページ](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image2-new-schedule.png)

3. **[新しいスケジュール]** ダイアログ ボックスの **[パッケージ]** ページで、オプションの実行時設定と実行時環境を選択します。

    ![[新しいスケジュール] ダイアログ ボックスの [パッケージ] ページ](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image3-new-schedule2.png)

4. **[新しいスケジュール]** ダイアログ ボックスの **[スケジュール]** ページで、頻度、時刻、継続時間など、スケジュール設定を指定します。

    ![[新しいスケジュール] ダイアログ ボックスの [スケジュール] ページ](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image4-new-schedule3.png)

5. **[新しいスケジュール]** ダイアログ ボックスでジョブの作成が終わると確認が表示され、SSMS によってこれから作成される新しいデータ ファクトリ オブジェクトについて通知されます。 確認ダイアログ ボックスで **[はい]** を選択すると、Azure Portal で新しいデータ ファクトリ パイプラインが開きます。ここでレビューやカスタマイズができます。

    ![新しいスケジュールの確認](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image5-confirmation.png)

6. スケジュールのトリガーをカスタマイズするには、 **[トリガー]** メニューから **[New/Edit]\(新規/編集\)** を選択します。

    ![新しいパイプラインを任意で編集する](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image6-edit.png)

    **[トリガーの編集]** ブレードが開きます。ここでスケジュール オプションをカスタマイズできます。

    ![トリガーの編集](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image7-edit2.png)

## <a name="next-steps"></a>次の手順

SSIS パッケージのスケジュールを設定するその他の方法については、「[Azure で SSIS パッケージの実行をスケジュールする](ssis-azure-schedule-packages.md)」を参照してください。

Azure Data Factory のパイプライン、アクティビティ、トリガーの詳細については、次の記事をご覧ください。
-   [Azure Data Factory のパイプラインとアクティビティ](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities)
-   [Azure Data Factory のパイプラインの実行とトリガー](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers)
