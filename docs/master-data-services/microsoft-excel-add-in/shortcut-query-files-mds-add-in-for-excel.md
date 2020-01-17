---
title: ショートカット クエリ ファイル (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 1ba0219a-6c40-41fa-aff9-8c8f41ef3220
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3028682669ae1a7e33cb85847fbf6e9456c11d42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074388"
---
# <a name="shortcut-query-files-mds-add-in-for-excel"></a>ショートカット クエリ ファイル (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、よく使用するデータにすばやく接続して読み込むために、ショートカット クエリ ファイルを使用します。 MDS データを他のユーザーと共有する場合にも使用できます。 ワークシートを保存して電子メールで送信する代わりに、ショートカット クエリ ファイルを保存して電子メールで送信する必要があります。 これにより、両者が MDS リポジトリに接続して最新のデータを取得するようになります。  
  
 ショートカット クエリ ファイルは、次の情報を含む XML ファイルです。  
  
-   MDS リポジトリ接続。  
  
-   モデル、バージョン、およびエンティティ。  
  
-   ショートカットが作成されたときに適用されたフィルター。  
  
-   ショートカットが作成されたときの列の順序 (左から右)。  
  
 リストにこれらのファイルを保存し、アドインを開くときにその中から選択できます。 コンピューターまたは共有の場所にエクスポートするか、他のユーザーに送信することができます。  
  
 ショートカット クエリ ファイルを開くには、ファイルをインポートする方法と、ファイルをダブルクリックして QueryOpener アプリケーションで自動的に開く方法の 2 種類があります。  
  
## <a name="queryopener-application"></a>QueryOpener アプリケーション  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] をインストールすると、QueryOpener というアプリケーションが必ずインストールされます。 このアプリケーションを使用して、 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]でショートカット クエリ ファイルを開きます。 ショートカット クエリ ファイルをダブルクリックすると、このアプリケーションが自動的に使用され、アドインでファイルが開きます。  
  
 このアプリケーションでショートカット クエリ ファイルを開くときに、接続を "安全な" 接続にするように求めるメッセージが表示されます。これは、この場所からの内容を信頼することを意味します。 (プロンプト ウィンドウで **[このアドレスへの接続を常に許可する]** を選択すると、安全に接続できます。)接続を安全としてマークするたびに、接続がリストに追加されます。 このリストをクリアする場合は、 **[設定]** ダイアログ ボックスを開き、 **[セーフ リストに追加されたサーバー]** セクションで **[すべてクリア]** をクリックします。  
  
 アプリケーションの既定の場所は *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services\Excel Add-In\Microsoft.MasterDataServices.QueryOpener.exe です。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|アクティブなワークシートの内容をショートカット クエリ ファイルとして保存します。|[ショートカット クエリ ファイルの保存 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|アクティブなワークシートの内容を表すショートカット クエリ ファイルを電子メールで送信します。|[ショートカット クエリ ファイルの電子メールでの送信 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [接続 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel 用マスター データ サービス アドイン](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
-   [セキュリティ (マスター データ サービス)](../../master-data-services/security-master-data-services.md)  
  
  
