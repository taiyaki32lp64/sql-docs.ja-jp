---
title: 概要:(MDS アドインを Excel の) Excel にデータをエクスポートする |Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b628548b-982b-4e45-abf4-c8e83e3ab1c2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 75a23041a3e822ec103012aa18475a092b27b816
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074506"
---
# <a name="overview-exporting-data-to-excel-mds-add-in-for-excel"></a>概要:Excel へのデータのエクスポート (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、データを使用する前に、MDS リポジトリから Excel ワークシートにデータをエクスポートする必要があります。 データの操作が完了したら、そのデータを他のユーザーが共有できるように MDS リポジトリにインポートします。  
  
 エクスポートできるデータは、アクセスする権限があるデータに限定されます。 データにアクセスする権限は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションで設定するか、プログラムによって設定します。  
  
 大量のデータをエクスポートする場合は、読み込みに長時間かかる可能性があるデータのときに表示される警告を設定できます。 この操作を行うには、 **[オプション]** グループの **[設定]** をクリックします。 **[データ]** タブで、 **[大きなデータ セットの場合にフィルター警告を表示する]** を選択します。  
  
> [!WARNING]  
>  MDS が有効なブックは、Excel 用 MDS アドインを使用している Excel でのみ開き、更新する必要があります。 MDS Excel アドインがインストールされていないコンピューター上の Excel で、MDS が有効なブックを開くことはサポートされていませんし、ブック ファイルを破損する可能性があります。 他のユーザーとデータを共有したい場合は、ワークシートを保存して電子メールで送信するのではなく、ショートカット クエリ ファイルをそのユーザーに電子メールで送信します。 クエリの詳細については、「[ショートカット クエリ ファイルの電子メールでの送信 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="filtering-data"></a>データのフィルター処理  
 エクスポートする前にデータをフィルター処理して、ダウンロードするデータの量を制限できます。 これには、読み込む属性 (列)、属性を表示する順序、および使用するメンバー (データ行) の選択が含まれます。 詳細については、「 [エクスポート前のデータのフィルター処理 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)をクリックします。  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>自動接続とよく使用するデータの読み込み  
 常に同じサーバーに接続して同じデータ セットをエクスポートする場合は、接続およびフィルター情報を含むショートカット クエリ ファイルを作成できます。 クエリ ファイルの詳細については、「 [ショートカット クエリ ファイル (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)をクリックします。  
  
## <a name="refreshing-data"></a>データの更新  
 MDS リポジトリのデータは、エクスポートした後に他のユーザーによって更新される場合があります。 このようなデータを取得しても、MDS データ以外のデータに加えた変更は失われません。 詳細については、「[データの更新 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|Excel に読み込む前に MDS データをフィルター処理します。|[エクスポート前のデータのフィルター処理 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)|  
|MDS データを Excel に読み込みます。|[マスター データ サービスから Excel へのデータのエクスポート](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|データをダウンロードする前に列の順序を変更します。|[列の並べ替え (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [接続 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [ショートカット クエリ ファイル &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel 用マスター データ サービス アドイン](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
-   [セキュリティ (マスター データ サービス)](../../master-data-services/security-master-data-services.md)  
  
  
