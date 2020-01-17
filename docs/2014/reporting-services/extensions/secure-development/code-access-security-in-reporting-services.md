---
title: Reporting Services のコード アクセス セキュリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services]
- permission sets [Reporting Services]
- evidence [Reporting Services]
- code access security [Reporting Services], about code access security
- named permission sets [Reporting Services]
ms.assetid: 97480368-1fc3-4c32-b1b0-63edfb54e472
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3dd8d60c975efa1e0a230a08cc6b1ab1a9ce149b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62985738"
---
# <a name="code-access-security-in-reporting-services"></a>Reporting Services のコード アクセス セキュリティ
  コード アクセス セキュリティの中核を成す概念として、証拠、コード グループ、名前付き権限セットがあります。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]、レポート マネージャー、レポート デザイナー、およびレポート サーバー コンポーネントには、それぞれ、データ、配信、表示、セキュリティ拡張機能はもとより、カスタム アセンブリのコード アクセス セキュリティを設定するポリシー ファイルが存在します。 以下のセクションでは、コード アクセス セキュリティの概要について説明します。 このセクションで取り上げられているトピックの詳細については、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK ドキュメントの「セキュリティ ポリシー モデル」を参照してください。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] はコード アクセス セキュリティを使用します。その理由は、レポート サーバーは [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] テクノロジに基づき構築されているものの、一般の [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] アプリケーションとレポート サーバーの間には根本的な相違があるからです。 一般的な [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] アプリケーションはユーザー コードを実行しません。 一方、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ではオープンで拡張性のあるアーキテクチャが採用されています。これにより、ユーザーが、レポート定義言語の **Code** 要素を使用して、レポート定義ファイルを処理できるプログラムを作成すること、および特殊な機能を開発してレポートで使用するカスタム アセンブリに組み込むことが可能になります。 さらに、開発者は、レポート サーバーの能力を増強する強力な拡張機能を設計、展開できます。 この能力と柔軟性のために、最大限の防御とセキュリティが必要です。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の開発者はレポートの中で任意の [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] アセンブリを使用でき、グローバル アセンブリ キャッシュに展開されているアセンブリのすべての機能をネイティブに利用できます。 レポート サーバーによって制御されることは、レポートの式とロードされたカスタム アセンブリに与えられる権限だけです。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、カスタム アセンブリに既定で **Execute** 専用アクセス許可が与えられます。  
  
## <a name="evidence"></a>証拠  
 証拠は、共通言語ランタイム (CLR) がコード アセンブリのセキュリティ ポリシーを決定するために使用する情報です。 証拠は、コードが固有の特性を持っていることを、ランタイムに知らせます。 証拠の共通の形式には、デジタル署名やアセンブリの場所が含まれます。 証拠は、アプリケーションにとって意味のある、他の情報を表すようにカスタマイズすることもできます。  
  
 アセンブリ ドメインとアプリケーション ドメインはどちらも、証拠に基づいて権限を与えられます。 たとえば、厳密な名前を持たないアセンブリで使用される証拠の一般的な形式の 1 つに、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] がアクセスを試みているアセンブリの場所があります。 これは URL 証拠として知られています。 レポート サーバーに展開されたカスタム データ処理拡張機能の URL 証拠の一例は、"C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll" です。 アセンブリの厳密な名前またはデジタル署名もまた、証拠の一般的な形式です。 この場合、証拠はアセンブリの公開キーの情報です。  
  
## <a name="code-groups"></a>コード グループ  
 コード グループは、構成メンバーに対して条件が指定されたコードを論理的にグループ化したものです。 構成メンバーの条件を満たすコードは、すべてそのグループに含まれます。 管理者は、コード グループとそれに関連する権限セットを管理することによって、セキュリティ ポリシーを構成します。  
  
 コード グループの構成メンバーの条件は証拠に基づいています。 たとえば、コード グループの URL 構成メンバーは URL 証拠に基づいています。 共通言語ランタイム (CLR) では、URL 証拠のような識別特性を使用して、コードを記述し、グループの構成メンバー条件が満たされているかどうかを判定します。 たとえば、コード グループの構成メンバー条件が、"code in the assembly C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll" の場合、ランタイムは証拠を調べて、コードがその場所からのコードかどうかを判定します。 たとえば、この種のコード グループの構成のエントリは次のように記述されています。  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="FullTrust"  
   Name="MyCodeGroup"  
   Description="Code group for my data processing extension">  
      <IMembershipCondition class="UrlMembershipCondition"  
         version="1"  
         Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll"  
       />  
</CodeGroup>  
```  
  
 システム管理者またはアプリケーション展開の専門家と協力して、カスタム アセンブリまたは [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の拡張機能が必要とする、コード アクセス セキュリティとコード グループの種類を決定する必要があります。  
  
## <a name="named-permission-sets"></a>名前付き権限セット  
 名前付き権限セットは、管理者がコード グループに関連付けることができる権限のセットです。 ほとんどの名前付き権限セットは、少なくとも、1 つの権限、名前、および権限セットの説明から構成されます。 管理者は、名前付き権限セットを使用して、コード グループのセキュリティ ポリシーを作成または変更できます。 複数のコード グループを同じ名前付き権限セットに関連付けることができます。 CLR には、**Nothing**、**Execution**、**Internet**、**LocalIntranet**、**Everything**、**FullTrust** などの、組み込みの名前付きアクセス許可セットが用意されています。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のカスタム データ、配信、表示、およびセキュリティの拡張機能は、**FullTrust** アクセス許可セットの下で実行する必要があります。 システム管理者と協力して、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 拡張機能の適切なコード グループと構成メンバー条件を追加します。  
  
 使用するカスタム アセンブリに対する自身のカスタム権限レベルを、レポートに関連付けることができます。 たとえば、アセンブリが特定のファイルにアクセスする場合、その特定のファイルに対する I/O アクセスを許可する名前付き権限セットを作成し、その権限セットをコード グループに割り当てます。 次の権限セットは、ファイル MyFile.xml に対する読み取り専用のアクセスを許可します。  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="MyNewFilePermissionSet"  
   Description="A special permission set that grants read access to my file.">  
    <IPermission class="FileIOPermission"  
       version="1"  
       Read="C:\MyFile.xml"/>  
    <IPermission class="SecurityPermission"  
       version="1"  
       Flags="Assertion, Execution"/>  
</PermissionSet>  
```  
  
 この権限セットが付与されるコード グループは次のようになります。  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="MyNewFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\MyCustomAssembly.dll"/>  
</CodeGroup>  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティで保護された開発 &#40;Reporting Services&#41;](secure-development-reporting-services.md)  
  
  
