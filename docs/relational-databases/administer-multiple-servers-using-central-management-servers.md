---
title: 中央管理サーバーを使用した複数のサーバーの管理
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: a2e2da55bd04ba29cf1c6ef81757488f8d50fd24
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055618"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>中央管理サーバーを使用した複数のサーバーの管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  中央管理サーバーを指定し、サーバー グループを作成することで、複数のサーバーを管理できます。  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>中央管理サーバーおよびサーバー グループとは  
 中央管理サーバーとして指定した SQL Server のインスタンスは、1 つ以上のインスタンスの接続情報を含むサーバー グループを管理します。 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントおよびポリシー ベースの管理ポリシーをサーバー グループに対して同時に実行できます。 中央管理サーバーを通じて管理されているインスタンスのログ ファイルを表示することもできます。 
 
 基本的に、中央管理サーバーはマネージド サーバーのリストを含む中央リポジトリです。 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] より前のバージョンでは、中央管理サーバーを指定できません。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントは、登録済みサーバー内のローカル サーバー グループに対しても実行できます。  
  
## <a name="create-central-management-server-and-server-groups"></a>中央管理サーバーおよびサーバー グループを作成する 
 中央管理サーバーとサーバー グループを作成するには、 **の** [登録済みサーバー] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]ウィンドウを使用します。 中央管理サーバーを、それ自体が管理するグループのメンバーにすることはできません。 
 
 中央管理サーバーとサーバー グループの作成方法については、「[中央管理サーバーおよびサーバー グループの作成 &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
