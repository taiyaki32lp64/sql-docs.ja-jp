---
title: サービス マスター キー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 6a802cfadfa48c7dbba7479ca169daedf70fe8b9
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957137"
---
# <a name="service-master-key"></a>インスタンスに対して生成される
  サービス マスター キーは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 暗号化階層のルートです。 これは、最初に別のキーを暗号化する必要性が生じたときに自動的に生成されます。 既定では、サービス マスター キーはローカル コンピューターのキーを使用し、Windows データ保護 API により暗号化されます。 サービス マスター キーを作成した Windows サービス アカウント、またはサービス アカウント名とサービス アカウントのパスワードの両方にアクセスできるプリンシパルだけが、サービス マスター キーを開くことができます。  
  
 サービス マスター キーを再生成または復元するには、完全な暗号化階層の暗号化解除と再暗号化が必要になります。 この操作ではリソースが集中的に使用されるので、キーが侵害されている場合を除いて、業務が忙しい時間帯を避けてスケジュールを設定するようにしてください。  
  
 
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] AES 暗号化アルゴリズムを使用してサービス マスター キー (SMK) とデータベース マスター キー (DMK) を保護します。 AES は、以前のバージョンで使用されていた 3DES よりも新しい暗号化アルゴリズムです。 
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] のインスタンスを [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] にアップグレードした後で、マスター キーを AES にアップグレードするために SMK と DMK を再度生成する必要があります。 SMK の再作成の詳細については、「[ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)」および「[ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql)」を参照してください。  
  
## <a name="best-practice"></a>ベスト プラクティス  
 サービス マスター キーをバックアップし、バックアップしたコピーをセキュリティで保護されたオフサイトの場所に格納します。  
  
## <a name="related-tasks"></a>Related Tasks  
 [バックアップサービスマスターキー &#40;Transact-sql&#41;](/sql/t-sql/statements/backup-service-master-key-transact-sql)  
  
 [Transact-sql&#41;&#40;サービスマスターキーを復元する](/sql/t-sql/statements/restore-service-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
## <a name="see-also"></a>参照  
 [暗号化階層](encryption-hierarchy.md)  
  
  
