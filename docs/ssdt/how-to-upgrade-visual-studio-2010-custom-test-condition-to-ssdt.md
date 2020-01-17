---
title: 方法:Visual Studio 2010 のカスタム テスト条件を、以前のリリースから SQL Server Data Tools にアップグレードする | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 44c895a3-dee0-4032-a60f-812f5fe3c713
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2b46be709cb14ff9105bcfbcacd65bc32af8de77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035002"
---
# <a name="how-to-upgrade-a-visual-studio-2010-custom-test-condition-from-a-previous-release-to-sql-server-data-tools"></a>方法:Visual Studio 2010 のカスタム テスト条件を、以前のリリースから SQL Server Data Tools にアップグレードする
SQL Server Data Tools より前のバージョンで作成したテスト条件を使用するには、次のようにアップグレードする必要があります。  
  
-   [参照を更新する](#UpdateReferences)  
  
-   [クラス属性と型参照を更新する](#UpdateClassAttributesandTypeReference)  
  
-   [アップグレード済みのテスト条件をインストールする](#ApplytheNewRegistrationProcess)  
  
## <a name="UpdateReferences"></a>参照を更新する  
プロジェクトの参照を更新するには、次の手順を実行します。  
  
1.  Visual Basic のみで、**ソリューション エクスプローラー**で、 **[すべてのファイルを表示]** をクリックします。  
  
2.  **ソリューション エクスプローラー**で、 **[参照]** ノードを展開します。  
  
3.  次のアセンブリ参照を右クリックし、 **[削除]** をクリックします。  
  
    1.  Microsoft.Data.Schema.UnitTesting  
  
    2.  Microsoft.Data.Schema  
  
4.  **[プロジェクト]** メニューをクリックするか、または**ソリューション エクスプローラー**のプロジェクト フォルダーを右クリックして、 **[参照の追加]** をクリックします。  
  
5.  **[.NET]** タブをクリックします。  
  
6.  **[コンポーネント名]** の一覧で **System.ComponentModel.Composition** を選択し、 **[OK]** をクリックします。  
  
7.  必要なアセンブリ参照を追加します。 プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。 **[参照]** をクリックし、C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin フォルダーに移動します。 Microsoft.Data.Tools.Schema.Sql.dll を選択し、[追加] をクリックして、[OK] をクリックします。  
  
8.  **[プロジェクト]** メニューの **[プロジェクトのアンロード]** をクリックします。  
  
9. **ソリューション エクスプローラー**で**プロジェクト**を右クリックして、 **[** `project_name` **.csproj の編集]** をクリックします。  
  
10. `Microsoft.CSharp.targets` をインポートした後、次の Import ステートメントを追加します。  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
11. ファイルを保存して閉じます。 **ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[プロジェクトの再読み込み]** をクリックします。  
  
12. テスト条件クラスを開き、**Microsoft.Data.Schema** で始まるすべての using ステートメントを削除します。 この操作を最も簡単に行うには、ファイルを右クリックして、 **[using の整理]** を選択し、 **[削除および並べ替え]** を選択します。 次の using ステートメントを削除する必要があります。  
  
    ```  
    using Microsoft.Data.Schema.UnitTesting;  
    using Microsoft.Data.Schema.UnitTesting.Conditions;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema;  
    ```  
  
13. 次の using ステートメントがない場合は、ファイルに追加します。  
  
    ```  
    using System.ComponentModel;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
    ```  
  
これで、テスト条件では SQL Server 単体テストのアセンブリ参照を使用するようになりました。  
  
## <a name="UpdateClassAttributesandTypeReference"></a>クラス属性と型参照を更新する  
古い単体テストのクラス属性を新しい属性に置き換えます。 SQL Server 単体テストの機能拡張は、Managed Extensibility Framework (MEF) に基づいて作成されるようになりました。 また、いくつかの型参照も更新する必要があります。  
  
### <a name="update-class-attributes"></a>クラス属性を更新する  
次のようにコードを更新します。  
  
1.  `DatabaseSchemaProviderCompatibility` 属性を削除します。 これ (これら) は、以前のバージョンの拡張機能に必要な属性で、SQL Server 単体テストではサポートされていません。  
  
2.  `DisplayName` 属性を削除してください。 表示名は新しい属性に含まれます。  
  
3.  新しい `ExportTestCondition` 属性を追加します。 この属性は、テスト条件を SQL Server 単体テストで検出して使用するために必要です。 `ExportTestCondition` は、`DatabaseSchemaProviderCompatibility` 属性に置き換わります。 `ExportTestCondition` には、2 つのパラメーターがあります。  
  
    -   最初のパラメーターは、`DisplayName` です。 これは、`DisplayName` 属性に代わって、この型のすべてのテスト条件を記述するのに使用されます。  
  
    -   2 つ目のパラメーターは、拡張機能を一意に識別するために使用されます。 これは一意であるため、単に `typeof(NewTestCondition)` を使用して型を渡すことができます。 ただし、必要に応じて、文字列 ID を渡すこともできます。  
  
4.  クラス定義は、次のように変更されます。  
  
    次の処理の前  
  
    ```  
    [DatabaseSchemaProviderCompatibility(typeof(DatabaseSchemaProvider))]  
    [DatabaseSchemaProviderCompatibility(null)]  
    [DisplayName("NewTestCondition")]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
    次の処理の後  
  
    ```  
    [ExportTestCondition("NewTestCondition ", typeof(NewTestCondition))]  
    public class NewTestCondition:TestCondition  
    {  
       // Additional implementation to be added here  
    }  
    ```  
  
### <a name="update-type-references"></a>型参照を更新する  
SQL Server 単体テスト フレームワークでは、いくつかの型名が変更されました。 新しい型名を使用するようにコードを更新するには、 **[編集]** メニューの **[検索と置換]** を使用します。 型名は、**Sql** で始まるようになりました。 クラス名は次のように更新されました。  
  
|以前の型名|新しい型名|  
|-----------------|-----------------|  
|`ExecutionResult`|`SqlExecutionResult`|  
  
## <a name="ApplytheNewRegistrationProcess"></a>アップグレード済みのテスト条件をインストールする  
以前のバージョンのデータベース単体テストでは、テスト条件の情報をグローバル アセンブリ キャッシュにインストールするか、アセンブリ情報を含む XML ファイルを作成することが要求される場合がありました。 SQL Server 単体テストでは、この追加の処理が必要なくなりました (詳しくは、「[プロジェクトをコンパイルしてテスト条件をインストールする](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md#xxx)」をご覧ください。  
  
参照を更新したら、アセンブリが署名され、コンパイルされていることを確認します。  
  
次に、アセンブリ ファイルを出力ディレクトリ (既定では、My Documents\Visual Studio 2010\Projects\\<yoursolutionname>\\<yourprojectname>\bin\Debug\\) から %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions ディレクトリにコピーします。 Visual Studio の起動時に、TestConditions ディレクトリ内のすべての拡張機能が認識され、セッションで使用できるようになります。  
  
## <a name="upgrade-existing-tests-that-need-to-use-the-new-test-condition"></a>新しいテスト条件を使用する必要がある既存のテストをアップグレードする  
以前のテスト条件を使用していて、新しい条件を使用する必要があるテスト プロジェクトをすべて探します。 これらのテスト プロジェクトがアップグレードされるようにします。 詳しくは、「[データベース単体テストを含む以前のテスト プロジェクトをアップグレードする](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md)」をご覧ください。  
  
以前のテスト条件へのアセンブリ参照を削除します。  
  
新しい SQL Server 単体テストをプロジェクトに追加し、プロジェクト内のアップグレードされたテスト条件へのアセンブリ参照を作成します。 参照を作成するには、テスト クラスの追加が必要です。 参照を追加したら、このテスト クラスは削除してかまいません。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストのカスタム テスト条件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
