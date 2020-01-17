---
title: SQL Server 2014 の非推奨のマスター データ サービスの機能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd6342542da7528fef633ba02a430a8ba2ef5857
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483063"
---
# <a name="deprecated-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014 に含まれている非推奨のマスター データ サービス機能
  このトピックでは、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] でまだ使用できるものの、非推奨とされた [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]の機能について説明します。 これらの機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の今後のリリースで削除される予定です。 非推奨の機能を新しいアプリケーションで使用しないでください。  
  
## <a name="staging-process"></a>ステージング処理  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] で使用されていたステージング処理は、[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションでは使用できなくなりましたが、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] では引き続き使用できます。  
  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] のステージング処理のステージング エラーは、UI に表示されなくなります。 ステージング処理中に設定されたエラー コードは、ステージング テーブルで使用できることはこちら: [ https://msdn.microsoft.com/library/ff487022.aspx](https://msdn.microsoft.com/library/ff487022.aspx)します。  
  
 ステージング テーブル (tblStgMember、tblStgMemberAttribute、および tblStgRelationship) は、データベースで引き続き使用できます。 ステージング処理 (mdm.udpStagingSweep) を起動するために使用していたストアド プロシージャは、データベースで引き続き使用できます。  
  
 ステージング処理を呼び出す web サービス メソッドは引き続き使用できます。  
  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]で設定するステージングの間隔は、[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] および [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] の両方のステージング処理に適用されます。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] には、新しくパフォーマンスの高いステージング処理が実装されています。 詳細については、「[データのインポート &#40;マスター データ サービス&#41;](overview-importing-data-from-tables-master-data-services.md)」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 メタデータ モデルは[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションに引き続き表示されますが、使用しないでください。 将来のリリースでは削除される予定です。 ユーザーが内のメタデータを不要になった表示もできます、**エクスプ ローラー**  機能領域にして、メタデータ モデルのバージョン作成できなくします。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 で提供が中止されたマスター データ サービス機能](discontinued-master-data-services-features.md)  
  
  
