---
title: 'レッスン 3: 列名の変更 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80d9cae6deae4059327084f531f6a6d958a39ec6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070316"
---
# <a name="lesson-3-rename-columns"></a>レッスン 3: 列名の変更
  このレッスンでは、インポートした各テーブル内の多くの列の名前を変更します。 名前を変更することで、列がより識別しやすくなり、モデル デザイナー内でも、またクライアント アプリケーションでユーザーがフィールドを選択する際にも、移動が行いやすくなります。 詳細については、「[テーブルまたは列名の変更 (SSAS テーブル)](tabular-models/rename-a-table-or-column-ssas-tabular.md)」を参照してください。  
  
> [!IMPORTANT]  
>  列名の変更は、このチュートリアルを完了するために必ずしも必要ではありませんが、残りのレッスン (リレーションシップを作成するレッスンと、DAX 数式を使用して計算列とメジャーを作成するレッスン) では、このレッスンに記載されているわかりやすい列名が使用されます。 列名を変更しない場合は、レッスン 5、6、および 7 を行う際に、このレッスンで示す元のソース列名を使用するように DAX 数式を編集してください。  
  
 このレッスンを完了するまでに時間を推定するには。**20 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 2:データを追加する](lesson-2-add-data.md)します。  
  
## <a name="rename-columns"></a>列名の変更  
  
#### <a name="to-rename-columns"></a>列名を変更するには  
  
1.  モデル デザイナーで、 **Customer** テーブル (タブ) をクリックします。  
  
     タブをクリックすると、そのテーブルがモデル デザイナー ウィンドウでアクティブになります。  
  
2.  ダブルクリックして、 **CustomerKey**列名、し、入力`Customer  Id`、し、ENTER キーを押します。  
  
    > [!TIP]  
    >  内の列の名前を変更することもできます、**列名**列のプロパティ**プロパティ**ウィンドウ、またはダイアグラム ビューで。  
  
3.  **Customer** テーブル内の残りの列と、その他のテーブル内の列についても、ソース名を次の表示名に置き換えて名前変更します。  
  
     **Customer テーブル**  
  
    |ソース名|フレンドリ名|  
    |-----------------|-------------------|  
    |GeographyKey|[Geography Id]|  
    |CustomerAlternateKey|Customer Alternate Id|  
    |FirstName|First Name|  
    |MiddleName|Middle Name|  
    |LastName|Last Name|  
    |NameStyle|Name Style|  
    |BirthDate|[Birth Date]|  
    |MaritalStatus|Marital Status|  
    |EmailAddress|Email Address|  
    |YearlyIncome|Yearly Income|  
    |TotalChildren|Total Children|  
    |NumberChildrenAtHome|Number of Children At Home|  
    |EnglishEducation|Education|  
    |EnglishOccupation|Occupation|  
    |HouseOwnerFlag|Owns House|  
    |NumberCarsOwned|Number of Cars Owned|  
    |AddressLine1|Address Line 1|  
    |AddressLine2|Address Line 2|  
    |Phone|Phone Number|  
    |DateFirstPurchase|Date of First Purchase|  
    |CommuteDistance|Commute Distance|  
  
     **Date**  
  
    |ソース名|フレンドリ名|  
    |-----------------|-------------------|  
    |FullDateAlternateKey|date|  
    |DayNumberOfWeek|Day Number of Week|  
    |EnglishDayNameOfWeek|Day Name|  
    |DayNumberOfMonth|Day of Month|  
    |DayNumberOfYear|Day of Year|  
    |WeekNumberOfYear|Week Number of Year|  
    |EnglishMonthName|Month Name|  
    |MonthNumberOfYear|Month|  
    |CalendarQuarter|Calendar Quarter|  
    |CalendarYear|Calendar Year|  
    |CalendarSemester|Calendar Semester|  
    |FiscalQuarter|Fiscal Quarter|  
    |FiscalYear|Fiscal Year|  
    |FiscalSemester|Fiscal Semester|  
  
     **Geography**  
  
    |ソース名|フレンドリ名|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |StateProvinceCode|State Province Code|  
    |StateProvinceName|State Province Name|  
    |CountryRegionCode|Country Region Code|  
    |EnglishCountryRegionName|Country Region Name|  
    |PostalCode|Postal Code|  
    |SalesTerritoryKey|Sales Territory Id|  
  
     **Product**  
  
    |ソース名|フレンドリ名|  
    |-----------------|-------------------|  
    |ProductKey|[Product Id]|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |WeightUnitMeasureCode|Weight Unit Code|  
    |SizeUnitMeasureCode|Size Unit Code|  
    |EnglishProductName|製品名|  
    |StandardCost|Standard Cost|  
    |FinishedGoodsFlag|Is Finished Product|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|List Price|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Days to Manufacture|  
    |ProductLine|Product Line|  
    |Dealer Price|Dealer Price|  
    |ModelName|Model Name|  
    |LargePhoto|Large Photo|  
    |EnglishDescription|説明|  
    |StartDate|Product Start Date|  
    |EndDate|Product End Date|  
    |状態|Product Status|  
  
     **製品カテゴリ**  
  
    |ソース名|表示名|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Product Category Id|  
    |ProductCategoryAlternateKey|Product Category Alternate Id|  
    |EnglishProductCategoryName|Product Category Name|  
  
     **Product Subcategory**  
  
    |ソース名|フレンドリ名|  
    |-----------------|-------------------|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |ProductSubcategoryAlternateKey|Product Subcategory Alternate Id|  
    |EnglishProductSubcategoryName|Product Subcategory Name|  
    |ProductCategoryKey|Product Category Id|  
  
     **Internet Sales**  
  
    |ソース名|フレンドリ名|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |CustomerKey|Customer Id|  
    |PromotionKey|Promotion Id|  
    |CurrencyKey|Currency Id|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesOrderNumber|Sales Order Number|  
    |SalesOrderLineNumber|Sales Order Line Number|  
    |RevisionNumber|Revision Number|  
    |OrderQuantity|Order Quantity|  
    |UnitPrice|Unit Price|  
    |ExtendedAmount|Extended Amount|  
    |UnitPriceDiscountPct|Unit Price Discount Pct|  
    |DiscountAmount|Discount Amount|  
    |ProductStandardCost|Product Standard Cost|  
    |TotalProductCost|Total Product Cost|  
    |SalesAmount|Sales Amount|  
    |TaxAmt|Tax Amt|  
    |CarrierTrackingNumber|Carrier Tracking Number|  
    |CustomerPONumber|Customer PO Number|  
    |OrderDate|Order Date|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## <a name="next-step"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。[レッスン 4:日付テーブルとしてマーク](lesson-3-mark-as-date-table.md)します。  
  
  
