---
title: データソースの作成 (基本的なデータマイニングチュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3f85320a99c901a2fd71c9048750825569559099
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494025"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>データ ソースの作成 (基本的なデータ マイニング チュートリアル)
  *データソース*は、プロジェクトに保存および管理され、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]データベースに[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]配置されるデータ接続です。 データ ソースには、ソース データが存在するサーバーとデータベースの名前、および接続に必要なその他のプロパティが含まれます。  
  
> [!IMPORTANT]  
>  データベースの名前は [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] です。 このデータベースをまだインストールしていない場合は、 [MICROSOFT SQL サンプルデータベース](https://go.microsoft.com/fwlink/?LinkId=88417)のページを参照してください。  
  
### <a name="to-create-a-data-source"></a>データ ソースを作成するには  
  
1.  **ソリューションエクスプローラー**で、[**データソース**] フォルダーを右クリックし、[**新しいデータソース**] をクリックします。  
  
2.  [**データソースウィザードへようこそ**] ページで、[**次へ**] をクリックします。  
  
3.  [**接続の定義方法を選択**します] ページで、[**新規**] をクリック[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]してデータベースに接続を追加します。  
  
4.  [**接続マネージャー**] の [**プロバイダー** ] ボックスの一覧で、[**ネイティブ OLE Db\ SQL Server native Client 11.0**] を選択します。  
  
5.  [**サーバー名**] ボックスに、をインストール[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]したサーバーの名前を入力または選択します。  
  
     たとえば、データベースがローカルサーバーでホストされている場合は、「 **localhost** 」と入力します。  
  
6.  [**サーバーにログオン**する] で、[ **Windows 認証を使用する**] を選択します。  
  
    > [!IMPORTANT]  
    >  Windows 認証は SQL Server 認証よりも安全性に優れているので、実装時はできる限り Windows 認証を使用してください。 SQL Server 認証は旧バージョンとの互換性を維持するために提供されています。 認証方法の詳細については、「[データベースエンジンの構成-アカウントの準備](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md)」を参照してください。  
  
7.  [**データベース名の選択または入力**] ボックスの[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]一覧で、を選択し、[ **OK**] をクリックします。  
  
8.  [**次へ**] をクリックします。  
  
9. [**権限借用情報**] ページで、[**サービスアカウントを使用する**] をクリックし、[**次へ**] をクリックします。  
  
     [**ウィザードの完了**] ページで、既定では、データソースの名前が ADVENTURE works DW 2012 になっていることに注意してください。  
  
10. **[完了]** をクリックします。  
  
     新しいデータソース Adventure Works DW 2012 がソリューションエクスプローラーの [**データソース**] フォルダーに表示されます。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [データソースビュー &#40;の作成基本的なデータマイニングチュートリアル&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>このレッスンの前の作業  
 [Analysis Services プロジェクト&#40;の作成基本的なデータマイニングチュートリアル&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [データ ソースの作成 &#40;SSAS 多次元&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional)   
 [データソースの定義](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [権限借用オプションの設定 &#40;SSAS - 多次元&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional)  
  
  
