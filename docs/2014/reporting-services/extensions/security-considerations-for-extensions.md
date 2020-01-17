---
title: 拡張機能のセキュリティに関する考慮事項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], extensions
- extensions [Reporting Services], security
- permissions [Reporting Services], extensions
ms.assetid: 58cbdfeb-1105-4a7d-a3b8-b897ff95f367
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 128da8d5bb3b956b5b5661ce47ca6e4b741f0bc5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63282414"
---
# <a name="security-considerations-for-extensions"></a>拡張機能のセキュリティに関する考慮事項
  共通言語ランタイム (CLR) をターゲットとするすべてのアプリケーションは、CLR セキュリティ システムと対話する必要があります。 このようなアプリケーションを実行すると、CLR によってアプリケーションが自動的に評価され、権限のセットが付与されます。 アプリケーションに付与された権限に応じて、実行が継続されるかセキュリティ例外が生成されます。 特定のレポート サーバーのセキュリティ ポリシー構成ファイルのローカル セキュリティ設定とポリシーによって、アセンブリが受け取るコード権限が定義されます。  
  
 権限を要求する前に、拡張コードが使用するリソースと保護された操作を認識すると共に、そのリソースと操作を保護する権限について知っておく必要があります。 拡張機能コンポーネントによって呼び出されるクラス ライブラリ メソッドがアクセスするリソースを継続的に追跡することも必要です。 詳細については、『[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 開発者ガイド』の「アクセス許可の要求」を参照してください。  
  
 レポート サーバーに配置される拡張機能は、完全に信頼されて実行する必要があります。つまり、拡張機能は **FullTrust** アクセス許可セットを付与されたコード グループの一部である必要があります。 これは、特定のレポートに対してユーザーが承認されているかどうかに応じて、CLR を通して使用できる特定のサーバー リソースと操作に、拡張機能がアクセス権を持つことができることも意味します。 コード グループと拡張機能の詳細については、「[Reporting Services のコード アクセス セキュリティ](secure-development/code-access-security-in-reporting-services.md)」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、その拡張機能のすべてに [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] セキュリティを適用します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ処理、配信、表示、およびセキュリティの各拡張機能の配置には、次の条件が適用されます。  
  
-   ローカル管理者のみが拡張機能を配置する権限を持ちます。  
  
-   適切な読み取りおよび書き込み権限を持つユーザーのみが、拡張する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントの構成ファイルを変更できます。  
  
-   特権ユーザーのみが、セキュリティ ポリシー ファイルを編集して拡張機能のコード アクセス セキュリティを有効にする権限を持ちます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のコード アクセス セキュリティの詳細については、「[セキュリティで保護された配置 &#40;Reporting Services&#41;](secure-development/secure-development-reporting-services.md)」を参照してください。  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] セキュリティの詳細については、『[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 開発者ガイド』の「.NET Framework セキュリティ」を参照してください。  
  
## <a name="initialization-of-extension-assemblies"></a>拡張機能アセンブリの初期化  
 レポート サーバーで拡張機能を最初にメモリに読み込むときに、サービス アカウントの資格情報が使用されます。一部の拡張機能アセンブリでは、システム リソースへのアクセス、構成ファイルの読み込み、およびその他の依存するアセンブリの読み込みに特定の権限が必要であるためです。 ただし、アセンブリが読み込まれ、初期化された後は、拡張機能アセンブリのすべての呼び出しに、現在ログオンしているユーザー アカウントの資格情報が使用されます。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](reporting-services-extensions.md)   
 [Reporting Services 拡張機能ライブラリ](reporting-services-extension-library.md)  
  
  
