---
title: DQS クレンジング変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssdqs.designer.cleansing.f1
- sql13.SSDQS.DESIGNER.DQCONNECTION.F1
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1c3ccadbe443ca555e5386ea3d3434405ae97461
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291478"
---
# <a name="dqs-cleansing-transformation"></a>DQS クレンジング変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  DQS クレンジング変換では、Data Quality Services (DQS) を使用して、接続されたデータ ソースまたは類似のデータ ソース用に作成された承認済みのルールを適用することにより、接続されたデータ ソースのデータを修正します。 データ修正ルールの詳細については、「 [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)」を参照してください。 DQS の詳細については、「 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)」を参照してください。  
  
 データを修正する必要があるかどうかを判断するために、DQS クレンジング変換は、次の条件が当てはまる場合に、入力列のデータを処理します。  
  
-   データ修正のために列が選択されている。  
  
-   列のデータ型でデータ修正がサポートされている。  
  
-   列が、互換性のあるデータ型のドメインにマップされている。  
  
 また、変換には、低レベルのエラーを処理するように構成するエラー出力も含まれます。 エラー出力を構成するには、 **DQS クレンジング変換エディター**を使用します。  
  
 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) をデータ フローに含めて、重複部分と考えられるデータ行を特定することができます。  
  
## <a name="data-quality-projects-and-values"></a>データ品質プロジェクトと値  
 DQS クレンジング変換によってデータを処理すると、クレンジング プロジェクトが Data Quality Server に作成されます。 データ品質クライアントを使用してプロジェクトを管理します。 また、データ品質クライアントを使用して、プロジェクトの値を DQS のナレッジ ベースのドメインにインポートできます。 値は、DQS クレンジング変換で使用するように構成されているドメイン (またはリンク ドメイン) にしかインポートできません。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Data Quality Client で Integration Services プロジェクトを開く](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Import Cleansing Project Values into a Domain](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [データ ソースにデータ品質ルールを適用する](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [データ品質プロジェクトを開く、ロックを解除する、名前を変更する、削除する](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   social.technet.microsoft.com の記事「 [複合ドメインを使用した複雑なデータのクレンジング](https://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)」  
  
## <a name="dqs-cleansing-transformation-editor-dialog-box"></a>[DQS クレンジング変換エディター] ダイアログ ボックス
  **[DQS クレンジング変換エディター]** ダイアログ ボックスを使用すると、Data Quality Services (DQS) を使用してデータを修正できます。 詳細については、「 [Data Quality Services の概念](../../../data-quality-services/data-quality-services-concepts.md)」を参照してください。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [DQS クレンジング変換エディターを開く](#open)  
  
-   [[接続マネージャー] タブのオプションの設定](#connection)  
  
-   [[マッピング] タブのオプションの設定](#mapping)  
  
-   [[詳細設定] タブのオプションの設定](#advanced)  
  
-   [[DQS クレンジング接続マネージャー] ダイアログ ボックスのオプションの設定](#manager)  
  
###  <a name="open"></a> DQS クレンジング変換エディターを開く  
  
1.  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] で、DQS クレンジング変換を [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]パッケージに追加します。  
  
2.  コンポーネントを右クリックし、 **[編集]** をクリックします。  
  
###  <a name="connection"></a> [接続マネージャー] タブのオプションの設定  
 **[データ品質接続マネージャー]**  
 既存の DQS 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[DQS クレンジング接続マネージャー]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。 「 [[DQS クレンジング接続マネージャー] ダイアログ ボックスのオプションの設定](#manager)」を参照してください。  
  
 **[データ品質ナレッジ ベース]**  
 接続されたデータ ソースの既存の DQS ナレッジ ベースを選択します。 DQS サポート技術情報の詳細については、「 [DQS のナレッジ ベースとドメイン](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)」を参照してください。  
  
 **[暗号化接続]**  
 DQS サーバーと [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] の間のデータ転送を暗号化するために、接続を暗号化するかどうかを指定します。  
  
 **[使用できるドメイン]**  
 選択されたナレッジ ベースで使用できるドメインを一覧表示します。 ドメインには、単一ドメインと、2 つ以上の単一ドメインが含まれた複合ドメインの 2 種類があります。  
  
 複合ドメインに列をマップする方法については、「 [複合ドメインへの列のマップ](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md)」を参照してください。  
  
 ドメインの詳細については、「 [DQS のナレッジ ベースとドメイン](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)」を参照してください。  
  
 **エラー出力の構成**  
 行レベルのエラーを処理する方法を指定します。 接続されたデータ ソースのデータを変換で修正する際には、予期しないデータ値や検証制約が原因でエラーが発生することがあります。  
  
 有効な値は次のとおりです。  
  
-   **[エラー コンポーネント]** : 変換に失敗したこと、およびデータが Data Quality Services データベースに挿入されていないことを示します。 これが既定値です。  
  
-   **[行のリダイレクト]** : 入力データが Data Quality Services データベースに挿入されていないために、エラー出力にリダイレクトされることを示します。  
  
###  <a name="mapping"></a> [マッピング] タブのオプションの設定  
 複合ドメインに列をマップする方法については、「 [複合ドメインへの列のマップ](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md)」を参照してください。  
  
 **使用できる入力列**  
 接続されたデータ ソースの列を一覧表示します。 修正するデータを含む 1 つまたは複数の列を選択します。  
  
 **入力列**  
 **[使用できる入力列]** 領域で選択した入力列を一覧表示します。  
  
 **[ドメイン]**  
 入力列にマップするドメインを選択します。  
  
 **[ソースの別名]**  
 元の列値を含むソース列を一覧表示します。  
  
 列名を変更するフィールドをクリックしてください。  
  
 **[出力の別名]**  
 **DQS クレンジング変換**によって出力された列を一覧表示します。 この列には、元の列値または修正後の値が含まれます。  
  
 列名を変更するフィールドをクリックしてください。  
  
 **[状態の別名]**  
 修正されたデータの状態情報を含む列を一覧表示します。 列名を変更するフィールドをクリックしてください。  
  
###  <a name="advanced"></a> [詳細設定] タブのオプションの設定  
 **[出力の標準化]**  
 ドメインで定義されている出力形式に基づいて標準化された形式でデータを出力するかどうかを示します。 標準化された形式の詳細については、「 [データ クレンジング](../../../data-quality-services/data-cleansing.md)」を参照してください。  
  
 **[信頼度]**  
 修正されたデータの信頼レベルを含めるかどうかを示します。 信頼レベルは、DQS の修正または候補に対する確実性の度合いを示します。 信頼レベルの詳細については、「 [データ クレンジング](../../../data-quality-services/data-cleansing.md)」を参照してください。  
  
 **Reason**  
 データ修正の理由を含めるかどうかを示します。  
  
 **[追加されたデータ]**  
 既存の参照データ プロバイダーから取得した追加データを出力するかどうかを示します。 詳細については、「 [Reference Data Services in DQS](../../../data-quality-services/reference-data-services-in-dqs.md)」をご覧ください。  
  
 **[追加されたデータ スキーマ]**  
 データ スキーマを出力するかどうかを示します。 詳細については、「 [参照データへのドメインまたは複合ドメインのアタッチ](../../../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)」を参照してください。  
  
###  <a name="manager"></a> [DQS クレンジング接続マネージャー] ダイアログ ボックスのオプションの設定  
 **サーバー名**  
 接続先の DQS サーバーの名前を選択または入力します。 サーバーの詳細については、「 [DQS 管理](../../../data-quality-services/dqs-administration.md)」を参照してください。  
  
 **[接続テスト]**  
 クリックすると、指定した接続が利用可能であることを確認できます。  
  
 次の方法で、接続領域から **[DQS クレンジング接続マネージャー]** ダイアログ ボックスを開くこともできます。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、既存の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開くか、新しいプロジェクトを作成します。  
  
2.  接続領域内を右クリックし、 **[新しい接続]** をクリックして、 **[DQS]** をクリックします。  
  
3.  **[追加]** をクリックします。  
  
