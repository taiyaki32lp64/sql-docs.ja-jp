---
title: 権限借用の設定 (SSAS - 多次元) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.impersonationinfo.f1
helpviewer_keywords:
- Impersonation Information dialog box
ms.assetid: 8e127f72-ef23-44ad-81e6-3dd58981770e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3bd6de297f4b5b677db10861e594afc36f74bb5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072959"
---
# <a name="set-impersonation-options-ssas---multidimensional"></a>権限借用オプションの設定 (SSAS - 多次元)
  Analysis Services モデルで`data source` オブジェクトを作成するときに構成する必要がある設定の 1 つに、権限借用オプションがあります。 このオプションでは、接続関連のローカルの操作 (OLE DB データ プロバイダーの読み込みや、移動プロファイルをサポートする環境でのユーザー プロファイル情報の解決など) を実行するときに、Analysis Services で特定の Windows ユーザー アカウントの ID を使用するかどうかを指定します。  
  
 Windows 認証を使用する接続の場合、権限借用オプションにより、外部データ ソースに対するクエリを実行する際のユーザー ID も決まります。 たとえば、権限借用オプションを **contoso\dbuser**に設定した場合、処理時にデータの取得に使用されるクエリはデータベース サーバーの **contoso\dbuser** として実行されます。  
  
 このトピックでは、データ ソース オブジェクトの構成時に **[権限借用情報]** ダイアログ ボックスで権限借用オプションを設定する方法について説明します。  
  
## <a name="set-impersonation-options-in-sql-server-data-tools"></a>SQL Server Data Tools での権限借用オプションの設定  
  
1.  ソリューション エクスプローラーでデータ ソースをダブルクリックして、データ ソース デザイナーを開きます。  
  
2.  データ ソース デザイナーの **[権限借用情報]** タブをクリックします。  
  
