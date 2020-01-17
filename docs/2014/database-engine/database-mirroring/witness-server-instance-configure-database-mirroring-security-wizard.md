---
title: ミラーリング監視サーバー インスタンス (データベース ミラーリング セキュリティ構成ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.witnsrvr.f1
ms.assetid: b5763663-984a-473b-93a3-6cd3322ad41c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7db00b9deeb5faad62731aa666c54fa385be765b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753974"
---
# <a name="witness-server-instance-configure-database-mirroring-security-wizard"></a>[ミラーリング監視サーバー インスタンス] (データベース ミラーリング セキュリティ構成ウィザード)
  このページを使用すると、セッションのミラーリング監視サーバーとして機能するサーバー インスタンスの情報を指定できます。  
  
> [!NOTE]  
>  ミラーリング監視サーバー インスタンスは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
 **SQL Server Management Studio を使用してデータベース ミラーリングを構成するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>および  
 **[ミラーリング監視サーバー インスタンス]**  
 **[データベースのプロパティ]** ダイアログ ボックスの **[ミラー化]** ページで、ミラーリング監視サーバー インスタンスが既に指定されている場合、そのインスタンスが表示されます。詳細については、「[[データベースのプロパティ] &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)」を参照してください。  
  
 それ以外の場合、このリスト ボックスには現在のサーバーの名前が表示されます。 プリンシパル サーバー インスタンスまたはミラー サーバー インスタンスと同じ名前をミラーリング監視サーバー インスタンスに指定しないように注意してください。  
  
 **Connect**  
 ミラーリング監視サーバー インスタンスが指定されていない場合、 **[接続]** をクリックします。 **[サーバーへの接続]** ダイアログ ボックスが表示されます。ここでサーバー インスタンスを指定し、接続を確立できます。  
  
 インスタンスが指定されていても、エンドポイントが存在するかどうかをチェックできる権限を持つ接続がない場合には、 **[接続]** をクリックします。 **[サーバーへの接続]** ダイアログ ボックスが表示されます。この場合、サーバー インスタンスは選択されており、変更できません。 十分な権限を持つドメイン アカウントを指定して、サーバー インスタンスに接続します。  
  
> [!NOTE]  
>  データベース ミラーリング セキュリティ構成ウィザードは、 **[サーバーへの接続]** ダイアログ ボックスで指定された資格情報を使ってサーバー インスタンスに接続します。 これらは、ミラーリング セッションの資格情報とは異なります。ミラーリング セッションでは、サーバー インスタンスをサービスとして実行している開始アカウントの資格情報が使用されます。  
  
 **[リスナー ポート]**  
 このオプションでは、このサーバー インスタンスに対するミラーリング エンドポイントが存在するかどうかに応じて、次のような内容が表示されます。  
  
-   サーバー インスタンスに対するリスナー ポートが存在しない場合、 **[ポート]** テキスト ボックスにはポート番号 5022 が表示されます。 使用可能な任意のポート番号を入力できます (7022 など)。  
  
-   ミラーリング エンドポイントが既に存在する場合、そのエンドポイントからのポート番号が表示されます。 ポートを変更する必要がある場合は、ALTER ENDPOINT ステートメントを使用します。 詳細については、「[ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)」を参照してください。  
  
    > [!NOTE]  
    >  ポート番号は必須です。  
  
 **[エンドポイント名]**  
 このサーバー インスタンスのミラーリング エンドポイントが存在する場合、ここにエンドポイント名が表示されます。 エンドポイントが存在しない場合には、エンドポイントの名前を指定できます。  
  
 **[このエンドポイントから送られるデータを暗号化する]**  
 既定で、暗号化は有効になっています。 暗号化が有効な場合、暗号化は必須です (サポートされるだけではありません)。暗号化オプションにはすべて既定値が使用されます。 詳細については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)」を参照してください。  
  
 暗号化を無効にするには、チェック ボックスをオフにします。 暗号化を再度有効にするには、チェック ボックスをオンにします。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [データベース プロパティ &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [データベース ミラーリング モニターの起動 &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [データベース ミラーリング監視サーバー](database-mirroring-witness.md)  
  
  
