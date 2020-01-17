---
title: カスタム レポートでのオブジェクト エクスプローラー ノード プロパティの使用 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: c7b84355-71ba-402d-85af-23826f18b7da
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e3bc3c116f8082b17f392d04ae14e0895762fc37
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262066"
---
# <a name="use-custom-reports-with-object-explorer-node-properties"></a>カスタム レポートでのオブジェクト エクスプローラー ノード プロパティの使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
オブジェクト エクスプローラーで選択されているノードのレポート パラメーターがカスタム レポートで参照されていれば、そのノードのコンテキストでカスタム レポートを実行できます。 これにより、カスタム レポートで現在のコンテキスト (現在のデータベースなど)、またはデータベース オブジェクトやサーバー オブジェクトを使用できるようになります。  
  
## <a name="object-explorer-node-report-parameters"></a>オブジェクト エクスプローラー ノードのレポート パラメーター  
  
|[パラメーター名]|データ型|  
|------------------|-------------|  
|**ObjectName**|**文字列**|  
|**ObjectTypeName**|**String**|  
|**フィルター選択されたインデックス**|**ブール値**|  
|**ServerName**|**String**|  
|**フォント名**|**String**|  
|**DatabaseName**|**String**|  
  
## <a name="object-explorer-node-report-parameters-example"></a>オブジェクト エクスプローラー ノードのレポート パラメーターの例  
この例を実行するには、次の手順に従います。  
  
**オブジェクト エクスプローラーでノードのレポート パラメーターの値を表示するには**  
  
1.  次のサンプル コードを新規テキスト ファイルにコピーし、そのファイルに .rdl 拡張子を使った名前を付けます。  
  
2.  カスタム レポート用にデータベース サーバーで作成しておいたフォルダーに、このレポート ファイルをコピーします。  
  
3.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のオブジェクト エクスプローラーでノードを右クリックし、 **[レポート]** をポイントして、[カスタム レポート] をクリックします。 **[ファイルを開く]** ダイアログ ボックスで、カスタム レポート フォルダーを見つけてレポート ファイルを選択し、 **[開く]** をクリックします。  
  
    新しいカスタム レポートは、初めてオブジェクト エクスプローラーのノードから開いたときに、最近使用した一覧に追加されます。この一覧はノードのショートカット メニューの **[カスタム レポート]** の下に表示されます。 標準レポートも、初めて開いたときに **[カスタム レポート]** の下の最近使用した一覧に表示されます。 カスタム レポート ファイルを削除した場合は、次にそのアイテムを選択したときに、最近使用した一覧からアイテムを削除するというプロンプトが表示されます。  
  
    1.  最近使用した一覧の表示ファイル数を変更するには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[環境]** フォルダーを展開して **[全般]** をクリックします。  
  
    2.  **[最近使用したファイルの一覧]** の数を調整します。  
  
## <a name="custom-report-code-sample"></a>カスタム レポート コードのサンプル  
次のコードを使用して作成したレポートでは、オブジェクト エクスプローラー ノードに関連付けられているパラメーターが使用されます。  
  
