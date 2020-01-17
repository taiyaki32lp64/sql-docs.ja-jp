---
title: パッケージの構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package configuration syntax [Integration Services]
- SQL Server Integration Services packages, configurations
- SSIS packages, configurations
- XML [Integration Services]
- Integration Services packages, configurations
- configuration syntax [Integration Services]
- indirect configurations [Integration Services]
- configurations [Integration Services]
- direct configurations [Integration Services]
- packages [Integration Services], configurations
ms.assetid: d20e0311-1fc9-4ddc-a381-6d127cf11b69
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c220fc87f726d8ba3d8e8cc92904ce42e3baeb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056892"
---
# <a name="package-configurations"></a>[パッケージ構成]
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、プロパティの値を実行時に更新するためのパッケージ構成が用意されています。  
  
> [!NOTE]  
>  パッケージ配置モデルの構成を使用できます。 パラメーターは、プロジェクト配置モデルの構成の代わりに使用します。 プロジェクト配置モデルを使用すると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを配置できます。 配置モデルの詳細については、「 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
 1 つの構成は、完了した状態のパッケージに追加するプロパティと値のペアで定義されます。 通常、パッケージの開発中にパッケージ オブジェクトにプロパティを設定したパッケージを作成し、そのパッケージに構成を追加します。 パッケージの実行時に、構成からこのプロパティの新しい値を取得します。 たとえば、構成を使用して、接続マネージャーの接続文字列を変更したり、変数の値を更新したりできます。  
  
 パッケージの構成には、次のような利点があります。  
  
-   構成を使用すると、開発環境から運用環境へのパッケージの移行が容易になります。 たとえば、ある構成を使用して、ソース ファイルのパスを更新したり、データベースやサーバーの名前を変更したりできます。  
  
-   構成は、パッケージを多くの異なるサーバーに配置する場合に便利です。 たとえば、配置されたパッケージごとの構成の変数に、異なるディスク容量値を格納できます。また、使用できるディスク容量がこの値に満たない場合、パッケージは実行されません。  
  
-   構成を使用すると、パッケージの柔軟性が高まります。 たとえば、構成を使用すると、プロパティ式に使用されている変数の値を更新できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、XML ファイル、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベース内のテーブル、および環境変数およびパッケージ変数など、パッケージ構成を格納するための複数の異なる方法がサポートされています。  
  
 それぞれの構成は、プロパティと値のペアで定義されます。 XML 構成ファイルと [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成の種類には、複数の構成を含めることができます。  
  
 構成は、パッケージをインストールするためのパッケージ配置ユーティリティを作成したときに追加されます。 パッケージをインストールするときに、パッケージのインストールの 1 つの手順として構成を更新できます。  
  
## <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>実行時にパッケージ構成が適用されるしくみについて  
 **dtexec** コマンド プロンプト ユーティリティ (dtexec.exe) を使用して配置されたパッケージを実行する場合、パッケージ構成が 2 回適用されます。 コマンド ラインで指定したオプションの適用前と適用後の両方に構成が適用されます。  
  
 パッケージを読み込んで実行すると、次の順序でイベントが発生します。  
  
1.  **dtexec** ユーティリティでパッケージが読み込まれます。  
  
2.  デザイン時にパッケージに指定された構成が、パッケージに指定されている順序で適用されます (唯一の例外は、親パッケージ変数の構成です。 これらの構成は後から一度だけ適用されます)。  
  
3.  次に、コマンド ラインで指定したすべてのオプションが適用されます。  
  
4.  デザイン時にパッケージに指定された構成が、パッケージに指定されている順序で再読み込みされます (この場合も唯一の例外は、親パッケージ変数の構成です)。 指定されたすべてのコマンド ライン オプションを使用して構成が再読み込みされます。 したがって、異なる値が異なる場所から再読み込みされる可能性があります。  
  
5.  親パッケージ変数の構成が適用されます。  
  
6.  パッケージが実行されます。  
  
 **dtexec** ユーティリティでの構成の適用方法は、次のコマンド ライン オプションに影響します。  
  
-   実行時に **/Connection** または **/Set** オプションを使用すると、デザイン時に指定した場所とは別の場所からパッケージ構成を読み込むことができます。  
  
-   **/ConfigFile** オプションを使用すると、デザイン時に指定しなかった追加の構成を読み込むことができます。  
  
 ただし、これらのコマンド ライン オプションには制限事項がいくつかあります。  
  
-   **/Set** または **/Connection** オプションを使用して、構成で設定されている単一の値をオーバーライドすることはできません。  
  
-   **/ConfigFile** オプションを使用して、デザイン時に指定した構成を置き換える構成を読み込むことはできません。  
  
 これらのオプションとの間での動作のこれらのオプションの違いの詳細については[!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)]以前のバージョンを参照してくださいと[SQL Server 2014 Integration Services 機能の動作の変更](../../2014/integration-services/behavior-changes-to-integration-services-features-in-sql-server-2014.md)します。  
  
