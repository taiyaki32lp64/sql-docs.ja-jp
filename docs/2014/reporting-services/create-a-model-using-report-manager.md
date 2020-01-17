---
title: レポート マネージャーを使用して、モデルの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report models [Reporting Services], creating
- Report Manager [Reporting Services], model creation
ms.assetid: 8e5d2bd3-48ec-45f3-afee-6d86797c8f28
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b67e2a7048520d8a411789e501dbbe545d3cc02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109673"
---
# <a name="create-a-model-using-report-manager"></a>レポート マネージャーを使用してモデルを作成する
  レポート マネージャーを使用すると、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のキューブ、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のデータベース、Oracle のデータベースからモデルを生成できます。 レポート モデルは、レポート サーバーにパブリッシュされている共有データ ソースから生成されます。 まだ共有データ ソースがない場合は、作成する必要があります。  
  
 生成されるレポート モデルは、共有データ ソースのスキーマに完全に基づいています。 データ ソースのどの部分をモデルに含めるかを選択したり、生成されるモデルのルールやメタデータを編集したりすることはできません。 ただし、モデルが生成された後でモデルのプロパティを設定したり、モデル全体またはモデルの一部へのアクセスを制限するロールの割り当てを定義したりすることはできます。  
  
> [!NOTE]  
>  レポート マネージャーを使用して生成された Oracle ベースのモデルまたは[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] Oracle データ ソースへの接続に使用するユーザー アカウントのスキーマの一部であるデータベース オブジェクトが含まれます。 ユーザー アカウント名は、データ ソース プロパティの資格情報で指定されます。  
  
### <a name="to-create-a-new-data-source-for-a-report-model-using-report-manager"></a>レポート マネージャーを使用してレポート モデルの新しいデータ ソースを作成するには  
  
1.  Web ブラウザーで、アドレス バーにレポート サーバーの URL を入力します。  
  
2.  **[新しいデータ ソース]** をクリックします。  
  
3.  **[名前]** ボックスに、データ ソースの名前を入力します。  
  
4.  必要に応じて、 **[説明]** ボックスにモデルの簡単な説明を入力します。  
  
5.  **[このデータ ソースを有効にする]** チェック ボックスがオンになっていることを確認します。  
  
6.  **[接続の種類]** ボックスの一覧で、接続先のデータ ソースの種類を選択します。 接続の種類は、次のいずれかである必要があります。**Oracle**、 **Microsoft SQL Server**または**Microsoft SQL Server Analysis Services**します。  
  
7.  **[接続文字列]** ボックスに、データベースを指す接続文字列を入力します。  
  
8.  レポート ビルダーのユーザーがデータベースに接続するために使用する必要のある接続方法を選択します。  
  
    -   Windows 認証:オペレーティング システムに認証する場合は、このオプションを選択[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ユーザー。 このオプションを選択すると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、パスワードの暗号化などの Windows のセキュリティ機能を使用してユーザーを認証します。 このオプションを選択することを強くお勧めします。  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証:ユーザーを使用する場合は、このオプションを選択、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ログイン アカウントを作成します。 ユーザーは、正しい [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログイン名とパスワードを入力する必要があります。  
  
        > [!CAUTION]  
        >  できるだけ Windows 認証を使用してください。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-report-model-using-report-manager"></a>レポート マネージャーを使用してレポート モデルを作成するには  
  
1.  レポート マネージャーで、モデルに使用するデータ ソースを選択します。  
  
     [プロパティ] ページが表示されます。  
  
2.  データ ソースに対して指定したオプションが必要かどうかを確認します。  
  
3.  **[モデルの生成]** をクリックします。  
  
     データ ソースの [全般] ページが表示されます。  
  
4.  **[名前]** ボックスに、レポート モデルの名前を入力します。  
  
5.  **[説明]** ボックスに、モデルの簡単な説明を入力します。  
  
6.  レポート モデルの保存先として新しい場所を指定するには、 **[場所の変更]** をクリックします。  
  
     既定では、レポート モデルはレポート マネージャーの [ホーム] に保存されます。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     レポート モデルが作成され、指定した場所に保存されます。 レポート マネージャーを使用して、このモデルに権限を割り当てることができます。  
  
## <a name="see-also"></a>参照  
 [ネイティブ モードのレポート サーバーに対する権限の許可](security/granting-permissions-on-a-native-mode-report-server.md)   
 [データ接続、データ ソース、および Reporting Services の接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [[新しいデータ ソース] ページ (レポート マネージャー)](../../2014/reporting-services/new-data-source-page-report-manager.md)  
  
  
