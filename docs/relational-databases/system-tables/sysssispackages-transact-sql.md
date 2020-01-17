---
title: sysssispackages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackages90_TSQL
- sysdtspackages90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackages system table
ms.assetid: 66155dcd-dcdb-4e33-a242-1625828ad8d2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 21487ba46e53997ebb50403cc4eaf1ae54f0a103
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029643"
---
# <a name="sysssispackages-transact-sql"></a>sysssispackages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  保存されているパッケージごとに 1 つの行を含む[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このテーブルに格納されます、 **msdb**データベース。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|パッケージの一意識別子です。|  
|**id**|**uniqueidentifier**|パッケージの GUID。|  
|**description**|**nvarchar**|パッケージの説明 (省略可)。|  
|**createdate**|**datetime**|パッケージが作成された日付。|  
|**folderid**|**uniqueidentifier**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] によってパッケージの一覧が格納される論理フォルダーの GUID。|  
|**ownersid**|**varbinary**|パッケージを作成したユーザーの一意なセキュリティ識別子。|  
|**packagedata**|**image**|パッケージです。|  
|**packageformat**|**int**|パッケージが保存されている形式:<br /><br /> 2 の値は、パッケージに保存することを示します、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]形式。<br /><br /> 値 3 は、の形式にパッケージを保存することを示します[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]またはそれ以降。|  
|**packagetype**|**int**|パッケージを作成したクライアント。 次のような値が考えられます。<br /><br /> 0 (既定値)<br /><br /> 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インポートおよびエクスポート ウィザード)<br /><br /> 3 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]レプリケーション)<br /><br /> 5 ([!INCLUDE[ssIS](../../includes/ssis-md.md)]デザイナー)<br /><br /> 6 (メンテナンス プラン デザイナーまたはメンテナンス プラン ウィザード)<br /><br /> <br /><br /> この列の値に対応している、<xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>列挙体。|  
|**vermajor**|**int**|パッケージの最新のメジャー バージョン。|  
|**verminor**|**int**|パッケージの最新のマイナー バージョン。|  
|**verbuild**|**int**|パッケージの最新のビルド。|  
|**vercomments**|**nvarchar**|パッケージ バージョンについてのコメント。|  
|**verid**|**uniqueidentifier**|パッケージのバージョンの GUID です。|  
|**isencrypted**|**bit**|パッケージが暗号化されているかどうかを示すブール値。|  
|**readrolesid**|**varbinary**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パッケージを読み込むことができるロール。|  
|**writerolesid**|**varbinary**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パッケージを保存することができるロール。|  
  
## <a name="see-also"></a>関連項目  
 [Integration Services (SSIS) パッケージ](../../integration-services/integration-services-ssis-packages.md)  
  
  
