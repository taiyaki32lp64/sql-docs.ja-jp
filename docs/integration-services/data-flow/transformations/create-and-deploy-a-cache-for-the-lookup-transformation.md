---
title: 参照変換用のキャッシュを作成および配置する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- creating cache files for Lookup transformation
- deploying cache files for Lookup transformation
- Lookup transformation cache files
ms.assetid: cedf5cad-2fac-42d0-ad91-9461e117d330
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e53569a8680ec3a6414aeeaa83e9322e77568ecf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297973"
---
# <a name="create-and-deploy-a-cache-for-the-lookup-transformation"></a>参照変換用のキャッシュを作成および配置する

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  参照変換用のキャッシュ ファイル (.caw) を作成および配置できます。 参照データセットはキャッシュ ファイルに格納されます。  
  
 参照変換は、接続されているデータ ソースの入力列のデータを参照データセットの列と結合することにより参照を実行します。  
  
 キャッシュ接続マネージャーおよびキャッシュ変換を使用して、キャッシュ ファイルを作成します。 詳細については、「 [キャッシュ接続マネージャー](../../../integration-services/data-flow/transformations/cache-connection-manager.md) 」と「 [キャッシュ変換](../../../integration-services/data-flow/transformations/cache-transform.md)」を参照してください。  
  
 参照変換とキャッシュ ファイルの詳細については、「 [参照変換](../../../integration-services/data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
### <a name="to-create-a-cache-file"></a>キャッシュ ファイルを作成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開き、そのパッケージを開きます。  
  
2.  **[制御フロー]** タブで、データ フロー タスクを追加します。  
  
3.  **[データ フロー]** タブで、データ フローにキャッシュ変換を追加し、変換をデータ ソースに接続します。  
  
     必要に応じて、データ ソースを構成します。  
  
4.  キャッシュ変換をダブルクリックし、 **[キャッシュ変換エディター]** の **[接続マネージャー]** ページで **[新規作成]** をクリックして、新しい接続マネージャーを作成します。  
  
5.  **[キャッシュ接続マネージャー エディター]** ダイアログ ボックスの **[全般]** タブで、次のオプションを選択してキャッシュを保存するようにキャッシュ接続マネージャーを構成します。  
  
    1.  **[ファイル キャッシュを使用する]** をオンにします。  
  
    2.  **[ファイル名]** に、ファイル パスを入力します。  
  
     パッケージを実行すると、ファイルが作成されます。  
  
    > [!NOTE]  
    >  パッケージの保護レベルは、キャッシュ ファイルに適用されません。 キャッシュ ファイルに機密情報が含まれている場合は、アクセス制御リスト (ACL) を使用して、ファイルを格納している場所またはフォルダーへのアクセスを制限します。 特定のアカウントに対してのみアクセスを有効にする必要があります。 詳細については、「 [パッケージで使用されるファイルへのアクセス](../../../integration-services/security/security-overview-integration-services.md#files)」を参照してください。  
  
6.  **[列]** タブをクリックし、 **[インデックス位置]** オプションを使用して、インデックス列として使用する列を指定します。  
  
     インデックス以外の列の場合、インデックス位置は 0 です。 インデックス列の場合、インデックスの位置は連続した正の数になります。  
  
    > [!NOTE]  
    >  参照変換がキャッシュ接続マネージャーを使用するように構成されている場合、参照データセット内のインデックス列のみ入力列にマップできます。 また、すべてのインデックス列をマップする必要があります。  
  
     詳細については、「 [キャッシュ接続マネージャー エディター](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)」を参照してください。  
  
7.  必要に応じてキャッシュ変換を構成します。  
  
     詳細については、「[キャッシュ変換エディター &#40;[接続マネージャー] ページ&#41;](../../../integration-services/data-flow/transformations/cache-transformation-editor-connection-manager-page.md)」および「[キャッシュ変換エディター &#40;[マッピング] ページ&#41;](../../../integration-services/data-flow/transformations/cache-transformation-editor-mappings-page.md)」を参照してください。  
  
8.  パッケージを実行します。  
  
### <a name="to-deploy-a-cache-file"></a>キャッシュ ファイルを配置するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開き、そのパッケージを開きます。  
  
2.  必要に応じて、パッケージ構成を作成します。 詳細については、「 [パッケージ構成を作成する](../../../integration-services/packages/create-package-configurations.md)」を参照してください。  
  
3.  次の操作を行って、キャッシュ ファイルをプロジェクトに追加します。  
  
    1.  ソリューション エクスプローラーで、手順 1. で開いたプロジェクトを選択します。  
  
    2.  **[プロジェクト]** メニューの **[既存項目の追加]** をクリックします。  
  
    3.  キャッシュ ファイルを選択し、 **[追加]** をクリックします。  
  
     ソリューション エクスプローラーの **[その他]** フォルダーに、選択したキャッシュ ファイルが表示されます。  
  
4.  配置ユーティリティを作成するようにプロジェクトを構成し、プロジェクトをビルドします。 詳細については、「 [配置ユーティリティを作成する](../../../integration-services/packages/create-a-deployment-utility.md)」を参照してください。  
  
     マニフェスト ファイル \<*プロジェクト名*>.SSISDeploymentManifest.xml が作成されて、プロジェクトに含まれるその他のファイル、パッケージ、およびパッケージ構成の一覧が示されます。  
  
5.  パッケージをファイル システムに配置します。 詳細については、「 [配置ユーティリティを使用してパッケージを配置する](../../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [配置ユーティリティを作成する](../../../integration-services/packages/create-a-deployment-utility.md)  
  
  
