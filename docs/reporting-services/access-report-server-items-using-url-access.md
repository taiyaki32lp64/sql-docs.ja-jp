---
title: "URL アクセスを使用してレポート サーバー アイテムにアクセス |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: fa59193fcedb1d5437d8df14035fadca2b3a28f1
ms.openlocfilehash: 475435073cef3f748e26a2a71c31a55fa7e6304d
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="access-report-server-items-using-url-access"></a>URL アクセスを使用したレポート サーバー アイテムへのアクセス
  このトピックは、方法、レポート内のさまざまな種類のカタログ項目にアクセスするサーバー データベースまたは SharePoint サイトを使用してについて説明します。 *Rs:command*=*値*です。 実際にこのパラメーター文字列を追加する必要はありません。 この文字列を省略した場合、レポート サーバーがアイテムの種類を評価し、適切なパラメーター値を自動的に選択します。 ただし、URL に *rs:Command*=*Value* 文字列を使用することで、レポート サーバーのパフォーマンスを向上できます。  
  
 以下の例では、 `_vti_bin` プロキシ構文に注意してください。 プロキシ構文の詳細については、「 [URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md)」を参照してください。  
  
## <a name="access-a-report"></a>レポートへのアクセス  
 ブラウザーでレポートを表示するには、 *rs:Command*=*Render* パラメーターを使用します。 例:  
  
 - **ネイティブ** `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
 - **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  SharePoint および `_vti_bin` HTTP プロキシ経由で要求をルーティングする [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] プロキシ構文を URL に含めることは重要です。 プロキシによって、HTTP 要求にいくつかのコンテキストが追加されます。これは、SharePoint モード レポート サーバーに対してレポートを適切に実行するために必要なコンテキストです。  
  
## <a name="access-a-resource"></a>リソースへのアクセス  
 リソースにアクセスするには、 *rs:Command*=*GetResourceContents* パラメーターを使用します。画像などのリソースがブラウザーと互換性がある場合は、ブラウザーにリソースが表示されます。 それ以外の場合は、ファイルまたはリソースを開くか、ディスクに保存するように要求されます。  
  
 **ネイティブ** `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>データ ソースへのアクセス  
 データ ソースにアクセスするには、 *rs:Command*=*GetDataSourceContents* パラメーターを使用します。 ブラウザーで XML がサポートされている場合、そのデータ ソース定義が表示されます。ただし、目的のデータ ソースに対して **Read Contents** 権限が与えられている認証ユーザーであることが条件となります。 例:  
  
 **ネイティブ** `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 XML 構造は、次の例のようになります。  
  
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
  
 **ネイティブ** `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 表示されるユーザー インターフェイスは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Server (IIS) で使用されるディレクトリ参照モードと似ています。 ビルド番号を含むレポート サーバーのバージョン番号もフォルダー一覧の下に表示されます。  
  
## <a name="see-also"></a>参照  
 [URL アクセスと #40 です。SSRS &#41;](../reporting-services/url-access-ssrs.md)   
 [URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md) 
