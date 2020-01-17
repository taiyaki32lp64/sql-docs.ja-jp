---
title: Data Streaming Destination | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 06f2d0cef2cafa90476b4e3f5b6e68efe208c21b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293107"
---
# <a name="data-streaming-destination"></a>Data Streaming Destination

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Data Streaming Destination** は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) Destination コンポーネントであり、 **OLE DB Provider for SSIS** で SSIS パッケージの出力を表形式の結果セットとして利用することを可能にします。 OLE DB Provider for SSIS を利用するリンク サーバーを作成し、そのリンク サーバーで SQL クエリを実行し、SSIS パッケージが返したデータを表示できます。  
  
 下の例のクエリは、SSIS カタログの Power BI フォルダーに SSISPackagePublishing プロジェクトの Package.dtsx パッケージからの出力を返します。 このクエリは [Default Linked Server for Integration Services] という名前のリンク サーバーを利用し、このリンク サーバーは新しい OLE DB Provider for SSIS を利用します。 クエリには、SSIS カタログのフォルダー名、プロジェクト名、パッケージ名が含まれています。 OLE DB Provider for SSIS はクエリに指定されたパッケージを実行し、表形式の結果セットを返します。  
  
```sql
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>データ フィード パブリッシング コンポーネント  
 データ フィード パブリッシング コンポーネントにはコンポーネントとして、OLE DB Provider for SSIS、Data Streaming Destination、SSIS パッケージ パブリッシュ ウィザードが含まれています。 このウィザードでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース インスタンスで SSIS パッケージを SQL ビューとして公開できます。 このウィザードでは、OLE DB Provider for SSIS を利用するリンク サーバーとリンク サーバーでクエリを表示する SQL ビューを作成できます。 ビューを実行し、表形式のデータ セットとなっている SSIS パッケージからの結果にクエリを実行します。  
  
 SSISOLEDB プロバイダーがインストールされていることを確認するには、SQL Server Management Studio で、 **[サーバー オブジェクト]** 、 **[リンク サーバー]** 、 **[プロバイダー]** の順に展開し、 **SSISOLEDB** プロバイダーが表示されていることを確認します。 **[SSISOLEDB]** をダブルクリックし、有効になっていなければ、 **[InProcess 許可]** を有効にして **[OK]** をクリックします。  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>SQL ビューとして SSIS パッケージを公開する  
 以下では、SQL ビューとして SSIS パッケージを公開する手順について説明します。  
  
1.  SSIS パッケージを **Data Streaming Destination** コンポーネントで作成し、SSIS カタログにパッケージを配置します。  
  
2.  C:\Program Files\Microsoft SQL Server\130\DTS\Binn から ISDataFeedPublishingWizard.exe を実行するか、[スタート] メニューからデータ フィード パブリッシング ウィザードを実行し、 **SSIS パッケージ パブリッシュ ウィザード** を実行します。  
  
     このウィザードにより、OLE DB Provider for SSIS (SSISOLEDB) を利用するリンク サーバーが作成され、リンク サーバーのクエリを構成する SQL ビューが作成されます。 このクエリには、SSIS カタログのフォルダー名、プロジェクト名、およびパッケージ名が含まれます。  
  
3.  SQL Server Management Studio で SQL ビューを実行し、SSIS パッケージからの結果を確認します。 このビューにより、作成したリンク サーバーを経由して OLE DB Provider for SSIS にクエリが送信されます。 OLE DB Provider for SSIS はクエリに指定されたパッケージを実行し、表形式の結果セットを返します。  
  
> [!IMPORTANT]  
>  詳細な手順については、「[チュートリアル: SQL ビューとして SSIS パッケージを公開する](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)」を参照してください。  

## <a name="configure-data-streaming-destination"></a>Data Streaming Destination を構成する
  **[Data Streaming Destination の詳細エディター]** ダイアログ ボックスを使用して、Data Streaming Destination を構成します。 このダイアログ ボックスを開くには、コンポーネントをダブルクリックするか、データ フロー デザイナーでコンポーネントを右クリックしてから **[編集]** をクリックします。  
  
 このダイアログ ボックスには、 **[コンポーネントのプロパティ]** 、 **[入力列]** 、 **[入力プロパティと出力プロパティ]** という 3 つのタブがあります。  
  
## <a name="component-properties-tab"></a>[コンポーネントのプロパティ] タブ  
 このタブには、次の編集可能なフィールドがあります。  
  
|フィールド|[説明]|  
|-----------|-----------------|  
|[オブジェクト名]|パッケージ内の Data Streaming Destination コンポーネントの名前です。|  
|[ValidateExternalMetadata]|デザイン時に外部データ ソースを使用してコンポーネントを検証するかどうかを示します。 false に設定した場合、外部データ ソースに対する検証は実行時まで遅延されます。|  
|IDColumnName|データ フィード公開ウィザードによって生成されたビューには、この追加の ID 列があります。 ID 列は、データが他のアプリケーションによって OData フィードとして使用された場合に、データ フローからの出力データの EntityKey として機能します。<br /><br /> この列の既定の名前は _ID です。 この ID 列には別の名前を指定できます。|  
  
## <a name="input-columns-tab"></a>[入力列] タブ  
 このタブの上部ペインに、使用可能な入力列がすべて表示されます。 このコンポーネントの出力に含める列を選択します。 選択した列は、下部ペインの一覧に表示されます。 この一覧の **[出力の別名]** フィールドに新しい名前を入力することにより、出力列の名前を変更できます。  
  
## <a name="input-output-properties-tab"></a>[入力プロパティと出力プロパティ] タブ  
 [入力列] タブと同様に、このタブの出力列の名前は変更できます。左側のツリー ビューで、 **[Data Streaming Destination の入力]** 、 **[入力列]** の順に展開します。 入力列の名前をクリックし、右ペインで出力列の名前を変更します。
