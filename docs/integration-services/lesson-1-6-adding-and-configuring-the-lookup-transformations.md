---
title: 手順 6:参照変換を追加し、構成する | Microsoft Docs
ms.custom: ''
ms.date: 03/19/2019
ms.prod: sql
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
author: chugugrace
ms.author: chugu
ms.reviewer: ''
ms.openlocfilehash: ac10ace82a38110d2038f95c3514aa8271d5b88c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283745"
---
# <a name="lesson-1-6-add-and-configure-the-lookup-transformations"></a>レッスン 1-6:参照変換を追加し、構成する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



ソース ファイルからデータを取り出すフラット ファイルを構成したら、**CurrencyKey** と **DateKey** の値を取得する際に必要な参照変換を定義します。 参照変換は、指定の入力列のデータを参照データセットの列に結合することにより、参照を実行します。 参照データセットは、既存のテーブル、既存のビュー、新しいテーブル、または SQL ステートメントの結果のいずれかになります。 このチュートリアルでは、参照変換は、OLE DB 接続マネージャーを使用して、参照データセットのソース データを含むデータベースに接続します。  
  
> [!NOTE]  
> 参照データセットを含むキャッシュに接続するように参照変換を構成することもできます。 詳細については、「[参照変換](../integration-services/data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
この実習では、次の 2 つの参照変換コンポーネントをパッケージに追加し、構成します。  
  
-   **DimCurrency** ディメンション テーブルの **CurrencyKey** 列の値を参照する変換。**CurrencyID** 列の値と一致する値をフラット ファイルから探します。  
  
-   **DimDate** ディメンション テーブルの **DateKey** 列の値を参照する変換。**CurrencyDate** 列の値と一致する値をフラット ファイルから探します。  
  
いずれの場合も、参照変換では、以前に作成した OLE DB 接続マネージャーを使用します。  
  
## <a name="add-and-configure-the-lookup-currency-key-transformation"></a>Lookup Currency Key 変換を追加し、構成する  
  
1.  **[SSIS ツールボックス]** で **[共通]** を展開し、 **[参照]** を **[データ フロー]** タブのデザイン画面にドラッグします。 **[参照]** を **[Extract Sample Currency Data]** ソースのすぐ下に置きます。  
  
2.  **[Extract Sample Currency Data]** フラット ファイル ソースを選択し、青色の矢印を、新しく追加した **[参照]** 変換までドラッグしてこの 2 つのコンポーネントを接続します。  
  
3.  **[データ フロー]** デザイン画面で、 **[参照]** 変換の **[参照]** を選択し、名前を「**Lookup Currency Key**」に変更します。  
  
4.  **Lookup Currency Key** 変換をダブルクリックし、**参照変換エディター**を表示します。  
  
5.  **[全般]** ページで、以下の選択を行います。  
  
    1.  **[フル キャッシュ]** を選択します。  
  
    2.  **[接続の種類]** 領域で、 **[OLE DB 接続マネージャー]** を選択します。  
  
6.  **[接続]** ページで、以下の選択を行います。  
  
    1.  **[OLE DB 接続マネージャー]** ダイアログ ボックスに、 **localhost.AdventureWorksDW2012** が表示されていることを確認します。  
  
    2.  **[SQL クエリの結果を使用する]** をクリックし、次の SQL ステートメントを入力するか貼り付けます。  
  
        ```sql
        SELECT * FROM [dbo].[DimCurrency]
        WHERE [CurrencyAlternateKey]
        IN ('ARS', 'AUD', 'BRL', 'CAD', 'CNY',
            'DEM', 'EUR', 'FRF', 'GBP', 'JPY',
            'MXN', 'SAR', 'USD', 'VEB')
        ```  
    3.  **[プレビュー]** を選択し、クエリ結果を検証します。
  
7.  **[列]** ページで、以下の選択を行います。  
  
    1.  **[使用できる入力列]** パネルの **[CurrencyID]** を **[使用できる参照列]** パネルにドラッグし、 **[CurrencyAlternateKey]** の上にドロップします。  
  
    2.  **[使用できる参照列]** ボックスの一覧で、 **[CurrencyKey]** の左側のチェック ボックスをオンにします。  
  
8.  **[OK]** を選択し、 **[データ フロー]** デザイン画面に戻ります。  
  
9. [Lookup Currency Key] 変換を右クリックし、 **[プロパティ]** を選択します。  
  
10. **[プロパティ]** ウィンドウで、 **[LocaleID]** プロパティが **[英語 (米国)]** に、 **[DefaultCodePage]** プロパティが **[1252]** に設定されていることを確認します。  
  
## <a name="add-and-configure-the-lookup-date-key-transformation"></a>Lookup Date Key 変換を追加し、構成する  
  
1.  **[SSIS ツールボックス]** で **[参照]** をクリックし、 **[データ フロー]** デザイン画面上にドラッグします。 この **[参照]** を **[Lookup Currency Key]** のすぐ下に置きます。  
  
2.  **[Lookup Currency Key]** 変換を選択し、青色の矢印を新しい **[参照]** 変換までドラッグし、この 2 つのコンポーネントを接続します。  
  
3.  **[入出力の選択]** ダイアログの **[出力]** ボックスの一覧で **[参照の一致出力]** を選択し、 **[OK]** を選択します。  
  
4.  **[データ フロー]** デザイン画面で、新しく追加した **[参照]** 変換の名前 **[参照]** を選択し、名前を「**Lookup Date Key**」に変更します。  
  
5.  **[Lookup Date Key]** 変換をダブルクリックします。  
  
6.  **[全般]** ページで、 **[部分キャッシュ]** を選択します。  
  
7.  **[接続]** ページで、以下の選択を行います。  
  
    1.  **[OLEDB 接続マネージャー]** ダイアログに、確実に **localhost.AdventureWorksDW2012** が表示されているようにします。  
  
    2.  **[テーブルまたはビューを使用]** ボックスで、 **[dbo].[DimDate]** を選択するか、入力します。  
  
8.  **[列]** ページで、以下の選択を行います。  
  
    1.  **[使用できる入力列]** パネルの **[CurrencyDate]** を **[使用できる参照列]** パネルにドラッグし、 **[FullDateAlternateKey]** の上にドロップします。  データ型の不一致を示すメッセージが表示された場合、CurrencyDate のデータ型を [DT_DBDATE] に変更してください。
  
    2.  **[使用できる参照列]** ボックスの一覧で、 **[DateKey]** の左側のチェック ボックスをオンにします。  
  
9. **[詳細設定]** ページで、キャッシュ オプションを確認します。  
  
10. **[OK]** を選択し、 **[データ フロー]** デザイン画面に戻ります。  
  
11. **[Lookup Date Key]** 変換を右クリックし、 **[プロパティ]** を選択します。
  
12. **[プロパティ]** ウィンドウで、 **[LocaleID]** プロパティが **[英語 (米国)]** に、 **[DefaultCodePage]** プロパティが **[1252]** に設定されていることを確認します。  
  
## <a name="go-to-next-task"></a>次の実習に進む
[手順 7:OLE DB 変換先を追加し、構成する](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>参照  
[参照変換](../integration-services/data-flow/transformations/lookup-transformation.md)  
