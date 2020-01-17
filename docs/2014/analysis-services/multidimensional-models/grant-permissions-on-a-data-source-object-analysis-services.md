---
title: データ ソース オブジェクト (Analysis Services) に対する権限の付与 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.datasources.f1
helpviewer_keywords:
- read/write permissions
- user access rights [Analysis Services], data sources
- security [Analysis Services], data sources
- connection strings [Analysis Services]
- data sources [Analysis Services], security
ms.assetid: b4e302d3-c93b-4383-aa4a-37d15c129830
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4a869d2033adaa57be0ace522787332c03a69bcb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074999"
---
# <a name="grant-permissions-on-a-data-source-object-analysis-services"></a>データ ソース オブジェクトに対する権限の付与 (Analysis Services)
  通常、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のユーザーは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの基になるデータ ソースへのアクセスを必要とすることはほとんどありません。 ユーザーは通常、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内部のデータを要求するクエリを発行するだけです。 ただし、データ マイニングのコンテキストでは、マイニング モデルに基づいた予測の実行など、マイニング モデルの登録済みデータをユーザーが入力したデータに結合しなければならない場合があります。 ユーザーが入力したデータが含まれているデータ ソースに接続するには、[OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery) 句または [OPENROWSET &#40;DMX&#41;](/sql/dmx/source-data-query-openrowset) 句を含んでいるデータ マイニング拡張機能 (DMX) クエリを使用します。  
  
 データ ソースに接続する DMX クエリを実行するには、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内のデータ ソース オブジェクトに対するアクセス権が必要です。 既定では、サーバー管理者またはデータベース管理者のみが、データ ソース オブジェクトにアクセスできます。 つまり、ユーザーは管理者から権限を付与されている場合を除いてデータ ソース オブジェクトにアクセスできません。  
  
> [!IMPORTANT]  
>  セキュリティ上の理由から、OPENROWSET 句内の開いている接続文字列を使用して DMX クエリを送信することはできないようになっています。  
  
## <a name="set-read-permissions-to-a-data-source"></a>データ ソースに対する読み取り権限の設定  
 データベース ロールには、データ ソース オブジェクトへのアクセス権をまったく与えないか、または読み取り権限を与えることができます。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続し、オブジェクト エクスプローラーで適切なデータベースの **[ロール]** を展開し、データベース ロールをクリックするか、新しいデータベース ロールを作成します。  
  
2.  **[データ ソース アクセス]** ペインで、 **[データ ソース]** ボックスの一覧からデータ ソース オブジェクトを探し、データ ソースの **[アクセス]** ボックスの一覧で **[読み取り]** を選択します。 このオプションを使用できない場合は、 **[全般]** ペインでフル コントロールが選択されているかどうかを確認してください。 フル コントロールによって権限が既に提供されているため、データ ソースに対する権限をオーバーライドすることはできません。  
  
## <a name="working-with-the-connection-string-used-by-a-data-source-object"></a>データ ソース オブジェクトが使用する接続文字列の操作  
 データ ソース オブジェクトには、基になるデータ ソースに接続するための接続文字列が含まれています。 この接続文字列を使用すると、次のいずれかを指定できます。  
  
-   **ユーザー名とパスワードを指定する**  
  
     データ ソース オブジェクトで使用される接続文字列によってユーザー名とパスワードを指定すると、それぞれ異なるユーザー アカウントが設定された複数のデータ ソース オブジェクトを作成できます。 複数のデータ ソース オブジェクトを作成すると、ユーザーが特定のデータ ソース オブジェクトにだけアクセスし、その他のデータ ソース オブジェクトにアクセスできないようにすることができます。 このようなその他のデータ ソース オブジェクトは、キューブやマイニング モデルなどのオブジェクトを処理するために [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自体によって使用されます。  
  
-   **Windows 認証を指定する**  
  
     データ ソース オブジェクトで使用される接続文字列によって Windows 認証を指定すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、クライアントの権限を借用できるようになります。 データ ソースがリモート コンピューターにある場合、そのリモート コンピューターと Analysis Services のコンピューターの両方に、Kerberos 認証を使用して、権限借用のための認証を設定する必要があります。設定しないとクエリは失敗します。 詳細については、「 [Kerberos の制約付き委任のための Analysis Services の構成](../instances/configure-analysis-services-for-kerberos-constrained-delegation.md) 」を参照してください。  
  
     OLE DB またはその他のクライアント コンポーネントの権限借用レベル プロパティを通じての権限借用をクライアントが許可していない場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、基になるデータ ソースに匿名接続しようとします。 リモート データ ソースへの匿名接続が成功することはほとんどありません。これは、大部分のデータ ソースで匿名アクセスが許可されないためです。  
  
## <a name="see-also"></a>関連項目  
 [多次元モデルのデータ ソース](data-sources-in-multidimensional-models.md)   
 [接続文字列のプロパティ &#40;Analysis Services&#41;](../instances/connection-string-properties-analysis-services.md)   
 [Analysis Services でサポートされる認証方法](../instances/authentication-methodologies-supported-by-analysis-services.md)   
 [ディメンション データへのカスタム アクセス権の付与 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [キューブ権限またはモデル権限の付与 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [セル データへのカスタム アクセス権の付与 &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
