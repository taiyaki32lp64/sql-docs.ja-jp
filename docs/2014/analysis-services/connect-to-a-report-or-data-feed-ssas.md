---
title: レポートまたはデータフィードへの接続 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connreportdatafeed.f1
ms.assetid: e0ccfb0b-e646-4de8-b7da-f88c986c96e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7a8feb912a7987328afa06043b18586f6e9bb29
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70151828"
---
# <a name="connect-to-a-report-or-data-feed-ssas"></a>[レポートまたはデータ フィードへの接続] (SSAS)
  **テーブルのインポート ウィザード** のこのページを使用すると、データ フィードに接続できます。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]からウィザードにアクセスするには、 **[モデル]** メニューの **[データ ソースからのインポート]** をクリックします。  
  
## <a name="from-a-report"></a>レポートから  
 **接続の表示名**  
 データ フィード接続の表示名を入力します。  
  
 **[レポートのパス]**  
 データ フィードを生成する SQL Server Reporting Services レポートの URL が表示されます。 **[参照]** をクリックして、レポートの URL を指定します。  
  
 **[レポートの表示]** をクリックしてレポートを表示します。  
  
 **[参照]**  
 使用可能なレポートがある場所に移動します。  
  
 **詳細設定**  
 **[詳細プロパティの設定]** ダイアログ ボックスを使用して追加の接続プロパティを設定します。  
  
 **[接続テスト]**  
 現在の設定を使用して、データ ソースに対する接続の確立を試みます。 接続が正常に確立されたかどうかを示すメッセージが表示されます。  
  
## <a name="from-an-azure-datamarket-dataset"></a>Azure DataMarket データセットから  
 **接続の表示名**  
 データ フィード接続の表示名を入力します。  
  
 **データフィード URL**  
 Atom サービス ドキュメント (.atomsvc、.atom) への完全なパス、または単一のデータ フィードの URL を入力するか、 **[参照]** をクリックして Atom サービス ドキュメントを選択します。  
  
 **[参照]**  
 使用可能なレポートがある場所に移動します。  
  
 使用可能なデータセットを表示するには、 **[使用可能な Azure DataMarket データセットの表示]** をクリックします。  
  
 **アカウント キー**  
 Azure Marketplace データセットサブスクリプションへのアクセスに使用するアカウントキーを指定します。  
  
 **探す**  
 Windows Live アカウントに関連付けられたアカウント キーを検索します。  
  
 **アカウントキーを保存する**  
 暗号化されたアカウント キーをデータ接続と共に保存します。  
  
 **詳細設定**  
 **[詳細プロパティの設定]** ダイアログ ボックスを使用して追加の接続プロパティを設定します。  
  
 **[接続テスト]**  
 現在の設定を使用して、データ ソースに対する接続の確立を試みます。 接続が正常に確立されたかどうかを示すメッセージが表示されます。  
  
## <a name="from-other-feeds"></a>その他のフィードから  
 **接続の表示名**  
 データ フィード接続の表示名を入力します。  
  
 **データフィード URL**  
 Atom サービス ドキュメント (.atomsvc、.atom) への完全なパス、または単一のデータ フィードの URL を入力するか、 **[参照]** をクリックして Atom サービス ドキュメントを選択します。  
  
 **[すべてのフィード列を含める]** をクリックして、すべてのデータ フィード列をインポートするかどうかを指定します。  
  
 **[参照]**  
 使用可能なデータ フィードがある場所に移動します。  
  
 **詳細設定**  
 **[詳細プロパティの設定]** ダイアログ ボックスを使用して追加の接続プロパティを設定します。  
  
 **[接続テスト]**  
 現在の設定を使用して、データ ソースに対する接続の確立を試みます。 接続が正常に確立されたかどうかを示すメッセージが表示されます。  
  
  