3.  このトピックの「 [権限借用のオプション](#bkmk_options) 」で説明するオプションを選択します。  
  
## <a name="set-impersonation-options-in-management-studio"></a>Management Studio での権限借用オプションの設定  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、次のダイアログ ボックスのプロパティの参照ボタン ( **[...]** ) をクリックして、**[権限借用情報]** ダイアログ ボックスを開きます。  
  
-   **[データベースのプロパティ]** ダイアログ ボックスの、[データ ソースの権限借用情報] プロパティ。  
  
-   **[データ ソースのプロパティ]** ダイアログ ボックスの、[権限借用情報] プロパティ。  
  
-   **[アセンブリのプロパティ]** ダイアログ ボックスの、[権限借用情報] プロパティ。  
  
##  <a name="bkmk_options"></a> 権限借用のオプション  
 ダイアログ ボックスのすべてのオプションを使用できますが、すべてのオプションが各シナリオに適しているわけではありません。 以下の情報を参考にして、シナリオに最適なオプションを判断してください。  
  
 **[特定のユーザー名とパスワードを使用する]**  
 このオプションを選択、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクトは、この形式で指定された Windows ユーザー アカウントのセキュリティ資格情報を使用します。*\<ドメイン名 >***\\***\<ユーザー アカウント名 >* します。  
  
 データ アクセスのために特別に作成した専用の最小特権 Windows ユーザー ID を使用する場合に、このオプションを選択します。 たとえば、レポートで使用されるデータを取得するための汎用アカウントを定期的に作成している場合は、ここでそのアカウントを指定できます。  
  
 多次元データベースの場合、処理、ROLAP クエリ、不一致バインド、ローカル キューブ、マイニング モデル、リモート パーティション、リンク オブジェクト、ターゲットからソースへの同期に、指定した資格情報が使用されます。  
  
 表形式データベースの場合、処理、リレーショナル データ ストアに対して (DirectQuery を使用して) 実行されるクエリ、不一致バインド、リモート パーティション、ターゲットからソースへの同期に、指定した資格情報が使用されます。  
  
 DMX OPENQUERY ステートメントの場合、このオプションは無視され、指定したユーザーのアカウントではなく現在のユーザーの資格情報が使用されます。  
  
 **[サービス アカウントを使用する]**  
 このオプションを選択すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトを管理する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービスに関連付けられているセキュリティ資格情報が使用されます。 既定のオプションです。 以前のリリースでは、これが、使用できる唯一のオプションでした。 個々のユーザー アカウントではなく、サービス レベルでデータ アクセスを監視する場合は、このオプションを選択することをお勧めします。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、使用しているオペレーティング システムに応じて、サービス アカウントとして NetworkService または特定の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンス用に作成された組み込み仮想アカウントが使用されます。 Windows 認証を使用する接続にサービス アカウントを使用する場合は、処理時にデータの取得に使用されるため、このアカウント用のデータベース ログインを忘れずに作成して読み取り権限を付与してください。 サービス アカウントの詳細については、「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」をご覧ください。  
  
> [!NOTE]  
>  データベース認証を使用する際、Analysis Services の専用の仮想アカウントでサービスを実行する場合は、 **[サービス アカウントを使用する]** 権限借用オプションを選択してください。 このアカウントには、ローカル ファイルにアクセスする権限が付与されます。 一方、サービスを NetworkService として実行する場合は、 **[ローカル ログオンを許可する]** 権限を持つ最小特権の Windows ユーザー アカウントを使用する方が適しています。 指定するアカウントによっては、Analysis Services プログラム フォルダーに対するファイル アクセスの権限も付与する必要があります。  
  
 多次元データベースの場合、処理、ROLAP クエリ、リモート パーティション、リンク オブジェクト、ターゲットからソースへの同期に、サービス アカウント資格情報が使用されます。  
  
 表形式データベースの場合、処理、リレーショナル データ ストアに対して (DirectQuery を使用して) 実行されるクエリ、リモート パーティション、ターゲットからソースへの同期に、指定した資格情報が使用されます。  
  
 DMX OPENQUERY ステートメント、ローカル キューブ、およびマイニング モデルの場合、サービス アカウント オプションを選択しても、現在のユーザーの資格情報が使用されます。 サービス アカウント オプションは、不一致バインドではサポートされていません。  
  
> [!NOTE]  
>  サービス アカウントに Analysis Services インスタンスに対する管理者権限がない場合、キューブからデータ マイニング モデルを処理するときにエラーが発生することがあります。 詳細については、次を参照してください。[マイニング構造。DataSource が OLAP キューブの場合の処理中に問題](https://go.microsoft.com/fwlink/?LinkId=251610)します。  
  
 **[現在のユーザーの資格情報を使用する]**  
 このオプションを選択すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトにより、不一致バインド、DMX OPENQUERY、ローカル キューブ、マイニング モデルに現在のユーザーのセキュリティ資格情報が使用されます。  
  
 このオプションは表形式のデータベースではサポートされていません。  
  
 ローカル キューブおよび不一致バインドを使用した処理を除き、このオプションは多次元データベースではサポートされていません。  
  
 **[既定]** または **[継承]**  
 **[既定]** はデータベース レベルで設定されている権限借用オプションで使用され、 **[継承]** はデータ ソース レベルで設定されている権限借用オプションで使用されます。  
  
 **データ ソースの [継承] オプション**  
  
 データ ソース レベルでは、 **[継承]** によって [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が親オブジェクトの権限借用オプションを使用することが指定されます。 多次元モデルでは、親オブジェクトは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースです。 **[継承]** オプションを選択すると、対象のデータ ソースおよび同じデータベースに含まれる他のデータ ソースの権限借用設定を一元的に管理できます。 このオプションを有効にするには、データベース レベルで特定の Windows ユーザー名とパスワードを選択します。 データベース レベルで Windows ユーザー名とパスワードが指定されていない場合、データ ソースの **[継承]** とデータベースの **[既定]** の組み合わせは、サービス アカウント オプションを使用するのと同じです。  
  
 データベース レベルで Windows ユーザー名とパスワードを指定するには、次の操作を行います。  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] でデータベースを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[データ ソースの権限借用情報]** で、Windows ユーザー名とパスワードを指定します。  
  
3.  各データ ソースを右クリックし、プロパティを表示して、データ ソースが **[継承]** オプションを使用していることを確認します。  
  
 データベース レベルでの既定の設定に関する詳細については、「[多次元データベースのプロパティ設定 &#40;Analysis Services&#41;](set-multidimensional-database-properties-analysis-services.md)」を参照してください。  
  
 **データベースの既定のオプション**  
  
 表形式データベースの**既定**サービス アカウントを使用することを意味します。  
  
 多次元データベースの場合、 **[既定]** はサービス アカウントを使用し、データ マイニング操作に現在のユーザーを使用することを意味します。  
  
## <a name="see-also"></a>関連項目  
 [データ ソースの作成 &#40;SSAS 多次元&#41;](create-a-data-source-ssas-multidimensional.md)   
 [データ ソースのプロパティを設定&#40;SSAS 多次元&#41;](set-data-source-properties-ssas-multidimensional.md)   
 [DirectQuery の配置シナリオ&#40;SSAS 表形式&#41;](../directquery-deployment-scenarios-ssas-tabular.md)  
  
  
