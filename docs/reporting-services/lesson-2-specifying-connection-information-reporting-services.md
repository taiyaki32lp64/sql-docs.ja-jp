---
title: 'レッスン 2 : 接続情報の指定 (Reporting Services) | Microsoft Docs'
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a0c21b2662fc14977c4ac57687754d15d544994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106048"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>レッスン 2 : 接続情報の指定 (Reporting Services)

レッスン 1 で、[!INCLUDE[ssrsnoversion-md](../includes/ssrsnoversion-md.md)] のページ分割されたレポートを Tutorial プロジェクトに追加しました。
  
このレッスンでは、リレーショナル データベースやその他のリソースのデータにアクセスするためにレポートで使用される接続情報である*データ ソース*を定義する必要があります。

このレポートの場合、AdventureWorks2016 サンプル データベースをデータ ソースとして追加します。 このチュートリアルでは、このデータベースが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] の既定のインスタンスに配置されており、ローカル コンピューターにインストールされいるものとします。  

## <a name="to-set-up-a-connection"></a>接続を設定するには  

1. **[レポート データ]** ウィンドウで、 **[新規作成]**  >  **[データ ソース]** の順にクリックします。 **[レポート データ]** ウィンドウが表示されていない場合は、 **[表示]** メニュー > **[レポート データ]** の順に選択します。

    ![ssrs-table-tutorial-2-new-data-source](media/ssrs-table-tutorial-2-new-data-source.png)

    **[データ ソースのプロパティ]** ダイアログ ボックスが開き、 **[全般]** セクションが表示されます。

    ![[データ ソースのプロパティ] ダイアログ ボックス](media/lesson-2-specifying-connection-information-reporting-services/vs-datasource-connection-properties-dialog-box.png)

2. **[名前]** ボックスに「AdventureWorks2016」と入力します。

3. **[埋め込み接続]** を選択します。

4. **[種類]** ボックスで、[Microsoft SQL Server] を選択します。
  
5. **[接続文字列]** ボックスで、次の文字列を入力します。

    `Data source=localhost; initial catalog=AdventureWorks2016`

    > [!NOTE]
    > この接続文字列は、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、レポート サーバー、および AdventureWorks2016 データベースがすべてローカル コンピューターにインストールされていることが前提となります。
    >
    >この前提が成り立っていない場合、接続文字列を変更し、"localhost" をデータベース サーバー/インスタンスの名前に置き換えます。 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] または SQL Server の名前付きインスタンスを使用している場合、接続文字列を変更してインスタンス情報を含める必要があります。 例:
    >
    > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2016`
    >
    > 接続文字列の詳細については、以下の「`See also`」セクションを参照してください。

6. **[資格情報]** タブを選択し、 **[データ ソースに接続するための資格情報を変更します。]** セクションの下で **[Windows 認証 (統合セキュリティ) を使用する ]** を選択します。

7. **[OK]** を選択して処理を完了します。

レポート デザイナーにより、データソース AdventureWorks2016 が **[レポート データ]** ウィンドウに追加されます。

![ssrs-adventureworks-datasource](media/lesson-2-specifying-connection-information-reporting-services/ssrs-adventureworks-datasource2016.png)

## <a name="next-steps"></a>次の手順

このレッスンでは、AdventureWorks2016 サンプル データベースへの接続を正常に定義しました。 「[レッスン 3: テーブル レポートのデータセットの定義 &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)」に進み、レポートのデータセットを定義します。

## <a name="see-also"></a>参照

[Reporting Services でのデータ接続、データ ソース、および接続文字列](report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)
