---
title: Date ディメンションの変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4689d780-4bf6-4cf8-8fde-eb3f15dd668a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 826d5b1079e9fcfd0d2ec7a9abd55937f2da1a22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078799"
---
# <a name="modifying-the-date-dimension"></a>Date ディメンションの変更
  このトピックの実習では、ユーザー定義階層を作成し、Date、Month、Calendar Quarter、および Calendar Semester 属性に表示されるメンバー名を変更します。 また、属性の複合キーの定義、ディメンション メンバーの並べ替え順序の制御、および属性リレーションシップの定義も行います。  
  
## <a name="adding-a-named-calculation"></a>名前付き計算の追加  
 名前付き計算 (計算列として表される SQL 式) をデータ ソース ビューに追加できます。 この式は、テーブルの列として表示され、動作します。 名前付き計算を使用すると、基になるデータ ソースのテーブルを変更せずに、データ ソース ビュー内の既存のテーブルのリレーショナル スキーマを拡張できます。 詳細については、「 [データ ソース ビューでの名前付き計算の定義 (Analysis Services)](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>名前付き計算を追加するには  
  
1.  **Adventure Works DW 2012** データ ソース ビューを開くには、ソリューション エクスプローラーの **[データ ソース ビュー]** フォルダーでこのデータ ソース ビューをダブルクリックします。  
  
2.  一番下近く、**テーブル**ウィンドウで、右クリック`Date`、順にクリックします**新しい名前付き計算**します。  
  
3.  **名前付き計算の作成**ダイアログ ボックスに「`SimpleDate`で、**列名**ボックスに、入力またはコピーして貼り付け、次`DATENAME`内のステートメント、**式**ボックス。  
  
    ```  
    DATENAME(mm, FullDateAlternateKey) + ' ' +  
    DATENAME(dd, FullDateAlternateKey) + ', ' +  
    DATENAME(yy, FullDateAlternateKey)  
    ```  
  
     この `DATENAME` ステートメントは、FullDateAlternateKey 列から年、月、および日付の値を取得します。 この新しい列を、FullDateAlternateKey 属性の表示名として使用します。  
  
4.  をクリックして**OK**、順に展開`Date`で、**テーブル**ウィンドウ。  
  
     `SimpleDate`名前付き計算が Date テーブル内の列の一覧に表示されることを示すアイコンが表示されたが名前付き計算します。  
  
5.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
6.  **テーブル**ウィンドウで、右クリック`Date`、 をクリックし、**データの探索**。  
  
7.  **[Date テーブルの探索]** ビューで、右にスクロールして最後の列を確認します。  
  
     なお、`SimpleDate`元のデータ ソースを変更することがなくデータを基になるデータ ソースから複数の列を連結正しく列、データ ソース ビューに表示されます。  
  
8.  **[Date テーブルの探索]** ビューを閉じます。  
  
## <a name="using-the-named-calculation-for-member-names"></a>メンバー名に対応する名前付き計算の使用  
 データ ソース ビューで名前付き計算を作成したら、その名前付き計算を属性のプロパティとして使用できます。  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>メンバー名に対応する名前付き計算を使用するには  
  
1.  **で Date ディメンションの** ディメンション デザイナー [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を開きます。 これを行うには、ダブルクリック、`Date`ディメンション、**ディメンション**のノード**ソリューション エクスプ ローラー**します。  
  
2.  **[ディメンション構造]** タブの **[属性]** ペインで、 **[Date Key]** 属性をクリックします。  
  
3.  [プロパティ] ウィンドウが開いていない場合は、[プロパティ] ウィンドウを開き、タイトル バーにある **[自動的に隠す]** ボタンをクリックします。これにより、[プロパティ] ウィンドウが開いたままになります。  
  
4.  をクリックして、 **NameColumn**プロパティは、ウィンドウの下部にあるフィールドし、参照ボタンをクリックし ( **.** ) ボタンをクリックする、**名前列** ダイアログ ボックス。  
  
5.  選択`SimpleDate`の下部にある、**基になる列**ボックスの一覧をクリックして**OK**。  
  
6.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="creating-a-hierarchy"></a>階層の作成  
 新しい階層は、属性を **[属性]** ペインから **[階層]** ペインにドラッグすることで作成できます。  
  
#### <a name="to-create-a-hierarchy"></a>階層を作成するには  
  
1.  **ディメンション構造**ディメンションのディメンション デザイナーのタブ、`Date`ディメンションには、ドラッグ、**暦年**属性を**属性**ペイン、**階層**ウィンドウ。  
  
2.  ドラッグ、 **Calendar Semester**属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層** ウィンドウで、下、**暦年**レベル。  
  
3.  ドラッグ、 **Calendar Quarter**属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層** ウィンドウで、下、 **Calendar Semester**レベル。  
  
4.  ドラッグ、 **English Month Name**属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層** ウィンドウで、下、 **Calendar Quarter**レベル。  
  
5.  ドラッグ、 **Date Key**属性を**属性**ペイン、 **\<新しいレベル >** セル、**階層**ウィンドウ、の下に、 **English Month Name**レベル。  
  
6.  **階層**ウィンドウのタイトル バーを右クリックし、**階層**階層、 をクリックして**の名前を変更**、し、入力`Calendar Date`。  
  
7.  右クリック コンテキスト メニューを使用して、`Calendar Date`階層の名前を変更、 **English Month Name**レベルを`Calendar Month`、名前を変更し、 **Date Key**レベルを`Date`。  
  
8.  **Full Date Alternate Key** 属性はもう使用しないので、 **[属性]** ペインからこの属性を削除します。 **[オブジェクトの削除]** 確認ウィンドウで、 **[OK]** をクリックします。  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-attribute-relationships"></a>属性リレーションシップの定義  
 基になるデータで属性リレーションシップがサポートされる場合、属性間の属性リレーションシップを定義する必要があります。 属性リレーションシップを定義すると、ディメンション、パーティション、およびクエリの処理速度が上がります。  
  
#### <a name="to-define-attribute-relationships"></a>属性リレーションシップを定義するには  
  
1.  **ディメンション デザイナー**の`Date`ディメンションをクリックして、**属性リレーションシップ**タブ。  
  
2.  ダイアグラムで、 **[English Month Name]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
3.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[English Month Name]** を指定します。 **[関連属性]** を **[Calendar Quarter]** に設定します。  
  
4.  **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
     リレーションシップの種類を **[固定]** に設定するのは、時間が経過してもメンバー間のリレーションシップが変化しないためです。  
  
5.  **[OK]** をクリックします。  
  
6.  ダイアグラムで、 **[Calendar Quarter]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
7.  **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Calendar Quarter]** を指定します。 **[関連属性]** を **[Calendar Semester]** に設定します。  
  
8.  **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
9. **[OK]** をクリックします。  
  
10. ダイアグラムで、 **[Calendar Semester]** 属性を右クリックし、 **[新しい属性リレーションシップ]** をクリックします。  
  
11. **[属性リレーションシップの作成]** ダイアログ ボックスで、 **[基になる属性]** に **[Calendar Semester]** を指定します。 **[関連属性]** を **[Calendar Year]** に設定します。  
  
12. **[リレーションシップの種類]** ボックスの一覧で、リレーションシップの種類を **[固定]** に設定します。  
  
13. **[OK]** をクリックします。  
  
14. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="providing-unique-dimension-member-names"></a>一意なディメンション メンバー名の指定  
 この実習では、 **EnglishMonthName**、 **CalendarQuarter**、および **CalendarSemester** 属性で使用する表示名の列を作成します。  
  
#### <a name="to-provide-unique-dimension-member-names"></a>一意なディメンション メンバー名を指定するには  
  
1.  **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** データ ソース ビューに切り替えるには、ソリューション エクスプローラーの **[データ ソース ビュー]** フォルダーでこのデータ ソース ビューをダブルクリックします。  
  
2.  **テーブル**ウィンドウで、右クリックして`Date`、順にクリックします**新しい名前付き計算**します。  
  
3.  **名前付き計算の作成**ダイアログ ボックスに「`MonthName`で、**列名**ボックス、入力またはコピーして貼り付け次のステートメント、**式**ボックス:  
  
    ```  
    EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)  
    ```  
  
     このステートメントは、テーブルの各月に表示されている月と年度を連結し、連結した名前を新しい列に表示します。  
  
4.  **[OK]** をクリックします。  
  
5.  **テーブル**ウィンドウで、右クリックして`Date`、順にクリックします**新しい名前付き計算**します。  
  
6.  **名前付き計算の作成**ダイアログ ボックスに「`CalendarQuarterDesc`で、**列名**ボックスに、入力またはコピーして貼り付け、次の SQL スクリプト、**式**ボックス:  
  
    ```  
    'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY ' +  
    CONVERT(CHAR (4), CalendarYear)  
    ```  
  
     この SQL スクリプトは、テーブルの各四半期に表示されている四半期と年度を連結し、連結した名前を新しい列に表示します。  
  
7.  **[OK]** をクリックします。  
  
8.  **テーブル**ウィンドウで、右クリックして`Date`、順にクリックします**新しい名前付き計算**します。  
  
9. **名前付き計算の作成**ダイアログ ボックスに「`CalendarSemesterDesc`で、**列名**ボックスに、入力またはコピーして貼り付け、次の SQL スクリプト、**式**ボックス:  
  
    ```  
    CASE  
    WHEN CalendarSemester = 1 THEN 'H1' + ' ' + 'CY' + ' '   
           + CONVERT(CHAR(4), CalendarYear)  
    ELSE  
    'H2' + ' ' + 'CY' + ' ' + CONVERT(CHAR(4), CalendarYear)  
    END  
    ```  
  
     この SQL スクリプトは、テーブルの各半期に表示されている半期と年度を連結し、連結した名前を新しい列に表示します。  
  
10. **[OK]** をクリックします。  
  
11. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="defining-composite-keycolumns-and-setting-the-name-column"></a>複合 KeyColumns の定義と名前列の設定  
 **KeyColumns** プロパティは、属性のキーを表す 1 つ以上の列を示します。 この実習では、複合 **KeyColumns**を定義します。  
  
#### <a name="to-define-composite-keycolumns-for-the-english-month-name-attribute"></a>English Month Name 属性の複合 KeyColumns を定義するには  
  
1.  Date ディメンションの **[ディメンション構造]** タブを開きます。  
  
2.  **[属性]** ペインで、 **[English Month Name]** 属性をクリックします。  
  
3.  **[プロパティ]** ウィンドウで **[KeyColumns]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
4.  **[キー列]** ダイアログ ボックスの **[使用できる列]** ボックスの一覧で **[CalendarYear]** 列を選択し、 **[>]** をクリックします。  
  
5.  **[EnglishMonthName]** 列と **[CalendarYear]** 列が **[キー列]** ボックスの一覧に表示されるようになりました。  
  
6.  **[OK]** をクリックします。  
  
7.  **EnglishMonthName** 属性の **NameColumn** プロパティを設定するには、[プロパティ] ウィンドウで **[NameColumn]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
8.  **名前列**] ダイアログ ボックスで、**基になる列**一覧で、[ `MonthName`、順にクリックします **[ok]** します。  
  
9. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-quarter-attribute"></a>Calendar Quarter 属性の複合 KeyColumns を定義するには  
  
1.  **[属性]** ペインで、 **[Calendar Quarter]** 属性をクリックします。  
  
2.  **[プロパティ]** ウィンドウで **[KeyColumns]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
3.  **[キー列]** ダイアログ ボックスの **[使用できる列]** ボックスの一覧で **[CalendarYear]** 列を選択し、 **[>]** をクリックします。  
  
     **[CalendarQuarter]** 列と **[CalendarYear]** 列が **[キー列]** ボックスの一覧に表示されるようになりました。  
  
4.  **[OK]** をクリックします。  
  
5.  **Calendar Quarter** 属性の **NameColumn** プロパティを設定するには、[プロパティ] ウィンドウで **[NameColumn]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
6.  **名前列**] ダイアログ ボックスで、**基になる列**一覧で、[ `CalendarQuarterDesc`、順にクリックします **[ok]** します。  
  
7.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-semester-attribute"></a>Calendar Semester 属性の複合 KeyColumns を定義するには  
  
1.  **[属性]** ペインで、 **[Calendar Semester]** 属性をクリックします。  
  
2.  **[プロパティ]** ウィンドウで **[KeyColumns]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
3.  **[キー列]** ダイアログ ボックスの **[使用できる列]** ボックスの一覧で **[CalendarYear]** 列を選択し、 **[>]** をクリックします。  
  
     **[CalendarSemester]** 列と **[CalendarYear]** 列が **[キー列]** ボックスの一覧に表示されるようになりました。  
  
4.  **[OK]** をクリックします。  
  
5.  **Calendar Semester** 属性の **NameColumn** プロパティを設定するには、[プロパティ] ウィンドウで **[NameColumn]** フィールドをクリックし、参照ボタン ( **[...]** ) をクリックします。  
  
6.  **名前列**] ダイアログ ボックスで、**基になる列**一覧で、[ `CalendarSemesterDesc`、順にクリックします **[ok]** します。  
  
7.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="deploying-and-viewing-the-changes"></a>変更の配置と表示  
 属性と階層を変更したら、変更を表示する前に変更を配置し、関連するオブジェクトを再処理する必要があります。  
  
#### <a name="to-deploy-and-view-the-changes"></a>変更を配置して表示するには  
  
1.  **で、** [ビルド] [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]メニューの **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  受信した後、**配置が正常に完了した**メッセージで、をクリックして、**ブラウザー**のタブ**ディメンション デザイナー**の`Date`ディメンション、およびデザイナーのツールバーにある再接続ボタンをクリックします。  
  
3.  **[階層]** ボックスの一覧から **[Calendar Quarter]** を選択します。 **Calendar Quarter** 属性階層のメンバーを確認します。  
  
     名前付き計算を作成して名前として使用しているため、 **Calendar Quarter** 属性階層のメンバー名が明確でわかりやすい名前になっています。 メンバーは、各年の各四半期の **Calendar Quarter** 属性階層内に存在しています。 メンバーの並び順は年代順ではありません。 まず四半期順に並べ替えられ、次に年度順に並べ替えられています。 このトピックの次の実習では、この属性階層のメンバーが年度順に並べられ、さらに四半期順に並べられるように設定します。  
  
4.  **English Month Name** および **Calendar Semester** 属性階層のメンバーを確認します。  
  
     この 2 つの階層のメンバーも日時順には並んでいません。 EnglishMonthName は月、CalendarSemester は半期の順にまず並べ替えられ、その後、年度順に並べ替えられています。 このトピックの次の実習では、この並べ替え順序が変わるように複合キーを修正します。  
  
## <a name="changing-the-sort-order-by-modifying-composite-key-member-order"></a>複合キーのメンバーの順序を変更することによる並べ替え順序の変更  
 この実習では、複合キーを構成するキーの順序を変更することにより並べ替え順序を変更します。  
  
#### <a name="to-modify-the-composite-key-member-order"></a>複合キーのメンバーの順序を変更するには  
  
1.  開く、**ディメンション構造**ディメンションのディメンション デザイナーのタブ、`Date`ディメンションをクリックし  **Calendar Semester**で、**属性**ウィンドウ。  
  
2.  [プロパティ] ウィンドウで、 **OrderBy** プロパティの値を確認します。 **Key**に設定されています。  
  
     **Calendar Semester** 属性階層のメンバーは、キー値に基づいて並べ替えられます。 複合キーにより、メンバーのキーがまず 1 番目のキーに基づいて並べ替えられ、次に 2 番目のキーに基づいて並べ替えられています。 つまり、 **Calendar Semester** 属性階層のメンバーはまず半期順に並べ替えられ、続いて年度順に並べ替えられています。  
  
3.  **KeyColumns**プロパティの値を変更するため、[プロパティ] ウィンドウで参照ボタン ( **[...]** ) をクリックします。  
  
4.  **[キー列]** ダイアログ ボックスの **[キー列]** ボックスの一覧で、 **[CalendarSemester]** が選択されていることを確認します。次に、下矢印をクリックし、この複合キーのメンバーの順序を逆にします。 **[OK]** をクリックします。  
  
     CalendarSemester 属性階層のメンバーが、まず年度順に並べ替えられ、続いて半期順に並べ替えられるようになりました。  
  
5.  **[属性]** ペインで **[Calendar Quarter]** を選択した後、[プロパティ] ウィンドウで、**KeyColumns**プロパティの省略記号ボタン ( **[...]** ) をクリックします。  
  
6.  **[キー列]** ダイアログ ボックスの **[キー列]** ボックスの一覧で、 **[CalendarQuarter]** が選択されていることを確認します。次に、下矢印をクリックし、この複合キーのメンバーの順序を逆にします。 **[OK]** をクリックします。  
  
     CalendarQuarter 属性階層のメンバーが、まず年度順に並べ替えられ、続いて四半期順に並べ替えられるようになりました。  
  
7.  **[属性]** ペインで **[English Month Name]** を選択した後、[プロパティ] ウィンドウで、**KeyColumns**プロパティの省略記号ボタン ( **[...]** ) をクリックします。  
  
8.  **[キー列]** ダイアログ ボックスの **[キー列]** ボックスの一覧で、 **[EnglishMonthName]** が選択されていることを確認します。次に、下矢印をクリックし、この複合キーのメンバーの順序を逆にします。 **[OK]** をクリックします。  
  
     EnglishMonthName 属性階層のメンバーが、まず年度順に並べ替えられ、続いて月順に並べ替えられるようになりました。  
  
9. **で、** [ビルド] [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]メニューの **[Analysis Services Tutorial の配置]** をクリックします。 デプロイが正常に完了したら、クリックして、**ブラウザー**のディメンション デザイナーのタブ、`Date`ディメンション。  
  
10. **[ブラウザー]** タブのツール バーで、[再接続] ボタンをクリックします。  
  
11. **Calendar Quarter** および **Calendar Semester** 属性階層のメンバーを確認します。  
  
     これらの階層のメンバーは、日時順に並べ替えられるようになりました。まず年度順に並べ替えられ、続いて Calendar Quarter は四半期順に、CalendarSemester は半期順に並べ替えられています。  
  
12. **English Month Name** 属性階層のメンバーを確認します。  
  
     属性階層のメンバーは、まず年度順に並べ替えられ、続いて月名順 (アルファベット順) に並べ替えられるようになりました。 これは、データ ソース ビューの EnglishCalendarMonth 列のデータ型が、基になるリレーショナル データベースでの nvarchar データ型に基づき、文字列型となっているためです。 各年度の月を古い順に並べ替えられるようにする方法の詳細については、「[2 次属性に基づく属性メンバーの並べ替え](lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)」を参照してください。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [配置したキューブの表示](lesson-3-5-browsing-the-deployed-cube.md)  
  
## <a name="see-also"></a>関連項目  
 [多次元モデル内のディメンション](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
