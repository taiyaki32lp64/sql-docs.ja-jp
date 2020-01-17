---
title: Reporting Services セキュリティ ポリシー ファイルの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- code groups [Reporting Services]
- CodeGroup elements
- configuration files [Reporting Services]
- code access security [Reporting Services], security policies
- security policies [Reporting Services]
- security configuration files [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: 2280fff6-3de7-44b1-87da-5db0ec975928
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ee7ba55e48f4704c912e92a4d8352e7c891c06b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62989674"
---
# <a name="using-reporting-services-security-policy-files"></a>Reporting Services セキュリティ ポリシー ファイルの使用
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、セットアップ時にファイル システムにコピーされる 3 つの構成ファイルにコンポーネントのセキュリティ ポリシーを格納します。 これらの構成ファイルには、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のコード アセンブリについて、内部用セキュリティ ポリシーとユーザー定義セキュリティ ポリシーの組み合わせを含めることができます。 3 つの構成ファイルで次の 3 つのセキュリティ保護可能なコンポーネントに対応[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]:レポート サーバーと Windows サービス、レポート マネージャー Web アプリケーション、およびレポート デザイナーのウィンドウをプレビューします。  
  
> [!NOTE]  
>  レポート デザイナーには 2 種類のプレビュー モードがあります。1 つは [プレビュー] タブ、もう 1 つは、レポート プロジェクトを **DebugLocal** モードで開始したときに起動されるポップアップ プレビュー ウィンドウです。 **[プレビュー]** タブはセキュリティ保護可能なコンポーネントではなく、セキュリティ ポリシー設定が適用されません。 レポート サーバー機能のシミュレーションを目的としているプレビュー ウィンドウには、ポリシー構成ファイルが備わっています。レポート デザイナーでカスタム アセンブリやカスタム拡張機能を使用する場合、ユーザーまたは管理者はこの構成ファイルを変更する必要があります。  
  
 セキュリティ ポリシー構成ファイルには、セキュリティ クラス情報、一部の既定の名前付き権限セット、および [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のアセンブリで使用するコード グループが含まれています。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のポリシー構成ファイルは Security.config ファイルと似ており、[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] のコンピューター レベル ポリシーおよびエンタープライズ レベル ポリシーに基づいてコード グループ階層と権限セットを決定します。 このファイルの場所は、C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\CONFIG\security.config です。  
  
## <a name="policy-files-in-reporting-services"></a>Reporting Services のポリシー ファイル  
 次の表は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のポリシー構成ファイル、既定インストールでの場所、および各機能を示しています。  
  
|ファイル名|場所 (既定インストール)|説明|  
|---------------|---------------------------------------|-----------------|  
|rssrvpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer|レポート サーバーのポリシー構成ファイル。 これらのセキュリティ ポリシーは、レポートがレポート サーバーに配置された後のレポートの式とカスタム アセンブリに主に影響します。 このポリシー ファイルは、カスタム データ、配信、表示、およびレポート サーバーに配置されるセキュリティ拡張機能にも影響します。|  
|rsmgrpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager|レポート マネージャーのポリシー構成ファイル。 これらのセキュリティ ポリシーは、カスタム配信用のサブスクリプション ユーザー インターフェイス拡張機能など、レポート マネージャーを拡張するすべてのアセンブリに影響します。|  
|rspreviewpolicy.config|C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies|レポート デザイナーのスタンドアロン プレビュー ポリシー構成ファイル。 これらのセキュリティ ポリシーは、プレビューおよび開発中にレポートに使用するカスタム アセンブリとレポートの式に影響します。 これらのポリシーは、レポート デザイナーに配置されるデータ処理拡張機能などのカスタム拡張機能にも影響します。|  
  
## <a name="modifying-configuration-files"></a>構成ファイルの変更  
 構成設定は、XML 要素または XML 属性のいずれかとして指定されます。 XML ファイルおよび構成ファイルを理解している場合は、テキスト エディターまたはコード エディターを使用して、ユーザーが定義可能な設定を変更できます。 セキュリティ構成ファイルには、コード グループ階層構造に関する情報と、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のポリシー レベルに関連付けたアクセス許可セットを含めます。 最初に Security.config ファイルのセキュリティ ポリシーを変更する場合は、.NET Framework 構成ユーティリティ (Mscorcfg.msc) またはコード アクセス セキュリティ ポリシー ユーティリティ (Caspol.exe) を使用して、ポリシーの変更をポリシー ファイルの有効な XML 構成要素に対応させることをお勧めします。 その後で、新しいコード グループと権限セットを Security.config から切り取って、コードと権限追加先のコンポーネントのポリシーに貼り付けることができます。  
  
> [!IMPORTANT]  
>  ポリシー構成ファイルをバックアップした後で変更を行ってください。  
  
 この方法を実行すると、2 つの結果が得られます。 まず、仮想ツールを使用して [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] にコード グループと権限セットを構築できます。 最初から XML 構成ファイル要素を記述するよりもこの方がはるかに簡単です。 次に、不適切な形式の XML 要素と属性によってセキュリティ ポリシー構成ファイルが破損することがありません。 コード アクセス セキュリティ ポリシー ユーティリティの詳細については、MSDN の「Reporting Services セキュリティ ポリシー ファイルの使用」を参照してください。  
  
 ポリシー構成ファイルを変更する前に、このセクションおよび関連項目で入手できるすべての情報を読んでおく必要があります。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のポリシー構成ファイルを変更すると、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] コンポーネントによる外部コード モジュール実行にセキュリティ上の重大な影響を及ぼす可能性があります。  
  
## <a name="placement-of-codegroup-elements-for-extensions"></a>拡張機能の CodeGroup 要素の配置  
 セキュリティ ポリシー ファイル内の CodeGroup 要素の配置は重要です。 開発した拡張機能とカスタム アセンブリの場合は、次のように URL メンバーシップ "$CodeGen$/*" の既存エントリのすぐ下にカスタム コード グループを配置することをお勧めします。  
  
```  
<CodeGroup  
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust">  
    <IMembershipCondition   
        class="UrlMembershipCondition"  
        version="1"  
        Url="$CodeGen$/*"  
    />  
</CodeGroup>  
<CodeGroup   
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust"  
    Name="MyCustomCodeGroup"  
    Description="Code group for my custom extension">  
        <IMembershipCondition class="UrlMembershipCondition"  
        version="1"  
        Url="C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer\bin\MyAssembly.dll"  
        />  
</CodeGroup>  
```  
  
 コード グループを順次追加できます。  
  
## <a name="see-also"></a>参照  
 [セキュリティ ポリシーの概要](understanding-security-policies.md)  
  
  
