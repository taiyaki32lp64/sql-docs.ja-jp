---
title: 暗号化されたミラー データベースの設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- database master key [SQL Server], database mirroring
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e96342ca114ae06d2c1d75954ccd32a674f900a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025233"
---
# <a name="set-up-an-encrypted-mirror-database"></a>暗号化されたミラー データベースの設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ミラー データベースのデータベース マスター キーの暗号化を自動的に解除できるようにするには、マスター キーの暗号化に使用したパスワードをミラー サーバー インスタンスに指定する必要があります。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンには、パスワードを転送するメカニズムがあります。 データベース ミラーリングを開始する前にデータベース マスター キーに対する資格情報を作成するには、 **sp_control_dbmasterkey_password** を使用します。 この処理は、ミラー化するすべてのデータベースに対して行う必要があります。 詳細については、「 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)」を参照してください。  
  
> [!CAUTION]  
>  **sa** など高いレベルの特権を持つサーバー プリンシパルからのアクセスを禁止したままにしておく必要のあるデータベースについては、フェールオーバー時の暗号化解除を有効にしないでください。 データベースのキー階層をサービス マスター キーで暗号化解除できないようにデータベースを構成できます。 このオプションは、 **sa** など特権レベルの高いサーバー プリンシパルからアクセスできてはならない情報を格納しているデータベースに対する多層防御の 1 つとしてサポートされています。 このようなデータベースに対してフェールオーバー時の暗号化解除を有効にすると、この多層防御が効力を失います。その結果、 **sa** など特権レベルの高いサーバー プリンシパルによるデータベースの暗号化解除が可能になります。  
  
## <a name="see-also"></a>参照  
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  
