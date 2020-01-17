---
title: 'レッスン 1: サンプル サブスクライバー データベースの作成 | Microsoft Docs'
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2aa2fefb5df874b08a34c4a7091d450afdfd4828
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62513164"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>レッスン 1 : サンプル サブスクライバー データベースの作成

この [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] のチュートリアル レッスンでは、小さな "サブスクライバー" データベースを作成して、データドリブン サブスクリプションに使用するサブスクリプション データを格納します。 サブスクリプションを処理するときに、レポート サーバーはこのデータを取得し、レポート出力のカスタマイズに使用します。 たとえば、データの行に特定の順序の数値を含めてフィルターに使用したり、レポートの生成時に、レポートのファイル形式を指定したりすることができます。  
  
このレッスンでは、[!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] を使用して SQL Server データベースを作成することを前提としています。  
  
### <a name="to-create-a-sample-subscriber-database"></a>サンプル サブスクライバー データベースを作成するには  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]を起動し、 [!INCLUDE[ssDEnoversion_md](../includes/ssdenoversion-md.md)]のインスタンスへの接続を開きます。  
  
2.  [データベース] を右クリックして **[新しいデータベース]** をクリックします。  
  
3.  [新しいデータベース] ダイアログ ボックスの **[データベース名]** に「 *Subscribers*」と入力します。 
4. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  ツール バーの **[新しいクエリ]** ボタンをクリックします。  
  
6.  次の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを空のクエリにコピーします。  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
7.  ツール バーの **[実行]** をクリックします。  
  
8.  SELECT ステートメントを使用して、3 行のデータがあることを確認します。 例: `select * from OrderInfo`  
  
## <a name="next-steps"></a>Next Steps  
+ 以上の操作で、レポートを配信し、各サブスクライバーごとにレポート出力を変えるサブスクリプション データを作成できました。 
+ 次に、格納された資格情報を使用するレポートのデータ ソースのプロパティを変更します。 
+ また、レポートのデザインを変更して、サブスクリプションがサブスクライバーのデータと共に使用するパラメーターを含めます。 [レッスン 2: レポート データ ソースのプロパティの変更](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  

## <a name="next-steps"></a>次の手順

[データ ドリブン サブスクリプションの作成](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[データベースの作成](../relational-databases/databases/create-a-database.md)  
[基本的なテーブル レポートの作成](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
