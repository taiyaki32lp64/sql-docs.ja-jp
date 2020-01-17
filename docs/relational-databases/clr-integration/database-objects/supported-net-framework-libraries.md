---
title: .NET Framework ライブラリのサポート |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: faace3cf7e03afe18d2298580c45470f0b32b580
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140882"
---
# <a name="supported-net-framework-libraries"></a>サポートされている .NET Framework ライブラリ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にホストされている共通言語ランタイム (CLR) を使用すると、ストアド プロシージャ、トリガー、ユーザー定義関数、ユーザー定義型、およびユーザー定義集計をマネージド コードで作成できます。 .NET Framework クラス ライブラリに用意されている機能を使用すると、文字列操作、高度な算術演算、ファイル アクセス、暗号化などの機能を提供する組み込みのクラスにアクセスできます。 これらのクラスは、任意のマネージド ストアド プロシージャ、ユーザー定義型、トリガー、ユーザー定義関数、またはユーザー定義集計からアクセスできます。  
  
> [!NOTE]  
>  グローバル アセンブリ キャッシュ (GAC) で、サポートされていないアセンブリを提供またはアップグレードすると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アプリケーションが動作しなくなる可能性があります。 これは、GAC でライブラリを提供またはアップグレードしても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内でそれらのアセンブリが更新されないためです。 アセンブリが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースと GAC の両方に存在する場合、アセンブリの 2 つのコピーが完全に一致する必要があります。 一致しない場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 統合によってアセンブリが使用されたときにエラーが発生します。 サービスまたはサポートされていない .NET Framework アセンブリを含む、データベースにも登録されている GAC のアセンブリをアップグレードすることも、サービスまたはアセンブリ内のコピーをアップグレードすることを確認して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データベースでは、 **ALTER ASSEMBLY**ステートメント。 詳細については、次を参照してください。[サポート技術情報の資料 949080](https://support.microsoft.com/kb/949080)します。  
  
## <a name="supported-libraries"></a>サポートされているライブラリ  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、サポートされている .NET Framework ライブラリの一覧が用意されています。これらのライブラリは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との連携に必要な信頼性およびセキュリティの基準を満たしていることがテストで確認されています。 サポートされているライブラリは、サーバーに明示的に登録することなく、コードから使用できます。[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、グローバル アセンブリ キャッシュ (GAC) からこれらのライブラリを直接読み込みます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の CLR 統合でサポートされるライブラリおよび名前空間を次に示します。  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   システム  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>サポートされていないライブラリ  
 サポートされていないライブラリは、マネージド ストアド プロシージャ、トリガー、ユーザー定義関数、ユーザー定義型、およびユーザー定義集計から呼び出すことができます。 サポートされていないライブラリに登録する必要があります、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を使用して、データベース、 **CREATE ASSEMBLY**ステートメントでは、前に、コードのために使用できます。 サポートされていないライブラリをサーバーに登録して実行する場合は、そのライブラリのセキュリティと信頼性を確認およびテストする必要があります。  
  
 たとえば、 **System.DirectoryServices**名前空間はサポートされていません。 System.DirectoryServices.dll アセンブリを登録する必要があります**UNSAFE**コードからを呼び出すにはアクセスを許可します。 **UNSAFE**アクセス許可が必要なため、クラス、 **System.DirectoryServices**名前空間の要件を満たしていない**セーフ**または**EXTERNAL_ACCESS**します。 詳細については、次を参照してください。 [CLR 統合プログラミング モデルの制限事項](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)と[CLR 統合のコード アクセス セキュリティ](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)します。  
  
## <a name="see-also"></a>参照  
 [アセンブリを作成します。](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR 統合のコード アクセス セキュリティ](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 統合プログラミング モデルの制限事項](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
