---
title: 属性の種類の構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- attributes [Analysis Services], types
- slowly changing dimensions
- account dimensions [Analysis Services]
- currency dimensions [Analysis Services]
- Type property
ms.assetid: c2c6a3da-555e-4362-a83f-88da28427520
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5223444f58326b7530388f3fe2fc06d72488a5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077409"
---
# <a name="configure-attribute-types"></a>属性の種類の構成
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、属性の型を使用して、ビジネス機能で属性を分類できます。 属性の型は多数用意されており、そのほとんどは属性の表示やサポートのためにクライアント アプリケーションで使用されています。 ただし、属性の型の中には、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]で特定の意味を持つものもあります。 たとえば、時間ディメンションのさまざまなカレンダーで時刻を表す属性を識別する属性の型がいくつか用意されています。  
  
##  <a name="setting_attibute_types"></a> 属性の型の設定  
 属性の型は、その属性の `Type` プロパティの値によって決まります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のいくつかのウィザードでは、ディメンションまたは属性の定義時に属性の型を設定します。 これらの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ウィザードでは、ウィザードによってディメンションに機能が追加された場合にも属性の型を設定します。 たとえば、ビジネス インテリジェンス ウィザードでは、ディメンション内の勘定科目の名前、コード、番号、構造を含んでいる属性を識別するための勘定科目インテリジェンスの追加時に、ディメンション内の属性に複数の属性の型を適用します。 また、ビジネス インテリジェンス ウィザードでは、通貨換算などにも属性の型を使用します。 詳細については、「 [通貨ディメンションの作成](database-dimensions-create-a-currency-type-dimension.md)」を参照してください。  
  
 次の表では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]で使用可能な属性の型について説明します。 表内の属性の型は次のカテゴリに区分されています。  
  
