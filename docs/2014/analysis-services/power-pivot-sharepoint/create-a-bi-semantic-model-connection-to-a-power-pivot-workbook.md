---
title: PowerPivot ブックへの BI セマンティック モデル接続の作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b2e3f97f-18a8-42b6-9030-b4f818afc3b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f525c45e71c290d3eaab410c0fa0fa62d1e9a61d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071643"
---
# <a name="create-a-bi-semantic-model-connection-to-a-powerpivot-workbook"></a>PowerPivot ブックへの BI セマンティック モデル接続の作成
  このトピックでは、同一ファーム内の PowerPivot ブックにリダイレクトする BI セマンティック モデル接続を設定する方法について説明します。  
  
 BI セマンティック モデル接続を作成して SharePoint 権限を構成したら、その接続を Excel または [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] レポートのデータ ソースとして使用できます。  
  
 このトピックのセクションは次のとおりです。 各タスクは、所定の順序で実行してください。  
  
 [前提条件の確認](#bkmk_prereq)  
  
 [接続の作成](#bkmk_create)  
  
 [BI セマンティック モデル接続への SharePoint 権限の構成](#bkmk_permissions)  
  
 [ブックへの SharePoint 権限の構成](#bkmk_userdb)  
  
 [次の手順](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> 前提条件の確認  
 BI セマンティック モデル接続ファイルを作成するには、投稿権限以上の権限が必要です。  
  
 BI セマンティック モデル接続のコンテンツ タイプをサポートしているライブラリが必要です。 詳細については、次を参照してください。 [BI セマンティック モデル接続のコンテンツ タイプをライブラリに追加&#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)します。  
  
 BI セマンティック モデル接続を設定する対象の PowerPivot ブックの URL を把握する必要があります (たとえば、 http://adventure-works/shared documents/myworkbook.xlsx)。 ブックは、同一ファーム内にある必要があります。  
  
 接続シーケンスに参加しているすべてのコンピューターとユーザーは、同じドメインまたは信頼されたドメイン (双方向の信頼関係) に属している必要があります。  
  
##  <a name="bkmk_create"></a> 接続の作成  
  
1.  BI セマンティック モデル接続の格納先となるライブラリで、SharePoint リボンの **[ドキュメント]** をクリックします。 [新しいドキュメント] の下矢印をクリックし、 **[BISM 接続ファイル]** を選択して、[新しい BI セマンティック モデル接続] ページを開きます。  
  
     ![SharePoint ライブラリ内の新しいドキュメント サブメニュー](../media/ssas-bismconnection-new.gif "SharePoint ライブラリ内の新しいドキュメント サブメニュー")  
  
2.  設定、 **Server**プロパティに、PowerPivot ブックの SharePoint URL (たとえば、  **http://mysharepoint/shared documents/myWorkbook.xlsx**します。 PowerPivot for SharePoint の配置では、ファーム内の任意のサーバーにデータを読み込むことができます。 このため、PowerPivot データへのデータ ソース接続では、ブックへのパスだけを指定します。 PowerPivot System サービスによって、データを読み込むサーバーが決定されます。  
  
     使用しないでください、**データベース**プロパティは、PowerPivot ブックの場所を指定する場合は使用しません。  
  
     ページは次の図のようになります。  
  
     ![ブックへの URL を示す BISM 接続ページ](../media/ssas-bismconnection-ppvtds.gif "ブックへの URL を示す BISM 接続ページ")  
  
     ブックに対する SharePoint 権限を持っている場合は、必要に応じて、その場所が有効であるかどうかを確認するための追加の検証手順が実行されます。 データへのアクセス権限がない場合は、検証の応答なしで BI セマンティック モデル接続を保存するオプションが表示されます。  
  
##  <a name="bkmk_permissions"></a> BI セマンティック モデル接続への SharePoint 権限の構成  
 BI セマンティック モデル接続を Excel ブックまたは Reporting Services レポートのデータ ソースとして使用するには、SharePoint ライブラリ内の BI セマンティック モデル接続アイテムに対する **読み取り** 権限が必要です。 読み取り権限レベルには、BI セマンティック モデル接続情報を Excel デスクトップ アプリケーションにダウンロードできるようにする **"アイテムを開く"** 権限が含まれます。  
  
 SharePoint で権限を付与するには、いくつかの方法があります。 次の手順では、 **読み取り** 権限レベルを持つ、 **BISM ユーザー** という名前の新しいグループを作成する方法について説明します。  
  
 権限を変更するには、サイト所有者である必要があります。  
  
1.  [サイトの操作] の **[サイトの権限]** をクリックします。  
  
2.  **[グループの作成]** をクリックして、新しいグループの名前を「 **BISM ユーザー**」と指定します。  
  
3.  **[読み取り]** 権限レベルを選択し、 **[作成]** をクリックします。  
  
4.  [ユーザーとグループ] の **[BISM ユーザー]** を選択します。  
  
5.  [新規作成] をポイントして **[ユーザーの追加]** をクリックし、ユーザー アカウントまたはグループ アカウントを追加します。  
  
     これで、追加したユーザーおよびグループに、サイト レベルから権限を継承するすべてのライブラリとリストを含むサイト全体の読み取り権限が付与されます。 この権限レベルでは高すぎる場合は、必要に応じて特定のライブラリ、リスト、またはアイテムからこのグループを削除できます。  
  
 アイテム レベルで権限を選択的に削除するには、次の操作を行います。  
  
1.  ライブラリで、ドキュメントを選択します。 右側の下矢印をクリックし、 **[権限の管理]** をクリックします。  
  
2.  既定では、アイテムは権限を継承します。 このライブラリ内の個々のドキュメントの権限を変更するには、 **[権限の継承を中止]** をクリックします。  
  
3.  **[BISM ユーザー]** の横にあるチェック ボックスをオンにします。  
  
4.  **[ユーザー権限の削除]** をクリックします。  
  
##  <a name="bkmk_userdb"></a> ブックへの SharePoint 権限の構成  
 Excel ブック内で PowerPivot データベースを使用している場合、BI セマンティック モデル接続を介したデータ アクセスは Excel ブックに対する SharePoint 権限によって決まります。 ブックを外部データ ソースとして使用するには、ブックにアクセスするすべてのユーザーにブックに対する読み取り権限が必要です。  
  
 前のセクションの手順に従って **[BISM ユーザー]** グループを作成した場合は、継承された権限をブックで使用すると想定して、ブックおよび BI セマンティック モデル接続ファイルに対する十分な権限が、 **BISM ユーザー** のメンバーであるユーザー アカウントとグループ アカウントに付与されます。  
  
##  <a name="bkmk_next"></a> 次の手順  
 BI セマンティック モデル接続を作成し、セキュリティで保護したら、データ ソースとして指定できます。 詳細については、「 [Excel または Reporting Services での BI セマンティック モデル接続の使用](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [PowerPivot BI セマンティック モデル接続&#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [Excel または Reporting Services での BI セマンティック モデル接続の使用](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)   
 [テーブル モデル データベースへの BI セマンティック モデル接続の作成](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
  
