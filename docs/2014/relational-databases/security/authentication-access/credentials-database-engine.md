---
title: 資格情報 (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d42f93735723c81baf837736bfabcda2b1707aae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011839"
---
# <a name="credentials-database-engine"></a>資格情報 (データベース エンジン)
  資格情報は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部のリソースへの接続に必要な認証情報 (資格情報) を含むレコードです。 この情報は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によって内部的に使用されます。 通常、資格情報には Windows ユーザー名とパスワードが含まれます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証経由で接続しているユーザーは、資格情報に格納された情報によって、サーバー インスタンスの外部のリソースにアクセスできるようになります。 外部リソースが Windows である場合、ユーザーは、資格情報に指定されている Windows ユーザーとして認証されます。 1 つの資格情報を複数の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインにマッピングすることもできます。 ただし、1 つの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは 1 つの資格情報にしかマップできません。  
  
 システム資格情報は、自動的に作成され、特定のエンドポイントに関連付けられます。 システム資格情報の名前は 2 つのシャープ記号 (##) で始まります。  
  
 資格情報の詳細については、次を参照してください。、 [sys.credentials](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql)カタログ ビューです。  
  
## <a name="related-content"></a>関連コンテンツ  
 [資格情報を作成](../authentication-access/create-a-credential.md) [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
 [SQL Server の保護](../securing-sql-server.md)  
  
  
