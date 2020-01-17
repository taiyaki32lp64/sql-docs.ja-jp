---
title: ライブラリ (PowerPivot for SharePoint) への BI セマンティック モデル接続のコンテンツ タイプの追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 145505ed-50bc-4528-912b-2a5cd2566011
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4712aba656fa111400e41566964cbd9719f778db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071971"
---
# <a name="add-a-bi-semantic-model-connection-content-type-to-a-library-powerpivot-for-sharepoint"></a>BI セマンティック モデル接続のコンテンツ タイプのライブラリへの追加 (PowerPivot for SharePoint)
  BI セマンティック モデル接続は、SharePoint で作成され、ネットワーク サーバー上の PowerPivot ブックまたは Analysis Services テーブル モデル データベース内の Business Intelligence Semantic Model データへのリダイレクトを可能にします。 SharePoint で BI セマンティック モデル接続を作成する前に、.bism ファイルの作成を許可するようにドキュメント ライブラリを拡張する必要があります。 この手順はライブラリごとに 1 回だけ実行する必要があり、.bism ファイルを作成するすべてのライブラリに対してこの手順を繰り返す必要があります。 ベスト プラクティスとして、権限を 1 か所で管理できるように、.bism ファイルを格納する単一のライブラリを作成することをお勧めします。  
  
> [!NOTE]  
>  既に SharePoint データ接続ライブラリを使用している場合、"BI セマンティック モデル接続" コンテンツ タイプがそのライブラリ テンプレートに自動的に追加されます。 既に新しい BI セマンティック モデル接続ドキュメントの作成が許可されているデータ接続ライブラリを使用する場合は、このセクションの手順を省略できます。  
  
##  <a name="bkmk_addtype"></a> ドキュメント ライブラリへのコンテンツ タイプの追加  
 コンテンツ タイプを追加および構成するには、管理リスト権限以上の権限が必要です。 この権限は、デザイン権限レベル以上の権限に組み込まれています。  
  
 ドキュメント ライブラリがあるサイトでは、PowerPivot for SharePoint の機能のアクティブ化が必要です。 詳細については、次を参照してください。 [PowerPivot 機能の統合サーバーの全体管理のサイト コレクション用にアクティブ化](activate-power-pivot-integration-for-site-collections-in-ca.md)します。  
  
1.  "BI セマンティック モデル接続" コンテンツ タイプを有効にする対象のドキュメント ライブラリを開きます。  
  
2.  SharePoint リボンで、[ライブラリ ツール] の **[ライブラリ]** をクリックします。  
  
3.  **[ライブラリの設定]** をクリックします。  
  
4.  [全般設定] の **[詳細設定]** をクリックします。  
  
5.  [コンテンツ タイプ] の [コンテンツ タイプの管理を許可する] セクションで **[はい]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
7.  [コンテンツ タイプ] セクションの **[既存のサイト コンテンツ タイプから追加]** をクリックします。 このページが表示されない場合は、サイトに戻って [ライブラリ ツール] の **[ライブラリ]** をクリックし、 **[ライブラリの設定]** をクリックします。  
  
8.  [コンテンツ タイプ] の **[既存のサイト コンテンツ タイプから追加]** をクリックします。  
  
9. [サイト コンテンツ タイプの選択元] で **[ビジネス インテリジェンス]** をクリックします。  
  
10. [利用可能なサイト コンテンツ タイプ] で **[BI セマンティック モデル接続ファイル]** をクリックしてから **[追加]** をクリックし、選択したコンテンツ タイプを [追加するコンテンツ タイプ] ボックスの一覧に追加します。  
  
11. **[OK]** をクリックします。  
  
12. コンテンツ タイプを追加したことを確認するには、ライブラリに戻り、ライブラリ リボンのドキュメント領域で **[新しいドキュメント]** をクリックします。 [新しいドキュメント] ボックスの一覧に、 **[BI セマンティック モデル接続ファイル]** が表示されます。  
  
     ![SharePoint ライブラリ内の新しいドキュメント サブメニュー](../media/ssas-bismconnection-new.gif "SharePoint ライブラリ内の新しいドキュメント サブメニュー")  
  
 "BI セマンティック モデル接続" コンテンツ タイプをライブラリに対して有効にした後で、Excel または [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] レポートで使用できるビジネス セマンティック モデル データへのリダイレクトを可能にする接続を作成できます。 次のステップの詳細については、次のリンクから選択してください。  
  
 [PowerPivot ブックへの BI セマンティック モデル接続の作成](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [テーブル モデル データベースへの BI セマンティック モデル接続の作成](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
## <a name="see-also"></a>参照  
 [PowerPivot BI セマンティック モデル接続&#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [Excel または Reporting Services での BI セマンティック モデル接続の使用](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
  
