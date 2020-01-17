---
title: URL アクセスを使用してレポート履歴スナップショットを表示する | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2caf9def46440aa87f8b4e143cc9e3163e408ba5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580804"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>URL アクセスを使用してレポート履歴スナップショットを表示する
  *rs:Snapshot* パラメーターを指定し、その値を有効なスナップショット ID に設定することによって、レポート履歴スナップショットに基づくレポートを表示できます。 パラメーターの値は、国際標準化機構 (ISO) 8601 の標準に基づく、YYYY-MM-DDTHH:MM:SS の形式です。  
  
 このパラメーターを省略した場合、レポートは、レポート サーバーのレポート実行およびキャッシュ管理オプションの設定に基づいて表示されます。 レポートの実行方法については、「 [レポート処理プロパティの設定](../reporting-services/report-server/set-report-processing-properties.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例は、レポート履歴スナップショットを取得する URL を示します。  
  
```  
https://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>参照  
 [URL アクセス &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md)  
  
  
