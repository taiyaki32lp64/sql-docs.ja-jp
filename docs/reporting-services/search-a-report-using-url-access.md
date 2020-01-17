---
title: URL アクセスを使用してレポートを検索する | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b2568c2930080ddbb060f2c4d014c40476ab38f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570885"
---
# <a name="search-a-report-using-url-access"></a>URL アクセスを使用してレポートを検索する
  URL アクセスを使用して、レポート内に特定の文字列があるかどうかを検索できます。 レポート内を検索するには、URL の *rc:FindString* パラメーターの値として検索する文字列を設定します。 さらに、 *rc:StartFind* パラメーターと *rc:EndFind* パラメーターを使用すれば、検索対象をレポート内の特定のページに絞り込むことができます。  
  
## <a name="example"></a>例  
 次の URL アクセスの例では、Product Catalog サンプル レポートの 1 ～ 5 ページを検索し、最初に出現する Mountain-400 という文字列を探します。  
  
```  
https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>参照  
 [URL アクセス &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md)  
  
  
