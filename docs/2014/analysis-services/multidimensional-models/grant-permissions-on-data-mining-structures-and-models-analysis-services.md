---
title: データ マイニング構造およびモデル (Analysis Services) に対する権限の付与 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.miningmodels.f1
helpviewer_keywords:
- data mining [Analysis Services], security
- permissions [Analysis Services], mining models
- mining models [Analysis Services], security
- mining structures [Analysis Services], security
- permissions [Analysis Services], mining structures
- user access rights [Analysis Services], mining structures
- user access rights [Analysis Services], mining models
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25eb8fe00c523d4a94b7f6f0325bfd2c1f55e7be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074938"
---
# <a name="grant-permissions-on-data-mining-structures-and-models-analysis-services"></a>データ マイニング構造およびデータ マイニング モデルに対する権限の付与 (Analysis Services)
  既定では、Analysis Services サーバー管理者にのみ、データベースのデータ マイニング構造またはマイニング モデルを表示する権限があります。 管理者以外のユーザーに権限を付与するには、次の手順に従ってください。  
  
## <a name="set-permissions-to-access-a-mining-structure"></a>マイニング構造にアクセスするための権限の設定  
  
1.  SSMS で、Analysis Services に接続します。 手順について不明な点がある場合は、「[クライアント アプリケーションからの接続 &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md)」を参照してください。  
  
2.  オブジェクト エクスプローラーで **[データベース]** フォルダーを開き、データベースを選択します。  
  
3.  **[ロール]** を右クリックし、 **[新しいロール]** を選択します。  
  
4.  [全般] ページで、名前を入力し、必要に応じて説明を入力します。 このページには、フル コントロール、データベースの処理、定義の読み取りなどデータベース権限もいくつか含まれています。 これらのいずれの権限も、データ マイニングのアクセスには必要ありません。 データべース権限の詳細については、「[データベース権限の付与 &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)」を参照してください。  
  
5.  **[マイニング構造]** ペインで、データ マイニング構造ごとに **[読み取り]** または **[読み取り/書き込み]** を選択します。  
  
6.  **[メンバーシップ]** ペインで、このロールを使用して Analysis Services に接続する Windows ユーザー アカウントおよびグループ アカウントを追加します。  
  
7.  **[OK]** をクリックして、ロールの作成を終了します。  
  
## <a name="set-permissions-to-access-a-mining-model"></a>マイニング モデルにアクセスするための権限の設定  
 データ マイニング モデルの場合、ロールに **[読み取り]** 権限または **[読み取り/書き込み]** 権限を設定できるほか、 **[ドリルスルー]** 権限および **[定義の読み取り]** 権限を設定して基になるデータの表示および参照を許可することもできます。  
  
 **注** マイニング構造とマイニング モデルの両方についてドリルスルーを有効にした場合、そのマイニング モデルとマイニング構造に対するドリルスルー権限を持つロールのすべてのメンバー ユーザーが、マイニング構造内の列を表示できるようになります。これらの列がマイニング モデルに含まれていなかったとしても同様です。 したがって、機密情報を保護するため、個人情報をマスクするデータ ソース ビューを設定し、マイニング構造に対するドリルスルー アクセスは必要な場合にのみ許可する必要があります。  
  
 データベース ロールに読み取り権限または読み取り/書き込み権限を与えるには、ユーザーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバー ロールのメンバーであるか、フル コントロール (管理者) 権限を持つ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース ロールのメンバーである必要があります。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続し、オブジェクト エクスプローラーで適切なデータベースの **[ロール]** を展開し、データベース ロールをクリックするか、新しいデータベース ロールを作成します。  
  
2.  **[マイニング構造]** ペインで、 **[マイニング モデル]** ボックスの一覧からマイニング モデルを見つけ、そのマイニング モデルの **[読み取り]** 、 **[読み取り/書き込み]** 、 **[ドリルスルー]** 、または **[参照]** を選択します。  
  
3.  **[メンバーシップ]** ペインで、このロールを使用して Analysis Services に接続する Windows ユーザー アカウントおよびグループ アカウントを追加します。  
  
4.  **[OK]** をクリックして、ロールの作成を終了します。  
  
 データ マイニング拡張機能 (DMX) の OPENQUERY 句を使用するドリルスルー クエリでデータ ソースを使用するには、適切なデータ ソース オブジェクトに対する読み取り/書き込み権限もデータベース ロールに与える必要があります。 詳細については、「[データ ソース オブジェクトに対する権限の付与 &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)」および[OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery)」を参照してください。  
  
> [!NOTE]  
>  既定では、OPENROWSET を使った DMX クエリの送信が無効になっています。  
  
## <a name="see-also"></a>参照  
 [サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [キューブ権限またはモデル権限の付与 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [ディメンション データへのカスタム アクセス権の付与 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [セル データへのカスタム アクセス権の付与 &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
