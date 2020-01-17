---
title: 式で使用される組み込みコレクション (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e572e6bd7070247c8e872283964f50ad734d4e32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106422"
---
# <a name="built-in-collections-in-expressions-report-builder-and-ssrs"></a>式で使用される組み込みコレクション (レポート ビルダーおよび SSRS)
  レポートの式には、次の組み込みコレクションへの参照を含めることができます:ReportItems、Parameters、Fields、DataSets、DataSources、Variables。また、レポート名などのグローバル情報の組み込みフィールドを含めることができます。 **[式]** ダイアログ ボックスにすべてのコレクションが表示されるとは限りません。 DataSets コレクションと DataSources コレクションを使用できるのは、レポート サーバー上でパブリッシュされたレポートの実行時のみです。 ReportItems コレクションは、ページまたはページ ヘッダーのテキスト ボックスなど、レポート領域内のテキスト ボックスのコレクションです。  
  
 詳細については、「[式 (レポート ビルダーおよび SSRS)](expressions-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Collections"></a> 組み込みコレクションについて  
 次の表は、式を記述するときに使用できる組み込みコレクションの一覧です。 各行に、プログラム上のコレクション名 (大文字と小文字は区別されます)、[式] ダイアログ ボックスを使用してコレクションへの参照を対話的に追加できるかどうか、使用例、および説明 (コレクションの値がいつ初期化され使用できるようになるかなど) を示します。  
  
|組み込みコレクション|[式] ダイアログ ボックスのカテゴリ|例|説明|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|`Globals`|組み込みフィールド|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|レポート名またはページ番号など、レポートで役立つグローバル変数を表します。 常に使用可能です。<br /><br /> 詳細については、「[組み込み Globals および Users 参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md)」をご覧ください。|  
|`User`|組み込みフィールド|`=User.UserID`<br /><br /> - または -<br /><br /> `=User.Language`|言語設定やユーザー ID など、レポートを実行しているユーザーに関するデータのコレクションを表します。 常に使用可能です。<br /><br /> 詳細については、「[組み込み Globals および Users 参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md)」をご覧ください。|  
|`Parameters`|パラメーター|`=Parameters("ReportMonth").Value`<br /><br /> - または -<br /><br /> `=Parameters!ReportYear.Value`|レポート パラメーターのコレクションを表します。各パラメーターには単一値または複数値を指定できます。 初期化処理が完了するまで使用できません。 詳細については、「[Parameters コレクションの参照 (レポート ビルダーおよび SSRS)](built-in-collections-parameters-collection-references-report-builder.md)」を参照してください。|  
|`Fields(` *\<データセット >* `)`|フィールド|`=Fields!Sales.Value`|レポートで使用可能なデータセットのフィールドのコレクションを表します。 データをデータ ソースからデータセットに取得した後で使用可能です。 詳細については、「[データセット フィールド コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-dataset-fields-collection-references-report-builder.md)」を参照してください。|  
|`DataSets`|表示されません|`=DataSets("TopEmployees").CommandText`|レポート定義の本文から参照されるデータセットのコレクションを表します。 ページ ヘッダーまたはページ フッターでのみ使用されるデータ ソースは含まれません。 ローカル プレビューでは使用できません。 詳細については、「[DataSources コレクションと DataSets コレクションの参照 (レポート ビルダーおよび SSRS)](built-in-collections-datasources-and-datasets-references-report-builder.md)」を参照してください。|  
|`DataSources`|表示されません|`=DataSources("AdventureWorks2012").Type`|レポートの本文内から参照されるデータ ソースのコレクションを表します。 ページ ヘッダーまたはページ フッターでのみ使用されるデータ ソースは含まれません。 ローカル プレビューでは使用できません。 詳細については、「[DataSources コレクションと DataSets コレクションの参照 (レポート ビルダーおよび SSRS)](built-in-collections-datasources-and-datasets-references-report-builder.md)」を参照してください。|  
|`Variables`|`Variables`|`=Variables!CustomTimeStamp.Value`|レポート変数とグループ変数のコレクションを表します。 詳細については、「[レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS)](built-in-collections-report-and-group-variables-references-report-builder.md)」を参照してください。|  
|`ReportItems`|表示されません|`=ReportItems("Textbox1").Value`|レポート アイテムのテキスト ボックスのコレクションを表します。 このコレクションは、ページ ヘッダーまたはページ フッターに含めるためにページ上のアイテムをまとめる場合に使用できます。 詳細については、「[ReportItems コレクションの参照 (レポート ビルダーおよび SSRS)](built-in-collections-reportitems-collection-references-report-builder.md)」を参照してください。|  
  
##  <a name="Syntax"></a> 式でのコレクション構文の使用  
 式からコレクションを参照するには、コレクション内のアイテムに対して標準の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 構文を使用します。 次の表に、コレクション構文の例を示します。  
  
|構文|例|  
|------------|-------------|  
|*Collection!ObjectName.Property*|`=Fields!Sales.Value`|  
|*Collection!ObjectName("Property")*|`=Fields!Sales("Value")`|  
|*Collection("ObjectName").Property*|`=Fields("Sales").Value`|  
|*Collection("Member")*|`=User("Language")`|  
|*Collection.Member*|`=User.Language`|  
  
## <a name="see-also"></a>関連項目  
 [式の追加 (レポート ビルダーおよび SSRS)](add-an-expression-report-builder-and-ssrs.md)   
 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
