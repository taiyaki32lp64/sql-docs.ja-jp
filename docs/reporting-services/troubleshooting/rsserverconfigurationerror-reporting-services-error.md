---
title: rsServerConfigurationError - Reporting Services エラー | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4291245b101799238412115ced8b114de5a551be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572140"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Reporting Services エラー
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|rsServerConfiguration|  
|イベント ソース|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|コンポーネント|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|メッセージ テキスト|レポート サーバーで構成エラーが発生しました。|  
  
## <a name="explanation"></a>説明  
 これは、レポート サーバーまたはレポート作成ツールの構成設定が無効な場合に発生する、一般的なエラーです。 通常、このエラーは、エラーの実際の原因を示す 2 番目のメッセージと共に表示されます。  
  
 考えられる原因を次に示します。  
  
-   RSReportServer.config ファイルまたは RSReportDesigner.config ファイルが見つからないか読み取ることができません。  
  
-   一方の構成ファイル内の XML 要素が見つからないか無効です。  
  
-   1 つまたは複数の XML 要素の値が見つからないか無効です。  
  
-   レジストリ設定が無効です。  
  
## <a name="user-action"></a>ユーザーの操作  
 構成ファイルを手動で編集した後にこのエラーが発生するようになった場合は、変更を破棄して以前の値を入力するか、バックアップがある場合は以前のバージョンを復元します。  
  
 **rsServerConfiguration** エラーに伴うエラー メッセージの詳細情報を確認するには、レポート サーバーのトレース ログ ファイルを確認します。このファイルは、\Microsoft SQL Server\MSRS12.\<instancename >\Reporting Services\LogFiles にあります。 詳細については、「 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)」を参照してください。  
  
## <a name="internal-only"></a>内部使用のみ  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
