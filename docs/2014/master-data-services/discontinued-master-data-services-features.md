---
title: 廃止された SQL server 2014 マスター データ サービス機能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3f1eb85cb05c8284990d46241ed752515ef5504b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479441"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014 で提供が中止されたマスター データ サービス機能
  このトピックでは、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で使用できなくなった [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の機能について説明します。  
  
## <a name="includesssql14includessssql14-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 提供が中止された機能  
 今回のリリースで提供が中止された機能はありません。  
  
## <a name="includesssql11includessssql11-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 提供が中止された機能  
  
### <a name="security"></a>セキュリティ  
 セキュリティの割り当てを簡単にするために、モデル オブジェクト権限を派生階層、明示的階層、および属性グループの各オブジェクトに割り当てることができなくなりました。  
  
-   派生階層権限は、モデルに基づくようになりました。 たとえば、ユーザーを派生階層に対する権限を持っている場合は、割り当てる必要があります**Update**モデル オブジェクトにします。 割り当てることができますし、 **Deny**がアクセスするユーザーをしたくない任意のエンティティへのアクセス。  
  
-   明示的階層権限は、エンティティに基づくようになりました。 たとえば、ユーザーがある**Update**アカウント エンティティにアクセス許可は、エンティティのすべての明示的階層は更新可能になります。  
  
-   属性グループの権限を割り当てられなくなります、**ユーザーとグループ権限**機能領域。 代わりで、**システム管理**機能領域の属性グループを作成、ユーザーおよびグループを指定することができます**Update**属性グループへのアクセス許可。 **読み取り専用**属性グループへのアクセス許可が使用できなくします。  
  
### <a name="staging-process"></a>ステージング処理  
 新しいステージング処理を使用して、次の操作を実行することはできません。  
  
-   コレクションの作成または削除。  
  
-   コレクションへのメンバーの追加またはコレクションからのメンバーの削除。  
  
-   メンバーまたはコレクションの再アクティブ化。  
  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] のステージング処理を使用して、コレクションを操作できます。  
  
### <a name="model-deployment-wizard"></a>モデル配置ウィザード  
 データを含むパッケージは、ウィザードを使用して [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションに作成および配置することができなくなりました。 代わりに、新しいコマンド ライン ユーティリティを使用することができます。 詳細については、「[モデルの配置 (マスター データ サービス)](deploying-models-master-data-services.md)」を参照してください。  
  
 このウィザードは、データを含まないパッケージの作成および配置には引き続き使用できます。  
  
 また、パッケージは作成されたエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のみで展開できます。 つまり、 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] で作成されたパッケージを [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]に配置することはできません。 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 環境にパッケージを展開してから、データベースを [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] にアップグレードする必要があります。  
  
### <a name="code-generation-business-rules"></a>コード生成のビジネス ルール  
 Code 属性の値を自動的に生成するビジネス ルールを管理する方法が変わりました。 使用して、Code 属性の値を生成するには、以前は、**生成値に対する既定の属性**アクションで、**システム管理**機能領域で**ビジネス ルール**. **システム管理**、自動的に生成されたコードの値を有効にするエンティティを編集する必要があります。 詳細については、「[コードの自動作成 (マスター データ サービス)](automatic-code-creation-master-data-services.md)」を参照してください。  
  
 この種類のルールが格納された [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] モデルの配置パッケージを持っている場合は、データベースを [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] にアップグレードすると、ビジネス ルールが除外されます。  
  
### <a name="bulk-updates-and-exporting"></a>一括更新と一括エクスポート  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションで、複数のメンバーの属性値を一括更新することができなくなりました。 一括更新を実行するには、ステージング処理を使用または[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]します。  
  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションで、メンバーを Excel にエクスポートできなくなりました。 Excel でメンバーを操作するには、使用、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]します。  
  
### <a name="transactions"></a>トランザクション  
 **エクスプ ローラー**機能領域で、ユーザーは不要になったが、独自のトランザクションを元に戻します。 ユーザーがデータに加えた変更をこれまでは、元に戻す**エクスプ ローラー**します。 管理者はすべてのユーザーのトランザクションを戻すことができますが、**バージョン管理**機能領域。  
  
 注釈が永続的に保持されるようになり、削除できなくなりました。 以前は、注釈はトランザクションと見なされていて、トランザクションを元に戻すことで削除できました。  
  
### <a name="web-service"></a>Web サービス  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web サービスが、Silverlight の必要に応じて自動的に有効にされるようになりました。 以前は、Web サービスは手動で有効にする必要がありました。  
  
### <a name="powershell-cmdlets"></a>PowerShell コマンドレット  
 MDS に PowerShell コマンドレットが含まれなくなりました。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 に含まれている非推奨のマスター データ サービス機能](deprecated-master-data-services-features.md)  
  
  
