---
title: (MDS アドインを Excel の) データの読み込み |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b628548b-982b-4e45-abf4-c8e83e3ab1c2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3bbd3ac1bf97530d64760d1434b9e7e8f6a81d34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482798"
---
# <a name="loading-data-mds-add-in-for-excel"></a>データの読み込み (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]、する必要がありますにデータを読み込む、MDS リポジトリから Excel ワークシートを使用する前にします。 データの操作が完了したら、そのデータを他のユーザーが共有できるように MDS リポジトリにパブリッシュします。  
  
 読み込むことができるデータは、アクセスする権限があるデータに限定されます。 データにアクセスする権限は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションで設定するか、プログラムによって設定します。  
  
 大量のデータを読み込む場合は、読み込みに長時間かかる可能性があるデータのときに表示される警告を設定できます。 この操作を行うには、 **[オプション]** グループの **[設定]** をクリックします。 **[データ]** タブで、 **[大きなデータ セットの場合にフィルター警告を表示する]** を選択します。  
  
> [!WARNING]  
>  MDS が有効なブックは、Excel 用 MDS アドインを使用している Excel でのみ開き、更新する必要があります。 MDS Excel アドインがインストールされていないコンピューター上の Excel で、MDS が有効なブックを開くことはサポートされていませんし、ブック ファイルを破損する可能性があります。 他のユーザーとデータを共有したい場合は、ワークシートを保存して電子メールで送信するのではなく、ショートカット クエリ ファイルをそのユーザーに電子メールで送信します。 クエリの詳細については、「[ショートカット クエリ ファイルの電子メールでの送信 (Excel 用 MDS アドイン)](email-a-shortcut-query-file-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="filtering-data"></a>データのフィルター処理  
 ダウンロードしようとしているデータの量を制限するを読み込む前にデータをフィルター処理できます。 これには、読み込む属性 (列)、属性を表示する順序、および使用するメンバー (データ行) の選択が含まれます。 詳細については、次を参照してください。[読み込み前にデータのフィルター選択&#40;MDS アドインの Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)します。  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>自動接続とよく使用するデータの読み込み  
 常に同じサーバーに接続して同じデータ セットを読み込む場合は、接続およびフィルター情報を含むショートカット クエリ ファイルを作成できます。 クエリ ファイルの詳細については、「[ショートカット クエリ ファイル (Excel 用 MDS アドイン)](shortcut-query-files-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="refreshing-data"></a>データの更新  
 MDS リポジトリのデータは、読み込んだ後に他のユーザーによって更新される場合があります。 このようなデータを取得しても、MDS データ以外のデータに加えた変更は失われません。 詳細については、「[データの更新 (Excel 用 MDS アドイン)](refreshing-data-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|Excel に読み込む前に MDS データをフィルター処理します。|[読み込み前にデータをフィルター処理&#40;MDS アドインの Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)|  
|MDS データを Excel に読み込みます。|[MDS から Excel へのデータの読み込み](export-data-to-excel-from-master-data-services.md)|  
|データをダウンロードする前に列の順序を変更します。|[列の並べ替え (Excel 用 MDS アドイン)](reorder-columns-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [接続 (Excel 用 MDS アドイン)](connections-mds-add-in-for-excel.md)  
  
-   [ショートカット クエリ ファイル &#40;Excel 用 MDS アドイン&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel 用マスター データ サービス アドイン](master-data-services-add-in-for-microsoft-excel.md)  
  
-   [セキュリティ (マスター データ サービス)](../security-master-data-services.md)  
  
  
