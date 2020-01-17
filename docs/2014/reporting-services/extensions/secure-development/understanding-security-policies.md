---
title: セキュリティ ポリシーの概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services], security policies
- Execution permission set
- custom assemblies [Reporting Services], security
- permission sets [Reporting Services]
- expressions [Reporting Services], security
- evidence [Reporting Services]
- FullTrust permission set
- security policies [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: a9bf043a-139a-4929-9a58-244815323df0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fb69c4b064329b53f9ab3efef62f0d1c54b897a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990129"
---
# <a name="understanding-security-policies"></a>セキュリティ ポリシーの概要
  レポート サーバーが実行するすべてのコードは、特定のコード アクセス セキュリティ ポリシーの一部である必要があります。 これらのセキュリティ ポリシーは、証拠と名前付き権限セットとを対応付けるコード グループで構成されます。 多くの場合、コード グループは、そのグループ内のコードに対して与えることのできる権限が指定された名前付き権限セットに関連付けられます。 ランタイムは、信頼されるホストまたはローダーが提供した証拠を使用して、コードが属するコード グループ、およびコードに付与された権限を確認します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] の共通言語ランタイム (CLR) によって定義された、このセキュリティ ポリシー アーキテクチャに準拠します。 ここでは、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の各種コードおよび関連付けられたポリシー ルールについて説明します。  
  