|項目|定義|  
|----------|----------------|  
|[一般的な属性の型](#general_attribute_types)|これらの値はすべての属性で使用できます。また、クライアント アプリケーション用の属性の分類にのみ使用できます。|  
|[勘定科目ディメンションの属性の型](#account_dimension_attribute_types)|これらの値によって、勘定科目ディメンションに属している属性を識別します。 勘定科目ディメンションの詳細については、「 [親子型ディメンションの財務アカウントの作成](database-dimensions-finance-account-of-parent-child-type.md)」を参照してください。|  
|[通貨ディメンションの属性の型](#currency_dimension_attribute_types)|これらの値によって、通貨ディメンションに属している属性を識別します。 通貨ディメンションの詳細については、「 [通貨ディメンションの作成](database-dimensions-create-a-currency-type-dimension.md)」を参照してください。|  
|[緩やかに変化するディメンションの属性](#slowly_changing_dimension_attribute_types)|これらの値によって、緩やかに変化するディメンションに属している属性を識別します。|  
|[時間ディメンションの属性](#time_dimension_attribute_types)|これらの値によって、時間ディメンションに属している属性を識別します。 時間ディメンションの詳細については、「 [日付型ディメンションの作成](database-dimensions-create-a-date-type-dimension.md)」を参照してください。|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|属性の型の値|説明|  
|--------------------------|-----------------|  
|`Address`|住所を表します。|  
|`AddressBuilding`|住所のビル名を表します。|  
|`AddressCity`|住所の市区町村を表します。|  
|`AddressCountry`|住所の国または地域を表します。|  
|`AddressFax`|FAX 番号を表します。|  
|`AddressFloor`|住所の階数を表します。|  
|`AddressHouse`|住所の棟番号を表します。|  
|`AddressPhone`|電話番号を表します。|  
|`AddressQuarter`|住所の地区を表します。|  
|`AddressRoom`|住所の部屋番号を表します。|  
|`AddressStateOrProvince`|住所の都道府県を表します。|  
|`AddressStreet`|住所の番地を表します。|  
|`AddressZip`|住所の郵便番号を表します。|  
|`BomResource`|部品表 (BOM) のリソースを表します。|  
|`Caption`|キャプションを表します。|  
|`CaptionAbbreviation`|省略形を表します。|  
|`CaptionDescription`|説明を表します。|  
|`Channel`|チャネルを表します。|  
|`City`|市区町村を表します。|  
|`Company`|会社を表します。|  
|`Continent`|大陸を表します。|  
|`Country`|国または地域を表します。|  
|`County`|郡を表します。|  
|`CustomerGroup`|顧客のグループを表します。|  
|`CustomerHousehold`|顧客の世帯を表します。|  
|`Customers`|顧客を表します。|  
|`DateCanceled`|取り消された日付を表します。|  
|`DateDuration`|期間を表します。|  
|`DateEnded`|終了日を表します。|  
|`DateModified`|更新日を表します。|  
|`DateStart`|開始日を表します。|  
|**DeletedFlag**|(ビジネス機能の点から) メンバーが削除されているか、削除する必要があることを示します。<br /><br /> 注: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、この属性のタイプを使用して、メンバーが削除される必要があるかどうかを判断することはありません。 この属性のタイプはクライアント アプリケーションでの表示目的のみに使用されます。|  
|`FormattingColor`|書式設定で使用される色を表す属性です。|  
|`FormattingFont`|書式設定で使用されるフォントを表す属性です。|  
|`FormattingFontEffects`|書式設定で使用されるフォントの文字飾りを表す属性です。|  
|`FormattingFontSize`|書式設定で使用されるフォント サイズを表す属性です。|  
|`FormattingOrder`|書式設定で使用される並べ替え順を表す属性です。|  
|`FormattingSubtotal`|小計を表します。|  
|`GeoBoundaryBottom`|地理的境界の下端の値を表します。|  
|`GeoBoundaryFront`|地理的境界の前面の値を表します。|  
|`GeoBoundaryLeft`|地理的境界の左端の値を表します。|  
|`GeoBoundaryPolygon`|地理的境界の多角形定義を表します。|  
|`GeoBoundaryRear`|地理的境界の最後面の値を表します。|  
|`GeoBoundaryRight`|地理的境界の右端の値を表します。|  
|`GeoBoundaryTop`|地理的境界の上端の値を表します。|  
|`GeoCentroidX`|地理的領域の X 軸重心を表します。|  
|`GeoCentroidY`|地理的領域の Y 軸重心を表します。|  
|`GeoCentroidZ`|地理的領域の Z 軸重心を表します。|  
|`ID`|識別子 (ID) またはキーを表します。|  
|`Image`|未定義のグラフィック形式の画像を表します。|  
|`ImageBmp`|ビットマップ グラフィック形式の画像を表します。|  
|`ImageGif`|GIF (Graphics Interchange Format) グラフィック形式の画像を表します。|  
|`ImageJpg`|JPEG (Joint Photographic Experts Group) グラフィック形式の画像を表します。|  
|`ImagePng`|PNG (Portable Network Graphics) グラフィック形式の画像を表します。|  
|`ImageTiff`|TIFF (Tagged Image File Format) グラフィック形式の画像を表します。|  
|`OrganizationalUnit`|組織単位を表します。|  
|`OrgTitle`|職位を表します。|  
|`PercentOwnership`|所有権の比率を表します。|  
|`PercentVoteRight`|投票権の比率を表します。|  
|`Person`|個人を表します。|  
|`PersonContact`|個人の連絡先情報を表します。|  
|`PersonDemographic`|個人の人口統計情報を表します。|  
|`PersonFirstName`|個人の名を表します。|  
|`PersonFullName`|個人の氏名を表します。|  
|`PersonLastName`|個人の姓を表します。|  
|`PersonMiddleName`|個人のミドル ネームを表します。|  
|`PhysicalColor`|色を表します。|  
|`PhysicalDensity`|密度を表します。|  
|`PhysicalDepth`|奥行を表します。|  
|`PhysicalHeight`|高さを表します。|  
|`PhysicalSize`|サイズを表します。|  
|`PhysicalVolume`|容積を表します。|  
|`PhysicalWeight`|重量を表します。|  
|`PhysicalWidth`|幅を表します。|  
|`Point`|ポイントを表します。|  
|`PostalCode`|郵便番号を表します。|  
|`Product`|製品を表します。|  
|`ProductBrand`|製品ブランドを表します。|  
|`ProductCategory`|製品カテゴリを表します。|  
|`ProductGroup`|製品グループを表します。|  
|`ProductSKU`|製品 SKU (Stock Keeping Unit) を表します。|  
|`Project`|プロジェクトを表します。|  
|`ProjectCode`|プロジェクト コードを表します。|  
|`ProjectCompletion`|プロジェクトの完了状態を表します。|  
|`ProjectEndDate`|プロジェクト終了日を表します。|  
|`ProjectName`|プロジェクト名を表します。|  
|`ProjectStartDate`|プロジェクト開始日を表します。|  
|`Promotion`|昇格を表します。|  
|`QtyRangeHigh`|数量範囲の上限値を表します。|  
|`QtyRangeLow`|数量範囲の下限値を表します。|  
|`Quantitative`|数量属性を表します。|  
|`Rate`|レートを表します。|  
|`RateType`|レートの種類を表します。|  
|`Region`|顧客によって定義された領域を表します。|  
|`Regular`|標準属性を表します。|  
|`RelationToParent`|親へのリレーションを表します。|  
|`Representative`|代表者を表します。|  
|`Scenario`|シナリオを表します。|  
|`Sequence`|シーケンス属性を表します。|  
|`ShortCaption`|短いキャプションを表します。|  
|`StateOrProvince`|都道府県を表します。|  
|`Utility`|ユーティリティを表します。|  
|`Version`|バージョンを表します。|  
|`WebHtml`|HTML コンテンツを表します。|  
|`WebMailAlias`|電子メールの別名を表します。|  
|`WebUrl`|URL アドレスを表します。|  
|`WebXmlOrXsl`|XML または XSL コンテンツを表します。|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|属性の型の値|説明|  
|--------------------------|-----------------|  
|`Account`|勘定科目の親を表します。 この属性の型は、通常、勘定科目ディメンションの親属性に適用されます。|  
|`AccountName`|勘定科目名を表します。 この属性の型は、通常、勘定科目ディメンションのキー属性に適用されます。|  
|`AccountNumber`|勘定科目の番号を表します。|  
|`AccountType`|勘定科目の種類を表します。 この属性の種類は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの勘定科目の種類のディメンションに含まれる勘定科目メンバーの集計関数を指定します。|  
  
###  <a name="currency_dimension_attribute_types"></a> 通貨ディメンションの属性の型  
  
|属性の型の値|説明|  
|--------------------------|-----------------|  
|`CurrencyDestination`|通貨換算の換算先通貨を表します。 この属性の型は、通常、通貨換算で使用するためにレポーティング ディメンションのキー属性に適用されます。 通貨換算の詳細については、「[通貨換算 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)」を参照してください。|  
|`CurrencyIsoCode`|通貨の ISO (国際標準化機構) コードを表します。 通貨換算の詳細については、「[通貨換算 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)」を参照してください。|  
|`CurrencyName`|通貨の名前を表します。 通貨換算の詳細については、「[通貨換算 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)」を参照してください。|  
|`CurrencySource`|通貨換算の換算元通貨を表します。 この属性の型は、通常、通貨換算で使用するために通貨ディメンションのキー属性に適用されます。 通貨換算の詳細については、「[通貨換算 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)」を参照してください。|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> 緩やかに変化するディメンションの属性の型  
  
|属性の型の値|説明|  
|--------------------------|-----------------|  
|**ScdEndDate**|緩やかに変化するディメンションのメンバーの実効終了日を表します。|  
|**ScdOriginalID**|緩やかに変化するディメンションのメンバーの元の識別子を表します。|  
|**ScdStartDate**|緩やかに変化するディメンションのメンバーの実効開始日を表します。|  
|`ScdStatus`|緩やかに変化するディメンションのメンバーの実効状態を表します。|  
  
###  <a name="time_dimension_attribute_types"></a> 時間ディメンションの属性の型  
  
|属性の型の値|説明|  
|--------------------------|-----------------|  
|`Date`|日付を表します。 この属性の型は、通常、時間ディメンションまたはサーバー時間ディメンションのキー属性に適用されます。|  
|`DayOfHalfYear`|半期の通算日を表します。|  
|`DayOfMonth`|月の通算日を表します。|  
|`DayOfQuarter`|四半期の通算日を表します。|  
|`DayOfTenDays`|10 日間の通算日を表します。|  
|`DayOfTrimester`|三半期の通算日を表します。|  
|`DayOfWeek`|週の通算日を表します。|  
|`DayOfYear`|年の通算日を表します。|  
|`Days`|日数を表します。|  
|`FiscalDate`|会計カレンダーにおける日付を表します。|  
|`FiscalDayOfHalfYear`|会計カレンダーにおける半期の通算日を表します。|  
|`FiscalDayOfMonth`|会計カレンダーにおける月の通算日を表します。|  
|`FiscalDayOfQuarter`|会計カレンダーにおける四半期の通算日を表します。|  
|`FiscalDayOfTrimester`|会計カレンダーにおける三半期の通算日を表します。|  
|`FiscalDayOfWeek`|会計カレンダーにおける週の通算日を表します。|  
|`FiscalDayOfYear`|会計カレンダーにおける年の通算日を表します。|  
|`FiscalHalfYears`|会計カレンダーにおける半期を表します。|  
|`FiscalHalfYearOfYear`|会計カレンダーにおける年の通算半期を表します。|  
|`FiscalMonths`|会計カレンダーにおける月を表します。|  
|`FiscalMonthOfHalfYear`|会計カレンダーにおける半期の通算月を表します。|  
|`FiscalMonthOfQuarter`|会計カレンダーにおける四半期の通算月を表します。|  
|`FiscalMonthOfTrimester`|会計カレンダーにおける三半期の通算月を表します。|  
|`FiscalMonthOfYear`|会計カレンダーにおける年の通算月を表します。|  
|`FiscalQuarters`|会計カレンダーにおける四半期を表します。|  
|`FiscalQuarterOfHalfYear`|会計カレンダーにおける半期の通算四半期を表します。|  
|`FiscalQuarterOfYear`|会計カレンダーにおける年の通算四半期を表します。|  
|`FiscalTrimesters`|会計カレンダーにおける三半期を表します。|  
|`FiscalTrimesterOfYear`|会計カレンダーにおける年の通算三半期を表します。|  
|`FiscalWeeks`|会計カレンダーにおける週を表します。|  
|`FiscalWeekOfHalfYear`|会計カレンダーにおける半期の通算週を表します。|  
|`FiscalWeekOfMonth`|会計カレンダーにおける月の通算週を表します。|  
|`FiscalWeekOfQuarter`|会計カレンダーにおける四半期の通算週を表します。|  
|`FiscalWeekOfTrimester`|会計カレンダーにおける三半期の通算週を表します。|  
|`FiscalWeekOfYear`|会計カレンダーにおける年の通算週を表します。|  
|`FiscalYears`|会計カレンダーにおける年を表します。|  
|`HalfYears`|半期を表します。|  
|`HalfYearOfYear`|年の通算の半期を表します。|  
|`Hours`|時間数を表します。|  
|`IsHoliday`|祝日かどうかを表します。|  
|`ISO8601Date`|ISO 8601 カレンダーにおける日付を表します。|  
|`ISO8601DayOfWeek`|ISO 8601 カレンダーにおける週の通算日を表します。|  
|`ISO8601DayOfYear`|ISO 8601 カレンダーにおける年の通算日を表します。|  
|`ISO8601Weeks`|ISO 8601 カレンダーにおける週を表します。|  
|`ISO8601WeekOfYear`|ISO 8601 カレンダーにおける年の通算週を表します。|  
|`ISO8601Years`|ISO 8601 カレンダーにおける年を表します。|  
|`IsPeakDay`|ピーク日かどうかを表します。|  
|`IsWeekDay`|平日かどうかを表します。|  
|`IsWorkingDay`|営業日かどうかを表します。|  
|`ManufacturingDate`|製造カレンダーにおける日付を表します。|  
|`ManufacturingDayOfHalfYear`|製造カレンダーにおける半期の通算日を表します。|  
|`ManufacturingDayOfMonth`|製造カレンダーにおける月の通算日を表します。|  
|`ManufacturingDayOfQuarter`|製造カレンダーにおける四半期の通算日を表します。|  
|`ManufacturingDayOfTrimester`|製造カレンダーにおける三半期の通算日を表します。|  
|`ManufacturingDayOfWeek`|製造カレンダーにおける週の通算日を表します。|  
|`ManufacturingDayOfYear`|製造カレンダーにおける年の通算日を表します。|  
|`ManufacturingHalfYears`|製造カレンダーにおける半期を表します。|  
|`ManufacturingHalfYearOfYear`|製造カレンダーにおける年の通算の半期を表します。|  
|`ManufacturingMonths`|製造カレンダーにおける月を表します。|  
|`ManufacturingMonthOfHalfYear`|製造カレンダーにおける半期の通算月を表します。|  
|`ManufacturingMonthOfQuarter`|製造カレンダーにおける四半期の通算月を表します。|  
|`ManufacturingMonthOfTrimester`|製造カレンダーにおける三半期の通算月を表します。|  
|`ManufacturingMonthOfYear`|製造カレンダーにおける年の通算月を表します。|  
|`ManufacturingQuarters`|製造カレンダーにおける四半期を表します。|  
|`ManufacturingQuarterOfHalfYear`|製造カレンダーにおける半期の通算四半期を表します。|  
|`ManufacturingQuarterOfYear`|製造カレンダーにおける年の通算四半期を表します。|  
|`ManufacturingWeeks`|製造カレンダーにおける週を表します。|  
|`ManufacturingWeekOfHalfYear`|製造カレンダーにおける半期の通算週を表します。|  
|`ManufacturingWeekOfMonth`|製造カレンダーにおける月の通算週を表します。|  
|`ManufacturingWeekOfQuarter`|製造カレンダーにおける四半期の通算週を表します。|  
|`ManufacturingWeekOfTrimester`|製造カレンダーにおける三半期の通算週を表します。|  
|`ManufacturingWeekOfYear`|製造カレンダーにおける年の通算週を表します。|  
|`ManufacturingYears`|製造カレンダーにおける年を表します。|  
|`Minutes`|分数を表します。|  
|`Months`|月数を表します。|  
|`MonthOfHalfYear`|半期の通算月を表します。|  
|`MonthOfQuarter`|四半期の通算月を表します。|  
|`MonthOfTrimester`|三半期の通算月を表します。|  
|`MonthOfYear`|年の通算月を表します。|  
|`Quarters`|四半期を表します。|  
|`QuarterOfHalfYear`|半期の通算四半期を表します。|  
|`QuarterOfYear`|年の通算四半期を表します。|  
|`ReportingDate`|レポート カレンダーにおける日付を表します。|  
|`ReportingDayOfHalfYear`|レポート カレンダーにおける半期の通算日を表します。|  
|`ReportingDayOfMonth`|レポート カレンダーにおける月の通算日を表します。|  
|`ReportingDayOfQuarter`|レポート カレンダーにおける四半期の通算日を表します。|  
|`ReportingDayOfTrimester`|レポート カレンダーにおける三半期の通算日を表します。|  
|`ReportingDayOfWeek`|レポート カレンダーにおける週の通算日を表します。|  
|`ReportingDayOfYear`|レポート カレンダーにおける年の通算日を表します。|  
|`ReportingHalfYears`|レポート カレンダーにおける半期を表します。|  
|`ReportingHalfYearOfYear`|レポート カレンダーにおける年の通算半期を表します。|  
|`ReportingMonths`|レポート カレンダーにおける月を表します。|  
|`ReportingMonthOfHalfYear`|レポート カレンダーにおける半期の通算月を表します。|  
|`ReportingMonthOfQuarter`|レポート カレンダーにおける四半期の通算月を表します。|  
|`ReportingMonthOfTrimester`|レポート カレンダーにおける三半期の通算月を表します。|  
|`ReportingMonthOfYear`|レポート カレンダーにおける年の通算月を表します。|  
|`ReportingQuarters`|レポート カレンダーにおける四半期を表します。|  
|`ReportingQuarterOfHalfYear`|レポート カレンダーにおける半期の通算四半期を表します。|  
|`ReportingQuarterOfYear`|レポート カレンダーにおける年の通算四半期を表します。|  
|`ReportingTrimesters`|レポート カレンダーにおける三半期を表します。|  
|`ReportingTrimesterOfYear`|レポート カレンダーにおける年の通算三半期を表します。|  
|`ReportingWeeks`|レポート カレンダーにおける週を表します。|  
|`ReportingWeekOfHalfYear`|レポート カレンダーにおける半期の通算週を表します。|  
|`ReportingWeekOfMonth`|レポート カレンダーにおける月の通算週を表します。|  
|`ReportingWeekOfQuarter`|レポート カレンダーにおける四半期の通算週を表します。|  
|`ReportingWeekOfTrimester`|レポート カレンダーにおける三半期の通算週を表します。|  
|`ReportingWeekOfYear`|レポート カレンダーにおける年の通算週を表します。|  
|`ReportingYears`|レポート カレンダーにおける年を表します。|  
|`Seconds`|秒数を表します。|  
|`TenDayOfHalfYear`|半期の通算の 10 日間を表します。|  
|`TenDayOfMonth`|月の通算の 10 日間を表します。|  
|`TenDayOfQuarter`|四半期の通算の 10 日間を表します。|  
|`TenDayOfTrimester`|三半期の通算の 10 日間を表します。|  
|`TenDayOfYear`|年の通算の 10 日間を表します。|  
|`TenDays`|10 日間を表します。|  
|`Trimesters`|三半期を表します。|  
|`TrimesterOfYear`|年の通算三半期を表します。|  
|`UndefinedTime`|未定義の期間を表します。|  
|`WeekOfYear`|年の通算週を表します。|  
|`Weeks`|週数を表します。|  
|**WinterSummerSeason**|その日が冬期か夏期かを表します。|  
|`Years`|年数を表します。|  
  
## <a name="see-also"></a>参照  
 [属性と属性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [ディメンションの属性のプロパティの参照](dimension-attribute-properties-reference.md)  
  
  
