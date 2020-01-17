---
title: URL アクセスを使用したレポート サーバー アイテムへのアクセス | Microsoft Docs
ms.date: 05/08/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 52222f154ccc8068c77b0925f246e738a66721cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581258"
---
# <a name="access-report-server-items-using-url-access"></a>URL アクセスを使用したレポート サーバー アイテムへのアクセス
  このトピックでは、*rs:Command*=*Value* を使用してレポート サーバー データベースまたは SharePoint サイトにある異なる種類のカタログ アイテムにアクセスする方法について説明します。 実際にこのパラメーター文字列を追加する必要はありません。 この文字列を省略した場合、レポート サーバーがアイテムの種類を評価し、適切なパラメーター値を自動的に選択します。 ただし、URL に *rs:Command*=*Value* 文字列を使用することで、レポート サーバーのパフォーマンスを向上できます。  
  
 以下の例では、 `_vti_bin` プロキシ構文に注意してください。 プロキシ構文の詳細については、「 [URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md)」を参照してください。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
## <a name="access-a-report"></a>レポートへのアクセス  
 ブラウザーでレポートを表示するには、 *rs:Command*=*Render* パラメーターを使用します。 例:  
  
 - **ネイティブ** `https://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 - **SharePoint** `https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  SharePoint および `_vti_bin` HTTP プロキシ経由で要求をルーティングする [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] プロキシ構文を URL に含めることは重要です。 プロキシによって、HTTP 要求にいくつかのコンテキストが追加されます。これは、SharePoint モード レポート サーバーに対してレポートを適切に実行するために必要なコンテキストです。  

::: moniker-end
  
## <a name="access-a-resource"></a>リソースへのアクセス  
 リソースにアクセスするには、 *rs:Command*=*GetResourceContents* パラメーターを使用します。画像などのリソースがブラウザーと互換性がある場合は、ブラウザーにリソースが表示されます。 それ以外の場合は、ファイルまたはリソースを開くか、ディスクに保存するように要求されます。  
  
 **ネイティブ** `https://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
 **SharePoint** `https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  

::: moniker-end
  
## <a name="access-a-data-source"></a>データ ソースへのアクセス  
 データ ソースにアクセスするには、 *rs:Command*=*GetDataSourceContents* パラメーターを使用します。 ブラウザーで XML がサポートされている場合、そのデータ ソース定義が表示されます。ただし、目的のデータ ソースに対して **Read Contents** 権限が与えられている認証ユーザーであることが条件となります。 例:  
  
 **ネイティブ** `https://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
 **SharePoint** `https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 XML 構造は、次の例のようになります。  

::: moniker-end
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 接続文字列は、レポート サーバーの **SecureConnectionLevel** 設定に基づいて返されます。 **SecureConnectionLevel** 設定の詳細については、「 [セキュリティで保護された Web サービス メソッドの使用](../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)」を参照してください。  
  
## <a name="access-the-contents-of-a-folder"></a>フォルダーのコンテンツへのアクセス  
 フォルダーのコンテンツにアクセスするには、 *rs:Command*=*GetChildren* パラメーターを使用します。 要求されたフォルダーのサブフォルダー、レポート、データ ソース、およびリソースへのリンクを含む汎用フォルダー ナビゲーション ページが返されます。 例:  
  
 **ネイティブ** `https://myrshost/reportserver?/Sales&rs:Command=GetChildren`  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
 **SharePoint** `https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rs:Command=GetChildren`  

::: moniker-end
  
 表示されるユーザー インターフェイスは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Server (IIS) で使用されるディレクトリ参照モードと似ています。 ビルド番号を含むレポート サーバーのバージョン番号もフォルダー一覧の下に表示されます。  
  
## <a name="see-also"></a>参照  
 [URL アクセス &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md) 
