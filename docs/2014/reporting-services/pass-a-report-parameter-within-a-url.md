---
title: URL 内でレポート パラメーターを渡す | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 97fa6d01fc4a06825814c8494268ecb668f1da7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108112"
---
# <a name="pass-a-report-parameter-within-a-url"></a>URL 内でレポート パラメーターを渡す
  レポート パラメーターはレポート URL に含めることでレポートに渡すことができます。 このような URL パラメーターにはプレフィックスを付けません。パラメーターはレポート処理エンジンに直接渡されるためです。  
  
> [!IMPORTANT]  
>  SharePoint および `_vti_bin` HTTP プロキシ経由で要求をルーティングする [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] プロキシ構文を URL に含めることは重要です。 プロキシによって、HTTP 要求にいくつかのコンテキストが追加されます。これは、SharePoint モード レポート サーバーに対してレポートを適切に実行するために必要なコンテキストです。  
>   
>  プロキシ構文を含めない場合は、パラメーターの先頭に *rp:* を付ける必要があります。  
  
 すべてのクエリ パラメーターには、対応するレポート パラメーターを指定できます。 クエリ パラメーターをレポートに渡すには、対応するレポート パラメーターを渡します。 詳細については、「[リレーショナル クエリ デザイナーでのクエリの作成 &#40;レポート ビルダーおよび SSRS&#41;](report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)」を参照してください。  
  
> [!IMPORTANT]
>  レポート パラメーターでは大文字と小文字が区別されます。  
> 
> [!NOTE]
>  レポート パラメーターでは大文字と小文字が区別され、次の特殊文字が使用されます。  
> 
>  -   URL 文字列では、URL エンコード規格に基づいてすべての空白文字が文字列 "%20" に置き換えられます。  
> -   URL のパラメーター部分にある空白文字はプラス記号 (+) に置き換えられます。  
> -   文字列の任意の部分にあるセミコロンは文字列 "%3A" に置き換えられます。  
> -   通常、適切な URL エンコードはブラウザーによって自動的に行われます。 これらの文字を手動でエンコードする必要はありません。  
  
 URL 内にレポート パラメーターを設定するには、次の構文を使用します。  
  
```  
  
parameter=value  
```  
  
 たとえば、レポートで定義されている "ReportMonth" と "ReportYear" の 2 つのパラメーターを指定するには、ネイティブ モードのレポート サーバーで次の URL を使用します。  
  
```  
http://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 たとえば、レポートで定義されている同じ 2 つのパラメーターを指定するには、SharePoint 統合モードのレポート サーバーで次の URL を使用します。 `/_vti_bin`に注意してください。  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 パラメーターに NULL 値を渡すには、次の構文を使用します。  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 例を次に示します。  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 `Boolean` 値を渡す場合、False には 0 を、True には 1 を使用します。 `Float` 値を渡すには、サーバー ロケールに応じた小数点の記号を指定します。  
  
> [!NOTE]  
>  既定値を持つレポート パラメーターがレポートに含まれており、`Prompt` プロパティの値が `false` である場合 (つまりレポート マネージャーで Prompt User プロパティが選択されていない場合)、URL 内でそのレポート パラメーターに値を渡すことはできません。 管理者はこの方法を使用して、エンド ユーザーが特定のレポート パラメーターの値を追加したり変更したりすることを禁止できます。  
  
##  <a name="bkmk_examples"></a> その他の例  
 次の URL の例には、空白や複数のパラメーターが含まれています。  
  
-   "SQL Server User Education Team" のフォルダー名には空白が含まれているため、各空白が "+" に置き換わります。  
  
-   "team project report" というレポート名には空白が含まれているため、各空白が "+" に置き換わります。  
  
-   値 "xgroup" を指定した "teamgrouping2" および値 "ygroup" を指定した "teamgrouping1" という 2 つのパラメーターを渡します。  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 次の URL の例には、複数の値を持つパラメーター "OrderID" が含まれています。 複数の値を持つパラメーターの形式では、値ごとにパラメーター名を繰り返します。  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 次の URL の例では、"7/1/2005" という値を持つ単一のパラメーター *SellStartDate* を、ネイティブ モードのレポート サーバーに渡します。  
  
```  
http://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>関連項目  
 [URL アクセス &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL アクセス パラメーター リファレンス](url-access-parameter-reference.md)  
  
  