## <a name="package-configuration-types"></a>パッケージの構成の種類  
 パッケージの構成の種類を次の表に示します。  
  
|型|説明|  
|----------|-----------------|  
|XML 構成ファイル|XML ファイルに構成を格納します。 XML ファイルは、複数の構成を格納できます。|  
|環境変数|環境変数に構成を格納します。|  
|レジストリ エントリ|レジストリ エントリに構成を格納します。|  
|親パッケージ変数|パッケージの変数に構成を格納します。 通常、この構成の種類は、子パッケージ内のプロパティを更新するために使用されます。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブル|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベース内のテーブルに構成を格納します。 テーブルは、複数の構成を格納できます。|  
  
### <a name="xml-configuration-files"></a>XML 構成ファイル  
 構成の種類として **[XML 構成ファイル]** を選択した場合は、新しい構成ファイルを作成したり、既存のファイルを再利用して新しい構成を追加できます。また、既存のファイルを再利用しながら既存のファイルの内容を上書きすることもできます。  
  
 XML 構成ファイルには、2 つのセクションがあります。  
  
-   この構成ファイルに関する情報が記載された見出し。 この要素には、ファイルの作成日やファイルの作成者の名前などの属性があります。  
  
-   それぞれの構成に関する情報が格納された構成要素。 この要素には、プロパティ パスやプロパティの構成値などの属性があります。  
  
 次の XML コードは、XML 構成ファイルの構文を示しています。 この例では、 `MyVar`という名前の整数変数の Value プロパティの構成を示します。  
  
```  
<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
### <a name="registry-entry"></a>レジストリ エントリ  
 レジストリ エントリを使用して構成を格納する場合は、既存のキーを使用するか、HKEY_CURRENT_USER で新しいキーを作成できます。 使用するレジストリ キーには、`Value` という名前の値が必要です。 この値には、DWORD または文字列を指定できます。  
  
 構成の種類として **[レジストリ エントリ]** を選択した場合は、[レジストリ エントリ] ボックスにレジストリ キーの名前を入力します。 形式は \<registry key> です。 HKEY_CURRENT_USER のルートにないレジストリ キーを使用する場合は、\<Registry key\registry key\\...> の形式を使用してキーを識別します。 たとえば、SSISPackages にある MyPackage キーを使用する場合は、「`SSISPackages\MyPackage`」と入力します。  
  
### <a name="sql-server"></a>SQL Server  
 構成の種類として **[SQL Server]** を選択した場合は、構成を格納する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースへの接続を指定します。 構成は、既存のテーブルに保存することも、指定したデータベース内に新しいテーブルを作成して保存することもできます。  
  
 次の SQL ステートメントは、パッケージ構成ウィザードで提供される既定の CREATE TABLE ステートメントを示しています。  
  
```  
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 構成に指定される名前は、 **ConfigurationFilter** 列に格納されている値です。  
  
## <a name="direct-and-indirect-configurations"></a>直接構成および間接構成  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、直接構成と間接構成があります。 構成を直接指定した場合、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] は、構成アイテムとパッケージ オブジェクト プロパティとの間に直接リンクを作成します。 直接構成は、ソースの位置が変化しない場合に適しています。 たとえば、パッケージ内のすべての配置で同じファイル パスが必ず使用される場合は、XML 構成ファイルを指定できます。  
  
 間接構成では、環境変数が使用されます。 構成設定を直接指定する代わりに、構成値を格納する環境変数が指定されます。 間接構成は、パッケージのそれぞれの配置に対して構成の位置が変更される可能性がある場合に適しています。  
  
## <a name="related-tasks"></a>Related Tasks  
 [パッケージ構成を作成する](../../2014/integration-services/create-package-configurations.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   msdn.microsoft.com の技術記事「 [Integration Services パッケージ構成について](https://go.microsoft.com/fwlink/?LinkId=165643)」  
  
-   ブログ エントリ「[コード - パッケージ構成でパッケージを作成する](https://go.microsoft.com/fwlink/?LinkId=217663)、www.sqlis.com にします。  
  
-   ブログ エントリ「 [API のサンプル - がプログラムによって構成ファイル パッケージに追加](https://go.microsoft.com/fwlink/?LinkId=217664)、blogs.msdn.com します。  
  
  
