---
title: SQL Server の知的所有権の保護 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: afe179023f72ec509af5828bb89afb51f93b53a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986595"
---
# <a name="protecting-your-sql-server-intellectual-property"></a>SQL Server の知的所有権の保護
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

ソフトウェア開発者から、どのようにすれば、顧客が [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] データ アプリケーションを分析したり、分解できないように、アプリケーションを配布できるかよく質問されます。 ここでの基本原則は、知的財産の保護は法的な問題であり、保護に関する記載は使用許諾契約にあるということです。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] が他のユーザーが管理するコンピューターにインストールされている場合、ユーザーは元からそれを完全に管理することはできません。 

## <a name="nature-of-the-problem"></a>問題の性質
コンピューターの所有者または管理者は、そのコンピューターにインストールされている [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] のインスタンスにいつでもアクセスできます。 お客様が管理するコンピューターにアプリケーションを展開した場合、管理者であるため、お客様は **sysadmin** 固定サーバー ロールのメンバーとして [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] に接続できます。 つまり、アクセス権限の付与、(他のコンピューターへのバックアップの復元を含む) バックアップの管理、復号化、およびデータ ファイルの移動などもできるのです。詳細については、「 [システム管理者がロックアウトされた場合の SQL Server への接続](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)」を参照してください。 

ストアド プロシージャおよびデータは暗号化できますが、データ構造は非表示にできないので、サーバー プロセスにデバッガーをアタッチできるユーザーは、実行時にメモリから復号化されたプロシージャとデータを取得できてしまいます。

クライアントがコンピューターの管理者でない場合は、クライアントのアクセスを阻止できます。 ファイル データの暗号化、バックアップの暗号化、すべてのユーザー操作の監査には、[透過的なデータ暗号化](../../relational-databases/security/encryption/transparent-data-encryption.md)を使用できます。 ただし、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] コンピューターの [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] の管理者と管理グループは、これらの操作を取り消すことができます。

## <a name="solution"></a>解決方法
クライアントのコンピューターに [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] をインストールしなくてもクライアントのデータ アクセスを構成する方法は多数あります。 最も簡単な方法は、クライアントが管理者ではない [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] を [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) と組み合わせて使用する方法です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] の概要については、「[SQL Database とは SQL データベースの概要](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)」を参照してください。  

また、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] を自分のネットワークにホストし、クライアントがネットワーク経由で直接または Web アプリケーションを経由してデータにアクセスできるようにできます。

## <a name="see-also"></a>参照

[SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[SQL Server の保護](../../relational-databases/security/securing-sql-server.md)  

