---
title: データ ソースの非時間テーブルを生成することで、ディメンションの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 962df497e804011e69e2a350c24ce41f4c273b6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076436"
---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>データ ソースに時間テーブル以外のテーブルを生成することによるディメンションの作成
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のディメンション ウィザードを使用して、既存のデータ ソースを使用せずにディメンションを作成できます。 この操作を行うには、ウィザードの **[作成方法の選択]** ページで **[データ ソースに時間テーブル以外のテーブルを生成]** オプションを選択します。 基になるデータ ソースに新しいディメンション テーブルを作成するには、基になるデータ ソースにオブジェクトを作成する権限が必要です。 定義済みのデータ ソース ビューを使用せずにディメンションを定義する場合、ディメンションを最初から定義することも、ディメンション テンプレートを使用することもできます。  
  
 ディメンション ウィザードで提供されるサンプルのディメンション テンプレートから、一般的に使用される種類のディメンションを構築できます。 次のディメンションの種類から選択できます。  
  
-   アカウント  
  
-   Customer  
  
-   date  
  
-   Department  
  
-   Destination Currency  
  
-   Employee  
  
-   Geography  
  
-   Internet Sales Order Details  
  
-   Organization  
  
-   製品  
  
-   Promotion  
  
-   Reseller Sales Order Details  
  
-   Reseller  
  
-   Sales Channel  
  
-   Sales Reason  
  
-   Sales Summary Order Details  
  
-   Sales Territory  
  
-   シナリオ  
  
-   Source Currency  
  
 それぞれの標準テンプレートでは、ディメンションに含めるように選択できる属性がサポートされています。 また、データでよく使用するディメンションの独自のテンプレート ファイルを追加することもできます。 ディメンション テンプレートは次のフォルダーにあります。  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 ディメンション ウィザードを完了した後、ディメンション デザイナーを使用して、ディメンションの属性と階層を追加、削除、および設定できます。  
  
 データ ソースを使用せずに時間ディメンション以外のディメンションを作成している場合、ディメンション ウィザードでは、ディメンションの種類を指定し、キー属性と緩やかに変化するディメンションを識別する手順が示されます。  
  
## <a name="specify-dimension-type"></a>ディメンションの種類の指定  
 ディメンション ウィザードの **[ディメンションの種類を指定]** ページでは、ディメンションの種類を指定できます。 テンプレートを基にディメンションを構築している場合、ディメンションの種類は自動的に定義されます。 このページでは、指定したディメンションの種類に標準的な属性があれば、選択することもできます。  
  
 ディメンションの種類に対応するテンプレートを選択した場合は、そのディメンションの種類のオプションでこのページが作成されます。 テンプレートを選択しなかった場合や、該当するディメンションの種類がない場合、既定のディメンションの種類は **[標準]** です。 ディメンションの種類がまだ選択されていない場合は、作成するディメンションに最適な種類を選択します。 適切な種類が **[ディメンションの種類]** の一覧に表示されていない場合は、 **[標準]** を使用します。  
  
 ディメンションの種類を選択すると、そのディメンションに適用する属性の型が **[ディメンションの属性]** ボックスの一覧に表示されます。 属性の型を選択するには、属性の型の横にある **[追加]** チェック ボックスをオンにし、 **[ディメンションの属性]** で属性名を入力します。 既定の名前は、 **[属性の型]** の値と同じです。  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>キー属性と変化するディメンションの識別  
 **[ディメンションのキーおよび種類を指定]** ページで、ディメンションのキー属性とする属性を選択します。 通常、キー属性はメイン ディメンション テーブルの主キー列に対応しており、ディメンションのリーフ メンバーのインデックスを作成します。  
  
 テンプレートを選択しており、そのテンプレートでキー属性が定義されている場合は、その属性が既定のキー属性となります。 テンプレートを選択しても、そのテンプレートでキー属性が定義されていない場合は、一覧の先頭の属性が既定となります。 この一覧には、 **[ディメンションの種類を指定]** ページで選択したすべての属性が含まれます。 **[ディメンションの種類を指定]** ページで選択したどの属性も、キー属性に選択できます。 属性を選択しなかった場合は、ウィザードによってキー属性が自動的に作成され、ディメンション名と "ID" を連結した名前が付けられます。  
  
 最後に、このディメンションが変化するディメンションかどうかを指定します。 変化するディメンションのメンバーは、時間の経過と共に階層内の別の場所に移動します。 ウィザードでは、追加の列が生成され、それらの列に対応する属性が作成されます。 こうした列を使用すると、ユーザーは、変更を考慮してディメンションに対するクエリを実行できます。 スキーマ生成ウィザードを使用して後で作成するパッケージでは、緩やかに変化するディメンションの特性に基づき、代理キーが管理されます。  
  
 **[変化するディメンション]** チェック ボックスをオンにすると、ディメンション ウィザードでは、次の表に示す属性が定義されます。  
  
|属性|型|  
|---------------|----------|  
|SCD のオリジナル ID|SCDOriginalID|  
|SCD の終了日|SCDEndDate|  
|SCD の開始日|SCDStartDate|  
|SCD ステータス|SCDStatus|  
  
 既定では、緩やかに変化するディメンションのこれらの属性が定義されているテンプレートを使用する場合、 **[変化するディメンション]** チェック ボックスがオンになっています。 チェック ボックスをオフにすると、緩やかに変化するディメンション属性はディメンションから削除されます。  
  
 ディメンション デザイナーを使用すると、緩やかに変化するディメンションのプロパティを構成できます。  
  
## <a name="completing-the-dimension-wizard"></a>ディメンション ウィザードの完了  
 **[ウィザードの完了]** ページで、新しいディメンションの名前を入力し、ディメンション構造を表示します。 **[完了]** をクリックした後にスキーマ生成ウィザードを開始するには、 **[今すぐスキーマを生成する]** チェック ボックスをオンにします。 追加オブジェクトを作成する計画がある場合は、このチェック ボックスはオンにしないでください。 このチェック ボックスを選択しない場合は、ディメンション デザイナーを使用して後でスキーマを作成できます。  
  
## <a name="see-also"></a>参照  
 [Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md)   
 [Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md)  
  
  
