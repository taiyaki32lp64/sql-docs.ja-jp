---
title: MSdistpublishers (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c19f2d8e75a3c9744318d65683b29d1d84857ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907424"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **MSdistpublishers**テーブルには、ローカル ディストリビューターによってサポートされている各リモート パブリッシャーに 1 つの行が含まれています。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|パブリッシャーのディストリビューターの名前。|  
|**distribution_db**|**sysname**|ディストリビューション データベースの名前。|  
|**working_directory**|**nvarchar (255)**|パブリケーションのデータとスキーマ ファイルを格納するために使用する作業ディレクトリの名前。|  
|**security_mode**|**int**|ディストリビューターで実装されているセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。<br /><br /> **1** = Windows 認証。|  
|**login**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログイン ID です。|  
|**password**|**nvarchar(524)**|(暗号化) パスワード[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**active**|**bit**|ローカルのディストリビューターがリモート パブリッシャーによって使用するかどうかを示します。|  
|**trusted**|**bit**|リモート パブリッシャーがローカル ディストリビューターと同じパスワードを使用するかどうかを示します。<br /><br /> **0** = A、ディストリビューターに接続するリモートのパブリッシャーでパスワードが必要です。<br /><br /> **1** = No パスワードが必要です。|  
|**third_party**|**bit**|パブリッシャーがのインストールであるかどうか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストール **。1** = 異種データ ソース。|  
|**publisher_type**|**sysname**|パブリッシャーの種類:<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。<br /><br /> **ORACLE**標準の Oracle パブリッシャーを = です。<br /><br /> **ORACLE GATEWAY** = Oracle ゲートウェイ パブリッシャーです。|  
|**storage_connection_string**|**nvarchar(779)**|Azure SQL Database ストレージ接続文字列の値。|  

  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
