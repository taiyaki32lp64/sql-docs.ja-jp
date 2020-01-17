---
title: パッケージを保存する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 60dcf1692fb8b805b9eef8fad228353104131c93
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295736"
---
# <a name="save-packages"></a>パッケージを保存する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用してパッケージを構築し、XML ファイル (.dtsx ファイル) としてファイル システムに保存します。 パッケージ XML ファイルのコピーは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の msdb データベースまたはパッケージ ストアに保存することもできます。 パッケージ ストアとは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが管理するファイル システムの場所にあるフォルダーのことです。  
  
 ファイル システムに保存したパッケージは、後で [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] またはパッケージ ストアにインポートできます。 詳細については、「[Integration Services サービス (SSIS サービス)](../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。  
  
 また、コマンド プロンプト ユーティリティの **dtutil**を使用して、ファイル システムと msdb 間でパッケージをコピーできます。 詳細については、「 [dtutil ユーティリティ](../integration-services/dtutil-utility.md)」を参照してください。  
## <a name="save-a-package-to-the-file-system"></a>ファイル システムにパッケージを保存する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、ファイルに保存するパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、保存するパッケージをクリックします。  
  
3.  **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
    > [!NOTE]  
    >  パッケージが保存されたファイルのパスと名前は、[プロパティ] ウィンドウで確認できます。  

## <a name="save-a-copy-of-a-package"></a>パッケージのコピーを保存する
  このセクションでは、パッケージのコピーをファイル システム、パッケージ ストア、または [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の **msdb** データベースに保存する方法について説明します。 パッケージのコピーを保存する場所を指定するとき、パッケージの名前を更新することもできます。  
  
 パッケージ ストアには、 **msdb** データベースとファイル システム内のフォルダーの両方、 **msdb**のみ、またはファイル システム内のフォルダーのみを含めることができます。 **msdb**では、パッケージは **sysssispackages** テーブルに保存されます。 このテーブルには、パッケージが属する論理フォルダーを識別する **folderid** 列があります。 論理フォルダーは、 **msdb** に保存されるパッケージをグループ化するための便利な方法を提供します。これは、ファイル システムのフォルダーが、ファイル システムに保存されるパッケージをグループ化する方法を提供するのと同じです。 **msdb** 内の **sysssispackagefolders** テーブルの行は、フォルダーを定義します。  
  
 **msdb** がパッケージ ストアの一部として定義されていない場合は、 **[パッケージのパス]** オプションで [SQL Server] を選択するときに、引き続きパッケージを既存の論理フォルダーに関連付けることができます。  
  
> [!NOTE]  
>  パッケージのコピーを保存するには、事前にパッケージを [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで開いておく必要があります。  
  
### <a name="to-save-a-copy-of-a-package"></a>パッケージのコピーを保存するには  
  
1.  ソリューション エクスプローラーで、コピーを保存するパッケージをダブルクリックします。  
  
2.  **[ファイル]** メニューの **[\<パッケージ ファイル> のコピーに名前を付けて保存]** をクリックします。  
  
3.  **[パッケージのコピーの保存]** ダイアログ ボックスで、 **[パッケージの場所]** 一覧からパッケージの保存場所を選択します。 使用できるオプションは以下のとおりです。  
    -   SQL Server
    -   [ファイル システム] 
    -   [SSIS パッケージ ストア] 
  
4.  保存場所が **[SQL Server]** または **[SSIS パッケージ ストア]** の場合、サーバー名を指定します。  
  
5.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に保存する場合は、認証の種類を指定します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用する場合、ユーザー名とパスワードを指定します。  
  
6.  パッケージのパスを指定するには、パスを入力するか、参照ボタン **[...]** をクリックしてパッケージの場所を指定します。 パッケージの既定の名前は Package です。 必要に応じて、パッケージの名前をニーズに合う名前に更新します。  
  
     **[パッケージのパス]** オプションとして **[SQL Server]** を選択した場合、パッケージのパスは、 **msdb** 内の論理フォルダーとパッケージ名で構成されます。 たとえば、パッケージ DownloadMonthlyData が [MSDB] フォルダー ( **msdb**内のルート論理フォルダーの既定の名前) 内の [Finance] フォルダーと関連付けられている場合、DownloadMonthlyData という名前のパッケージのパッケージ パスは MSDB/Finance/DownloadMonthlyData になります。  
  
     **[パッケージのパス]** オプションとして **[SSIS パッケージ ストア]** を選択した場合、パッケージのパスは、Integration Services サービスが管理するフォルダーで構成されます。 たとえば、パッケージ UpdateDeductions が、Integration Services サービスが管理するファイル システム フォルダー内の [HumanResources] フォルダーに存在する場合、パッケージのパスは /File System/HumanResources/UpdateDeductions になります。同様に、パッケージ PostResumes が [MSDB] フォルダー内の [HumanResources] フォルダーに関連付けられている場合、パッケージのパスは MSDB/HumanResources/PostResumes になります。  
  
     **[パッケージのパス]** オプションとして **[ファイル システム]** を選択した場合、パッケージのパスは、ファイル システム内の場所とファイル名になります。 たとえば、パッケージ名が UpdateDemographics の場合、パッケージのパスは C:\HumanResources\Quarterly\UpdateDemographics.dtsx になります。  
  
7.  パッケージの保護レベルを確認します。  
  
8.  必要に応じて、 **[保護レベル]** ボックスの近くの参照ボタン **[...]** をクリックし、保護レベルを変更します。  
  
    -   **[パッケージの保護レベル]** ダイアログ ボックスで、別の保護レベルを選択します。  
  
    -   **[OK]** をクリックします。  
  
9. **[OK]** をクリックします。  

## <a name="save-a-package-as-a-package-template"></a>パッケージをパッケージ テンプレートとして保存する
 このセクションでは、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で新しい Integration Services パッケージを作成するときに、カスタム パッケージをテンプレートとして指定および使用する方法について説明します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに新しいパッケージを追加する場合に、既定で、新しいパッケージを作成するパッケージ テンプレートを使用します。 この既定のテンプレートを置き換えることはできませんが、新しいテンプレートを追加することはできます。  
  
 テンプレートとして、複数のパッケージを指定できます。 カスタム パッケージをテンプレートとして実装するには、そのパッケージをあらかじめ作成しておく必要があります。  
  
 カスタム パッケージをテンプレートとして使用してパッケージを作成すると、新しいパッケージの名前と GUID は、テンプレートと同じになります。 パッケージを区別するには、 **Name** プロパティの値を更新して、 **ID** プロパティの新しい GUID を生成する必要があります。 詳細については、「[SQL Server データ ツールでのパッケージの作成](../integration-services/create-packages-in-sql-server-data-tools.md)」および「[パッケージのプロパティを設定する](../integration-services/set-package-properties.md)」を参照してください。  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>カスタム パッケージをパッケージ テンプレートとして指定するには  
  
1.  ファイル システムで、テンプレートとして使用するパッケージを指定します。  
  
2.  パッケージを DataTransformationItems フォルダーにコピーします。 既定では、このフォルダーは、C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject にあります。  
  
3.  テンプレートとして使用する各パッケージについて、手順 1. と手順 2. を繰り返します。  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>カスタム パッケージをパッケージ テンプレートとして使用するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、パッケージを作成する [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、プロジェクトを右クリックして **[追加]** をポイントし、 **[新しい項目]** をクリックします。  
  
3.  **[新しい項目の追加 - \<プロジェクト名>]** ダイアログ ボックスで、テンプレートとして使うパッケージをクリックします。  
  
     テンプレートの一覧には、"新しい SSIS パッケージ" という名前の既定のパッケージ テンプレートがあります。 パッケージ テンプレートとして使用できるテンプレートは、パッケージ アイコンで示されます。  
  
4.  **[追加]** をクリックします。  
