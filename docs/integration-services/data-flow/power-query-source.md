---
title: Power Query ソース | Microsoft Docs
description: SQL Server Integration Services データ フロー内の Power Query ソースを構成する方法について説明します
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.powerqueryconnmgr.f1
- sql13.ssis.designer.powerquerysource.queries.f1
- sql13.ssis.designer.powerquerysource.connmgrs.f1
- sql14.ssis.designer.powerqueryconnmgr.f1
- sql14.ssis.designer.powerquerysource.queries.f1
- sql14.ssis.designer.powerquerysource.connmgrs.f1
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: efefe16b7c5180ed0ae0dd853737c2182f335f61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034398"
---
# <a name="power-query-source-preview"></a>Power Query ソース (プレビュー)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



この記事では、SQL Server Integration Services (SSIS) データ フロー内の Power Query ソースのプロパティを構成する方法について説明します。 Power Query は、Excel/Power BI Desktop を使用したさまざまなデータ ソースへの接続とデータの変換を可能にするテクノロジです。 詳細については、「[Power Query - 概要と学習](https://support.office.com/article/power-query-overview-and-learning-ed614c81-4b00-4291-bd3a-55d80767f81d)」の記事を参照してください。 Power Query によって生成されたスクリプトをコピーし、SSIS データ フローの Power Query ソースに貼り付けて構成することができます。
  
> [!NOTE]
> 現在のプレビュー リリースでは、フィードバックを迅速に収集して機能強化の頻度を上げるために、Power Query ソースは、Azure Data Factory (ADF) の SQL Server Data Tools (SSDT) と Azure-SSIS Integration Runtime (IR) でのみ使用できます。 Power Query ソースをサポートする最新の SSDT は、[こちら](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017)からダウンロードできます。 Azure-SSIS IR をプロビジョニングするには、[ADF での SSIS のプロビジョニング](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)に関する記事を参照してください。

## <a name="configure-the-power-query-source"></a>Power Query ソースを構成する

SSDT で **Power Query ソース エディター**を開くには、SSIS Toolbox から **Power Query ソース**をデータ フロー デザイナーにドラッグ アンド ドロップした後、それをダブルクリックします。  

![PQ ソース](media/power-query-source/pq-source.png)

左側に 3 つのタブが表示されます。 **[クエリ]** タブでは、ドロップダウン メニューからクエリ モードを選択できます。
-   **[単一クエリ]** モードでは、Excel/Power BI Desktop から 1 つの Power Query スクリプトをコピーして貼り付けることができます。
-   **[変数からの単一クエリ]** モードでは、実行されるクエリを含む文字列変数を指定できます。

![PQ ソースの [クエリ] タブ (単一)](media/power-query-source/pq-source-queries-tab-single.png)

**[接続マネージャー]** タブでは、データソースへのアクセス資格情報を含む Power Query 接続マネージャーを追加または削除できます。 **[データ ソースの検出]** ボタンを選択すると、クエリで参照されているデータ ソースが識別され、一覧表示されます。この一覧を利用して、適切な既存の Power Query 接続マネージャーを割り当てるか、新しいものを作成します。

![PQ Sourceソースの [接続マネージャー] タブ (検出)](media/power-query-source/pq-source-connection-managers-tab-detect.png)

![PQ ソースの [接続マネージャー] タブ (追加)](media/power-query-source/pq-source-connection-managers-tab-add.png)

最後に、 **[列]** タブでは、出力列の情報を編集できます。

![PQ ソースの [列] タブ](media/power-query-source/pq-source-columns-tab.png)

## <a name="configure-the-power-query-connection-manager"></a>Power Query 接続マネージャーを構成する

SSDT で Power Query ソースを含むデータ フローを設計するときに、新しい Power Query 接続マネージャーを次の方法で作成できます。
- 前述のように、Power Query ソースの **[接続マネージャー]** タブで、 **[追加]** / **[データ ソースの検出]** ボタンを選択し、ドロップダウン メニューから **<New connection...>** を選択することで、間接的に作成する。
- パッケージの **[接続マネージャー]** パネルを右クリックし、ドロップダウン メニューから **[新しい接続...]** を選択することで、直接作成する。

![PQ ソースの [接続マネージャー] パネル (追加)](media/power-query-source/pq-source-connection-managers-panel-add.png)

**[SSIS 接続マネージャーの追加]** ダイアログで、[接続マネージャーの種類] の一覧の **[PowerQuery]** をダブルクリックします。

![PQ ソースの [接続マネージャー] パネル ([追加] ダイアログ)](media/power-query-source/pq-source-connection-managers-panel-add-dialog.png)

**Power Query 接続マネージャー エディター**で、 **[データソースの種類]** 、 **[データ ソースのパス]** 、および **[認証の種類]** を指定し、適切なアクセス資格情報を割り当てます。 **[データ ソースの種類]** では、現時点では 22 種類のドロップダウン メニューから選択できます。

![PQ ソース接続マネージャー エディター (種類)](media/power-query-source/pq-source-connection-manager-editor-kind.png)

一部のソース (**Oracle**、**DB2**、**MySQL**、**PostgreSQL**、**Teradata**、**Sybase**) では、[Power Query の前提条件](https://support.office.com/article/data-source-prerequisites-power-query-6062cf52-c764-45d0-a1c6-fbf8fc05b05a)に関する記事から取得できる ADO.NET ドライバーを追加でインストールする必要があります。 カスタム セットアップ インターフェイスを使用して Azure-SSIS IR にインストールできます。[Azure-SSIS IR のカスタマイズ](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)に関する記事を参照してください。

**[データ ソース パス]** では、接続文字列を形成するデータ ソース固有のプロパティを認証情報なしで入力できます。 たとえば、**SQL** データ ソースのパスは、`<Server>;<Database>` 形式になります。 **[編集]** ボタンを選択して、パスを形成するデータ ソース固有のプロパティに値を割り当てることできます。

![PQ ソース接続マネージャー エディター (パス)](media/power-query-source/pq-source-connection-manager-editor-path.png)

最後に、 **[認証の種類]** では、ドロップダウン メニューから **[匿名]** / **[Windows 認証]** / **[ユーザー名とパスワード]** / **[キー]** のいずれかを選択し、適切なアクセス資格情報を入力し、 **[テスト接続]** ボタンを選択して Power Query ソースが適切に構成されていることを確認します。

![PQ ソース接続マネージャー エディター (認証)](media/power-query-source/pq-source-connection-manager-editor-authentication.png)

### <a name="current-limitations"></a>現在の制限

-   **Oracle** データ ソースは現時点では使用できません。Azure-SSIS IR に Oracle ADO.NET ドライバーはインストールできないため、代わりに Oracle ODBC ドライバーをインストールし、当面は **ODBC** データ ソースを使用して Oracle に接続してください。[Azure-SSIS IR のカスタマイズ](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)に関する記事の **ORACLE STANDARD ODBC** の例を参照してください。

-   **Web** データ ソースは、現時点ではカスタム セットアップのある Azure-SSIS IR 上では使用できないため、現在のところはカスタム設定のない Azure-SSIS IR 上で使用してください。

## <a name="next-steps"></a>次の手順
Azure-SSIS IR で、ADF パイプラインのファーストクラスのアクティビティとして SSIS パッケージを実行する方法を確認します。 [SSIS パッケージのアクティビティ ランタイムの実行](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)に関する記事を参照してください。