## <a name="report-server-assemblies"></a>レポート サーバーのアセンブリ  
 レポート サーバーのアセンブリには、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 製品の一部であるコードが含まれています。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] はマネージド コード アセンブリを使用して記述されています。これらのアセンブリにはすべて厳密な名前が付けられています。つまり、デジタル署名されています。 これらのアセンブリのコード グループは、アセンブリの厳密な名前の公開キー情報に基づいて証拠を提供する **StrongNameMembershipCondition** を使用して定義されます。 コード グループには、**FullTrust** アクセス許可セットが付与されます。  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>レポート サーバーの拡張機能 (表示、データ、配信、およびセキュリティ)  
 レポート サーバーの拡張機能はカスタムのデータ、配信、表示、およびセキュリティ拡張機能であり、ユーザーまたは他のサード パーティが [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の機能を強化するために作成します。 このような拡張機能や機能強化する [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] コンポーネントに関連付けられたポリシー構成ファイルのアセンブリ コードには、**FullTrust** を付与する必要があります。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の一部として出荷される拡張機能は、レポート サーバーの公開キーで署名され、**FullTrust** アクセス許可セットが付与されます。  
  
> [!IMPORTANT]  
>  サード パーティの拡張機能では、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のポリシー構成ファイルを修正して **FullTrust** を許可する必要があります。 カスタム拡張機能用に **FullTrust** を持ったコード グループを追加しない限り、それらをレポート サーバーで使用することはできません。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のポリシー構成ファイルの詳細については、「[Reporting Services セキュリティ ポリシー ファイルの使用](using-reporting-services-security-policy-files.md)」を参照してください。  
  
## <a name="expressions-used-in-reports"></a>レポートで使用される式  
 レポートの式は、インライン コード式またはレポート定義言語ファイルの **Code** 要素に含まれるユーザー定義メソッドです。 ポリシー ファイルには、既定でこれらの式に **Execution** アクセス許可セットを付与する構成済みのコード グループがあります。 このコード グループは次のようになっています。  
  
```  
<CodeGroup  
   class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="Execution"  
   Name="Report_Expressions_Default_Permissions"  
   Description="This code group grants default permissions for code in report expressions and Code element. ">  
    <IMembershipCondition  
       class="StrongNameMembershipCondition"  
       version="1"  
       PublicKeyBlob="002400..."  
    />  
</CodeGroup>  
```  
  
 **Execution** アクセス許可によってコードを実行できますが、保護されたリソースを使用することはできません。 レポート内のすべての式はアセンブリ ("式のホスト" アセンブリ) にコンパイルされます。アセンブリはコンパイルされたレポートの一部として格納されます。 レポートを実行すると、レポート サーバーが式のホスト アセンブリを読み込み、そのアセンブリに対して、式を実行するための呼び出しを行います。 式のホスト アセンブリは、式のホストすべてのコード グループの定義に使用される特定のキーで署名されます。  
  
 レポートの式はレポート オブジェクト モデル コレクション (フィールド、パラメーターなど) を参照し、算術演算や文字列操作などの単純なタスクを実行します。 これらの単純な操作を実行するコードに必要なのは、**Execution** アクセス許可のみです。 既定では、**Code** 要素のユーザー定義メソッドとカスタム アセンブリには、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の **Execution** アクセス許可が付与されます。 したがって、現在の構成では、ほとんどの式に対してセキュリティ ポリシー ファイルを修正する必要がありません。 式のホスト アセンブリに追加権限を付与するには、管理者がレポート サーバーとレポート デザイナーのポリシー構成ファイルを修正し、レポート式のコード グループを変更する必要があります。 グローバル設定であるため、式のホストの既定の権限を変更すると、すべてのレポートに影響します。 この理由から、追加セキュリティを必要とするすべてのコードをカスタム アセンブリ内に配置することを強くお勧めします。 必要な権限は、このアセンブリにのみ付与します。  
  
> [!IMPORTANT]  
>  外部のアセンブリや保護されたリソースを呼び出すコードは、レポートで使用するカスタム アセンブリに組み込んでください。 そうすることで、コードが要求および表明する権限をより細かく制御できるようになります。 **Code** 要素内から、セキュリティで保護されたメソッドを呼び出すことは避けてください。 そのようにした場合、レポート式のホストに **FullTrust** を付与する必要があり、すべてのカスタム コードに CLR への完全なアクセス権が付与されます。  
  
> [!CAUTION]  
>  レポート式のホストのコード グループに **FullTrust** を付与しないでください。 付与した場合は、すべてのレポート式に、保護されたシステム呼び出しを許すことになります。  
  
## <a name="custom-assemblies-referenced-in-reports"></a>レポートで参照されるカスタム アセンブリ  
 一部のレポート式ではサード パーティのコード アセンブリを呼び出すことができます。[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、これをカスタム アセンブリとも呼びます。 レポート サーバーは、これらのアセンブリがポリシー構成ファイルに少なくとも **Execution** アクセス許可を持っていることを想定しています。 既定では、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] に付属のポリシー ファイルでは、"My Computer" ゾーンから起動されたすべてのアセンブリに **Execution** アクセス許可が付与されます。 カスタム アセンブリには、必要に応じて追加権限を付与できます。  
  
 レポート式の中で、特定のコード権限を必要とする操作を実行しなければならない場合もあります。 典型的な例としては、セキュリティで保護された CLR ライブラリ メソッド (ファイルやシステム レジストリにアクセスするもの) をレポート式から呼び出す場合が挙げられます。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] のドキュメントには、このようなセキュリティで保護された呼び出しに必要なコード権限が記載されています。呼び出しを実行するには、セキュリティで保護された特定の権限を呼び出し元コードに付与する必要があります。 レポートの式または **Code** 要素から呼び出す場合は、式のホスト アセンブリに適切なアクセス許可を付与する必要があります。 ただし、式のホストに権限を付与すると、あらゆる式とレポートで実行するすべてのコードに特定の権限が付与されます。 このような呼び出しはカスタム アセンブリから行うようにし、そのカスタム アセンブリに特定の権限を付与する方が、安全性は高くなります。  
  
## <a name="see-also"></a>参照  
 [Reporting Services のコード アクセス セキュリティ](code-access-security-in-reporting-services.md)   
 [セキュリティで保護された開発 &#40;Reporting Services&#41;](secure-development-reporting-services.md)  
  
  
