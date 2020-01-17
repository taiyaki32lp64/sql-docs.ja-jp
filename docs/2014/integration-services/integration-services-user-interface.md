---
title: Integration Services のユーザー インターフェイス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55b09057927fa9c5102b8d816c42e1741bc0883a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767674"
---
# <a name="integration-services-user-interface"></a>Integration Services のユーザー インターフェイス
  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーのタブ上にあるデザイン画面以外にも、パッケージに機能を追加したり、パッケージ オブジェクトのプロパティを構成するための、次に示すようなウィンドウやダイアログ ボックスが用意されています。  
  
-   ログ記録や構成などの機能をパッケージに追加するために使用する、ダイアログ ボックスおよびウィンドウ。  
  
-   パッケージ オブジェクトのプロパティを構成するためのカスタム エディター。 ほとんどすべての種類のコンテナー、タスク、およびデータ フロー コンポーネントには、独自のカスタム エディターがあります。  
  
-   **[詳細エディター]** ダイアログ ボックス。多くのデータ フロー コンポーネントに対して詳細な構成オプションを提供する、汎用エディターです。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、環境の構成やパッケージの処理に使用するウィンドウおよびダイアログ ボックスも用意されています。  
  
## <a name="dialog-boxes-and-windows"></a>ダイアログ ボックスおよびウィンドウ  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでパッケージを開いたり、新しいパッケージを作成する場合、次のダイアログ ボックスおよびウィンドウが使用できます。  
  
 次の表は、 **[SSIS]** メニューと [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーのデザイン画面から使用できるダイアログ ボックスの一覧です。  
  
|ダイアログ ボックス|目的|アクセス|  
|----------------|-------------|------------|  
|**作業の開始**|サンプル、チュートリアル、およびビデオにアクセスします。|**[制御フロー]** タブまたは **[データ フロー]** タブのデザイン画面で右クリックし、 **[作業の開始]** をクリックします。<br /><br /> 新しい **プロジェクトを作成するときに** [作業の開始] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ウィンドウが自動的に表示されるようにするには、ウィンドウの下部にある **[新しいプロジェクトで常に表示する]** を選択します。|  
|**[SSIS ログの構成]**|ログを追加してログ記録の詳細を設定することにより、パッケージとそのタスクのログ記録を構成します。|次に、 **[SSIS]** メニューの **[ログ記録]** をクリックします。<br /><br /> \- または -<br /><br /> **[制御フロー]** タブのデザイン画面で任意の場所を右クリックし、 **[ログ記録]** をクリックします。|  
|**[パッケージ構成オーガナイザー]**|パッケージの構成を追加して編集します。 パッケージ構成ウィザードは、このダイアログ ボックスから実行します。|**[SSIS]** メニューの **[パッケージ構成]** をクリックします。<br /><br /> \- または -<br /><br /> **[制御フロー]** タブのデザイン画面で任意の場所を右クリックし、 **[パッケージ構成]** をクリックします。|  
|**[デジタル署名]**|パッケージに署名したり、またはパッケージから署名を削除します。|**[SSIS]** メニューの **[デジタル署名]** をクリックします。<br /><br /> \- または -<br /><br /> **[制御フロー]** タブのデザイン画面で任意の場所を右クリックし、 **[デジタル署名]** をクリックします。|  
|**[ブレークポイントの設定]**|タスク上のブレークポイントを有効にし、ブレークポイントのプロパティを設定します。|**[制御フロー]** タブのデザイン画面でタスクまたはコンテナーを右クリックし、 **[ブレークポイントの設定]** をクリックします。 パッケージ上のブレークポイントを設定するには、 **[制御フロー]** タブのデザイン画面で任意の場所を右クリックし、 **[ブレークポイントの設定]** をクリックします。|  
  
 **[作業の開始]** ウィンドウには、サンプル、チュートリアル、およびビデオへのリンクが表示されます。 その他のコンテンツへのリンクを追加するには、現在のリリースの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]に付属する SamplesSites.xml ファイルを変更します。 RSS フィードの URL を指定する \<GettingStartedSamples> 要素値は変更しないでください。 このファイルは、\<*ドライブ*>:\Program Files\Microsoft SQL Server\110\DTS\Binn フォルダーにあります。 64 ビット コンピューターでは、このファイルは、\<*ドライブ*>:\Program Files(x86)\Microsoft SQL Server\110\DTS\Binn フォルダーにあります。  
  
 SamplesSites.xml ファイルが破損した場合は、ファイルの XML を次の既定の XML で置き換えてください。  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>https://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>https://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 次の表は、 **[SSIS]** メニュー、 **[表示]** メニュー、および [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーのデザイン画面から使用できるウィンドウの一覧です。  
  
