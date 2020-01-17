---
title: データ フロー式を使用して設定できるプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, property expressions
- Integration Services packages, property expressions
- packages [Integration Services], properties
- SSIS packages, property expressions
- property expressions [Integration Services]
ms.assetid: cd0e171a-08be-45d6-81dc-ed94f37698b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f70a956834108c21dd7b17bb9f3e04db38f29bfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059941"
---
# <a name="data-flow-properties-that-can-be-set-by-using-expressions"></a>式を使って設定できるデータ フロー プロパティ
  データ フロー タスク コンテナーで使用できるプロパティ式を使用して、データ フロー オブジェクトの特定のプロパティの値を指定できます。  
  
 プロパティ式の使用の詳細については、「 [パッケージでプロパティ式を使用する](expressions/use-property-expressions-in-packages.md)」を参照してください。  
  
 プロパティ式を使用して、パッケージを配置するインスタンスごとに構成をカスタマイズできます。 また、コマンド プロンプト ユーティリティ **dtexec** に **/set** オプションを付けて使用すると、プロパティ式を使用してパッケージの実行時制約を指定することもできます。 たとえば、並べ替え変換で使用される `MaximumThreads`、または、あいまいグループ化変換およびあいまい参照変換の `MaxMemoryUsage` を制約できます。 制約を行わないと、これらの変換により大容量のデータがメモリ内にキャッシュされる場合があります。  
  
 このトピックに示すデータ フロー オブジェクトのプロパティの 1 つに対するプロパティ式を指定するには、デザイナーの **[制御フロー]** 画面でデータ フロー タスクを選択するか、コンポーネントやパスを個別に選択せずにデザイナーの **[データ フロー]** タブを選択して、データ フロー タスクの **[プロパティ]** ウィンドウを表示します。 **[式]** プロパティを選択し、省略記号 (...) をクリックして、 **[プロパティ式エディター]** ダイアログ ボックスを表示します。 **[プロパティ]** の一覧からプロパティを選択し、 **[式]** テキスト ボックスに式を入力するか、省略記号 (...) をクリックして **[式ビルダー]** ダイアログ ボックスを表示します。  
  
 **[プロパティ]** の一覧には、現在、デザイナーの **[データ フロー]** 画面に配置されているデータ フロー オブジェクトで使用できるプロパティのみが表示されます。 したがって、 **[プロパティ]** の一覧では、プロパティ式をサポートするデータ フロー オブジェクトのすべてのプロパティを表示することはできません。 たとえば、デザイナー画面で、ADO NET ソースを配置した場合、**プロパティ**一覧にはエントリが含まれています、`[ADO NET Source].[SqlCommand]`プロパティ。 この一覧には、データ フロー タスク自体の多数のプロパティも表示されます。  
  
## <a name="properties-of-data-flow-objects-that-support-property-expressions"></a>プロパティ式をサポートするデータ フロー オブジェクトのプロパティ  
 次の一覧にあるプロパティの値は、プロパティ式を使用して指定できます。  
  
### <a name="data-flow-sources"></a>データ フローの変換元  
  
|データ フロー オブジェクト|[プロパティ]|  
|----------------------|--------------|  
|ADO NET ソース|TableOrViewName プロパティ<br /><br /> SqlCommand プロパティ|  
|XML ソース|XMLData プロパティ<br /><br /> XMLSchemaDefinition プロパティ|  
  
### <a name="data-flow-transformations"></a>データ フロー変換  
 これらのカスタム プロパティの詳細については、「 [変換のカスタム プロパティ](data-flow/transformations/transformation-custom-properties.md)」を参照してください。  
  
|データ フロー オブジェクト|プロパティ|  
|----------------------|--------------|  
|条件分割変換|FriendlyExpression プロパティ|  
|派生列変換|FriendlyExpression プロパティ|  
|あいまいグループ化変換|MaxMemoryUsage プロパティ|  
|あいまい参照変換|MaxMemoryUsage プロパティ|  
|参照変換|SqlCommand プロパティ<br /><br /> SqlCommandParam プロパティ|  
|OLE DB コマンド変換|SqlCommand プロパティ|  
|比率サンプリング変換|SamplingValue プロパティ|  
|ピボット変換|PivotKeyValue プロパティ|  
|行サンプリング変換|SamplingValue プロパティ|  
|並べ替え変換|MaximumThreads プロパティ|  
|ピボット解除変換|PivotKeyValue プロパティ|  
  
### <a name="data-flow-destinations"></a>データ フローの変換先  
  
|データ フロー オブジェクト|プロパティ|  
|----------------------|--------------|  
|ADO NET 変換先|TableOrViewName プロパティ<br /><br /> BatchSize プロパティ<br /><br /> CommandTimeOut プロパティ|  
|フラット ファイル変換先|Header プロパティ|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 変換先|TableName プロパティ|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 変換先|BulkInsertTableName プロパティ<br /><br /> BulkInsertFirstRow プロパティ<br /><br /> BulkInsertLastRow プロパティ<br /><br /> BulkInsertOrder プロパティ<br /><br /> Timeout プロパティ|  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [プロパティ式を追加または変更する](expressions/add-or-change-a-property-expression.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 pragmaticworks.com の技術記事「 [SSIS 式チート シート](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet)」  
  
## <a name="see-also"></a>関連項目  
 [パッケージでプロパティ式を使用する](expressions/use-property-expressions-in-packages.md)   
 [共通プロパティ](../../2014/integration-services/common-properties.md)   
 [変換のカスタム プロパティ](data-flow/transformations/transformation-custom-properties.md)   
 [パスのプロパティ](../../2014/integration-services/path-properties.md)  
  
  
