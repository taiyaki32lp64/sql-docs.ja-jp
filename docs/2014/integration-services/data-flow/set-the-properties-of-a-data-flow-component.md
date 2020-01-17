---
title: データ フロー コンポーネントのプロパティを設定する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc360da93b905bed20f118812898b5c029c570cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770748"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>データ フロー コンポーネントのプロパティを設定する
  変換元、変換先、変換などを含むデータ フロー コンポーネントのプロパティを設定するには、次の機能のいずれかを使用します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が提供するコンポーネント エディター。 これらのエディターには、各データ フロー コンポーネントのカスタム プロパティのみ含まれます。  
  
-   **[プロパティ]** ウィンドウでは、各要素のコンポーネントレベルのカスタム プロパティ、およびすべてのデータ フロー要素との共通プロパティの一覧が表示されます。  
  
-   **[詳細エディター]** ダイアログ ボックスでは、各コンポーネントのカスタム プロパティにアクセスできます。 また、 **[詳細エディター]** ダイアログ ボックスを使用すると、すべてのデータ フロー コンポーネントの共通プロパティである、入力、出力、エラー出力、列、および外部列のプロパティにもアクセスできます。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-a-component-editor"></a>コンポーネント エディターを使用してデータ フロー コンポーネントのプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、プロパティを表示して変更するコンポーネントのあるデータ フローが含まれる、データ フロー タスクをダブルクリックします。  
  
4.  データ フロー コンポーネントをダブルクリックします。  
  
5.  コンポーネント エディターで、プロパティ値を表示または変更し、エディターを閉じます。  
  
6.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-properties-window"></a>[プロパティ] ウィンドウを使用してデータ フロー コンポーネントのプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、プロパティを表示して変更するコンポーネントが含まれているデータ フロー タスクをダブルクリックします。  
  
4.  データ フロー コンポーネントを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  プロパティ値を表示または変更し、 **[プロパティ]** ウィンドウを閉じます。  
  
    > [!NOTE]  
    >  プロパティの多くは読み取り専用であり、変更できません。  
  
6.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-advanced-editor"></a>詳細エディターを使用してデータ フロー コンポーネントのプロパティを設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックし、表示または変更するコンポーネントが含まれているデータ フロー タスクをダブルクリックします。  
  
4.  データ フロー デザイナーで、データ フロー コンポーネントを右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、複数の入力をサポートするデータ フロー コンポーネントで **[詳細エディター]** を使用できません。  
  
5.  **[詳細エディター]** ダイアログ ボックスで、次のいずれかの手順を実行します。  
  
    -   コンポーネントで使用する接続を表示および指定するには、 **[接続マネージャー]** タブをクリックします。  
  
        > [!NOTE]  
        >  **[接続マネージャー]** タブは、接続マネージャーを使用してファイルやデータベースなどのデータ ソースに接続するデータ フロー コンポーネントのみで使用できます。  
  
    -   コンポーネント レベルのプロパティを表示および変更するには、 **[コンポーネントのプロパティ]** タブをクリックします。  
  
    -   外部列と使用できる出力との間のマッピングを表示および変更するには、 **[列マッピング]** タブをクリックします。  
  
        > [!NOTE]  
        >  **[列マッピング]** タブは、変換元または変換先を表示または編集するときにのみ使用できます。  
  
    -   使用できる入力列の一覧を表示して、出力列の名前を更新するには、 **[入力列]** タブをクリックします。  
  
        > [!NOTE]  
        >  [入力列] タブは、変換または変換先を使用した作業でのみ使用できます。 詳細については、「 [Integration Services の変換](transformations/integration-services-transformations.md)」を参照してください。  
  
    -   入力、出力、およびエラー出力のプロパティや、列自体のプロパティを表示および変更するには、 **[入力プロパティと出力プロパティ]** タブをクリックします。  
  
        > [!NOTE]  
        >  変換元には入力はありません。 変換先には出力はありません。ただし、オプションのエラー出力がある場合があります。  
  
6.  プロパティ値を表示または変更します。  
  
7.  **[OK]** をクリックします。  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services の変換](transformations/integration-services-transformations.md)  
  
  