|ウィンドウ|目的|アクセス|  
|------------|-------------|------------|  
|**変数**|カスタム変数を追加して管理します。|**[SSIS]** メニューの **[変数]** をクリックします。<br /><br /> \- または -<br /><br /> **[制御フロー]** タブおよび **[データ フロー]** タブのデザイン画面で任意の場所を右クリックし、 **[変数]** をクリックします。<br /><br /> \- または -<br /><br /> **[表示]** メニューで **[その他のウィンドウ]** をポイントし、 **[変数]** をクリックします。|  
|**[ログ イベント]**|実行時にログ エントリを表示します。|**[SSIS]** メニューの **[ログ イベント]** をクリックします。<br /><br /> \- または -<br /><br /> **[制御フロー]** タブおよび **[データ フロー]** タブのデザイン画面で任意の場所を右クリックし、 **[ログ イベント]** をクリックします。<br /><br /> \- または -<br /><br /> **[表示]** メニューで **[その他のウィンドウ]** をポイントし、 **[ログ イベント]** をクリックします。|  
  
## <a name="custom-editors"></a>カスタム エディター  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、ほとんどのコンテナー、タスク、変換元、変換、および変換先用のカスタム ダイアログ ボックスが用意されています。  
  
 次の表では、カスタム ダイアログ ボックスへのアクセス方法について説明します。  
  
|エディターの種類|アクセス|  
|-----------------|------------|  
|コンテナー。 詳細については、「 [Integration Services コンテナー](control-flow/integration-services-containers.md)」を参照してください。|**[制御フロー]** タブのデザイン画面で、コンテナーをダブルクリックします。|  
|タスク。 詳細については、「 [Integration Services のタスク](control-flow/integration-services-tasks.md)」を参照してください。|**[制御フロー]** タブのデザイン画面で、タスクをダブルクリックします。|  
|変換元。|**[データ フロー]** タブのデザイン画面で、変換元をダブルクリックします。|  
|変換。 詳細については、「 [Integration Services の変換](data-flow/transformations/integration-services-transformations.md)」を参照してください。|**[データ フロー]** タブのデザイン画面で、変換をダブルクリックします。|  
|変換先。|**[データ フロー]** タブのデザイン画面で、変換先をダブルクリックします。|  
  
## <a name="advanced-editor"></a>[詳細エディター]  
 **[詳細エディター]** ダイアログ ボックスは、データ フロー コンポーネントを構成するためのユーザー インターフェイスです。 このダイアログ ボックスには、汎用的なレイアウトを使用して、コンポーネントのプロパティが反映されています。 **[詳細エディター]** ダイアログ ボックスは、複数の入力を含む [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の変換には使用できません。  
  
 このエディターを開くには、 **[プロパティ]** ウィンドウで **[詳細エディターの表示]** をクリックするか、データ フロー コンポーネントを右クリックして **[詳細エディターの表示]** をクリックします。  
  
 カスタム変換元、変換、または変換先を作成する場合で、カスタム ユーザー インターフェイスを記述しない場合は、代わりに **[詳細エディター]** を使用できます。  
  
## <a name="sql-server-data-tools-features"></a>SQL Server データ ツールの機能  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを使用して作業するためのウィンドウ、ダイアログ ボックス、およびメニュー オプションが用意されています。  
  
 次は、使用できるウィンドウおよびメニューの概要です。  
  
-   **[ソリューション エクスプローラー]** ウィンドウ。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開発する [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトなどのプロジェクト、およびプロジェクト ファイルが一覧表示されます。  
  
     プロジェクトに含まれるパッケージを名前で並べ替えるには、 **[SSIS パッケージ]** ノードを右クリックし、 **[名前で並べ替え]** をクリックします。  
  
-   **[ツールボックス]** ウィンドウ。制御フローやデータ フローを構築するための、制御フロー アイテムおよびデータ フロー アイテムが一覧表示されます。  
  
-   **[プロパティ]** ウィンドウ。オブジェクトのプロパティが一覧表示されます。  
  
-   **[フォーマット]** メニュー。パッケージでサイズ変更や整列を行うための制御オプションが用意されています。  
  
-   **[編集]** メニュー。デザイン画面上でオブジェクトをコピーするための、コピーおよび貼り付けの機能が用意されています。  
  
-   **[表示]** メニュー。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでのオブジェクトのグラフィカル表示を変更するためのオプションが用意されています。  
  
 その他のウィンドウおよびメニューの詳細については、Visual Studio のマニュアルを参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]でパッケージを作成する方法については、「 [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SSIS デザイナー](ssis-designer.md)  
  
  
