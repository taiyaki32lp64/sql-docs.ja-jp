---
title: PUBLISHINGSERVERNAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e4ae8127d6365e2fd88b92992ab7dd3308e1460f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105017"
---
# <a name="replication-functions---publishingservername"></a>レプリケーション関数 - PUBLISHINGSERVERNAME
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース ミラーリング セッションに参加しているパブリッシュされたデータベースの元のパブリッシャーの名前を返します。 この関数は、パブリケーション データベース上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパブリッシャー インスタンス側で実行されます。 パブリッシュされたデータベースの元のパブリッシャーを確認するために使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
PUBLISHINGSERVERNAME()  
```  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 PUBLISHINGSERVERNAME は、すべての種類のレプリケーションで使用できます。  
  
 PUBLISHINGSERVERNAME は、パブリッシャーとミラーリング パートナー インスタンスの間のパブリケーション データベースでデータベース ミラーリング セッションが開かれているときに使用します。  
  
 この関数はパブリケーション データベースのコンテキスト内で実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のミラーリング サーバー インスタンスのパブリケーション データベースで PUBLISHINGSERVERNAME を実行すると、パブリッシュされたデータベースの発行元パブリッシャー インスタンスの名前が返されます。 この関数が、パブリッシュされていない、またはフェールオーバー後にミラー サーバー インスタンスからパブリッシュされたミラー サーバー インスタンスにあるデータベース上で実行されると、ミラー サーバー インスタンスの名前が返されます。 この関数が元のパブリッシャー インスタンスで実行されると、パブリッシャーの名前が返されます。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングとレプリケーション &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [レプリケーションの動作 &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/53702dee-de58-47d5-a552-7f32000f77d4)  
  
  