```  
<pre><?xml version="1.0" encoding="utf-8"?>  
<Report xmlns="https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition" xmlns:rd="https://schemas.microsoft.com/SQLServer/reporting/reportdesigner">  
<ReportParameters>  
<ReportParameter Name="ObjectName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>ObjectName</Prompt>  
</ReportParameter>  
<ReportParameter Name="ObjectTypeName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>ObjectTypeName</Prompt>  
</ReportParameter>  
<ReportParameter Name="Filtered">  
<DataType>Boolean</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>Filtered</Prompt>  
</ReportParameter>  
<ReportParameter Name="ServerName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<AllowBlank>true</AllowBlank>  
<Prompt>ServerName</Prompt>  
</ReportParameter>  
<ReportParameter Name="FontName">  
<DataType>String</DataType>  
<DefaultValue>  
<Values>  
<Value>Tahoma</Value>  
</Values>  
</DefaultValue>  
<AllowBlank>true</AllowBlank>  
<Prompt>FontName</Prompt>  
</ReportParameter>  
<ReportParameter Name="DatabaseName">  
<DataType>String</DataType>  
<Nullable>true</Nullable>  
<DefaultValue>  
<Values>  
<Value>master</Value>  
</Values>  
</DefaultValue>  
<AllowBlank>true</AllowBlank>  
<Prompt>DatabaseName</Prompt>  
</ReportParameter>  
</ReportParameters>  
<DataSources>  
<DataSource Name="AllReportParameters">  
<ConnectionProperties>  
<IntegratedSecurity>true</IntegratedSecurity>  
<ConnectString>Data Source=.</ConnectString>  
<DataProvider>SQL</DataProvider>  
</ConnectionProperties>  
<rd:DataSourceID>f1feee4c-0fdc-4301-9efa-3cd89eed2d9f</rd:DataSourceID>  
</DataSource>  
</DataSources>  
<BottomMargin>1in</BottomMargin>  
<RightMargin>1in</RightMargin>  
<rd:DrawGrid>true</rd:DrawGrid>  
<InteractiveWidth>8.5in</InteractiveWidth>  
<rd:SnapToGrid>true</rd:SnapToGrid>  
<Body>  
<ReportItems>  
<Textbox Name="textbox1">  
<rd:DefaultName>textbox1</rd:DefaultName>  
<ZIndex>1</ZIndex>  
<Width>6in</Width>  
<Style>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>20pt</FontSize>  
<Color>SteelBlue</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Height>0.36in</Height>  
<Value>AllReportParameters</Value>  
</Textbox>  
<Table Name="table1">  
<DataSetName>AllReportParameters</DataSetName>  
<Top>0.36in</Top>  
<Details>  
<TableRows>  
<TableRow>  
<TableCells>  
<TableCell>  
<ReportItems>  
<Textbox Name="ObjectName">  
<rd:DefaultName>ObjectName</rd:DefaultName>  
<ZIndex>5</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!ObjectName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="ObjectTypeName">  
<rd:DefaultName>ObjectTypeName</rd:DefaultName>  
<ZIndex>4</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!ObjectTypeName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="Filtered">  
<rd:DefaultName>Filtered</rd:DefaultName>  
<ZIndex>3</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!Filtered.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="ServerName">  
<rd:DefaultName>ServerName</rd:DefaultName>  
<ZIndex>2</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!ServerName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="FontName">  
<rd:DefaultName>FontName</rd:DefaultName>  
<ZIndex>1</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!FontName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="DatabaseName">  
<rd:DefaultName>DatabaseName</rd:DefaultName>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>=Parameters!DatabaseName.Value</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
</TableCells>  
<Height>0.21in</Height>  
</TableRow>  
</TableRows>  
</Details>  
<Header>  
<TableRows>  
<TableRow>  
<TableCells>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox2">  
<rd:DefaultName>textbox2</rd:DefaultName>  
<ZIndex>11</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>ObjectName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox3">  
<rd:DefaultName>textbox3</rd:DefaultName>  
<ZIndex>10</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>ObjectTypeName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox4">  
<rd:DefaultName>textbox4</rd:DefaultName>  
<ZIndex>9</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>Filtered</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox5">  
<rd:DefaultName>textbox5</rd:DefaultName>  
<ZIndex>8</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>ServerName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox6">  
<rd:DefaultName>textbox6</rd:DefaultName>  
<ZIndex>7</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>FontName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
<TableCell>  
<ReportItems>  
<Textbox Name="textbox7">  
<rd:DefaultName>textbox7</rd:DefaultName>  
<ZIndex>6</ZIndex>  
<Style>  
<BorderStyle>  
<Default>Solid</Default>  
</BorderStyle>  
<PaddingLeft>2pt</PaddingLeft>  
<PaddingBottom>2pt</PaddingBottom>  
<FontFamily>Tahoma</FontFamily>  
<FontWeight>700</FontWeight>  
<FontSize>11pt</FontSize>  
<BorderColor>  
<Default>LightGrey</Default>  
</BorderColor>  
<BackgroundColor>SteelBlue</BackgroundColor>  
<Color>White</Color>  
<PaddingRight>2pt</PaddingRight>  
<PaddingTop>2pt</PaddingTop>  
</Style>  
<CanGrow>true</CanGrow>  
<Value>DatabaseName</Value>  
</Textbox>  
</ReportItems>  
</TableCell>  
</TableCells>  
<Height>0.22in</Height>  
</TableRow>  
</TableRows>  
<RepeatOnNewPage>true</RepeatOnNewPage>  
</Header>  
<TableColumns>  
<TableColumn>  
<Width>3in</Width>  
</TableColumn>  
<TableColumn>  
<Width>1.5in</Width>  
</TableColumn>  
<TableColumn>  
<Width>0.75in</Width>  
</TableColumn>  
<TableColumn>  
<Width>1.125in</Width>  
</TableColumn>  
<TableColumn>  
<Width>2in</Width>  
</TableColumn>  
<TableColumn>  
<Width>1.375in</Width>  
</TableColumn>  
</TableColumns>  
</Table>  
</ReportItems>  
<Height>0.79in</Height>  
</Body>  
<rd:ReportID>abb14e58-fd36-495a-89ff-b66f29ef287b</rd:ReportID>  
<LeftMargin>1in</LeftMargin>  
<DataSets>  
<DataSet Name="AllReportParameters">  
<Query>  
<rd:UseGenericDesigner>true</rd:UseGenericDesigner>  
<CommandText>SELECT 1  
</CommandText>  
<DataSourceName>AllReportParameters</DataSourceName>  
</Query>  
<Fields>  
<Field Name="ObjectName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>ObjectName</DataField>  
</Field>  
<Field Name="ObjectTypeName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>ObjectTypeName</DataField>  
</Field>  
<Field Name="Filtered">  
<rd:TypeName>System.Boolean</rd:TypeName>  
<DataField>Filtered</DataField>  
</Field>  
<Field Name="ServerName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>ServerName</DataField>  
</Field>  
<Field Name="FontName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>FontName</DataField>  
</Field>  
<Field Name="DatabaseName">  
<rd:TypeName>System.String</rd:TypeName>  
<DataField>DatabaseName</DataField>  
</Field>  
</Fields>  
</DataSet>  
</DataSets>  
<Width>6.875in</Width>  
<InteractiveHeight>11in</InteractiveHeight>  
<Language>en-US</Language>  
<TopMargin>1in</TopMargin>  
</Report></pre>  
```

## <a name="see-also"></a>参照  
[Management Studio におけるカスタム レポート](../../ssms/object/custom-reports-in-management-studio.md)  
[Management Studio へのカスタム レポートの追加](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[カスタム レポート実行時の警告の抑制を解除する方法](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
  
