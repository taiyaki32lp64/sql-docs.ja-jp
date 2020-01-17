---
title: DROP AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 613841598b153dbe502f0267ed85197973bf706a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898294"
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定された可用性グループとそのすべてのレプリカを削除します。 可用性グループを削除する際、可用性レプリカの 1 つをホストするサーバー インスタンスがオフラインだった場合は、再度オンラインになった時点でローカルの可用性レプリカが削除されます。 可用性グループを削除すると、関連付けられている可用性グループ リスナーも削除されます (存在する場合)。  
  
> [!IMPORTANT]  
>  可能であれば、プライマリ レプリカをホストするサーバー インスタンスに接続しているときにのみ可用性グループを削除してください。 可用性グループをプライマリ レプリカから削除すると、元のプライマリ データベースで変更が許可されます (高可用性の保護なし)。 セカンダリ レプリカから可用性グループを削除すると、プライマリ レプリカは **RESTORING** 状態になり、変更はデータベースで許可されません。  
  
 可用性グループを削除する別の方法については、「[可用性グループの削除&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *group_name*  
 削除する可用性グループの名前を指定します。  
  
## <a name="limitations-and-recommendations"></a>制限事項と推奨事項  
  
-   **DROP AVAILABILITY GROUP** を実行するには、サーバー インスタンスで AlwaysOn 可用性グループ機能が有効になっている必要があります。 詳細については、「[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)」を参照してください。  
  
-   **DROP AVAILABILITY GROUP** は、バッチの一部として実行することや、トランザクション内で実行することはできません。 また、式および変数はサポートされません。  
  
-   可用性グループの削除は、その可用性グループに対する適切なセキュリティ資格情報が存在する任意の Windows Server フェールオーバー クラスタリング (WSFC) ノードから行うことができます。 そのため、可用性レプリカがまったく残っていなくても可用性グループを削除することができます。  
  
    > [!IMPORTANT]  
    >  Windows Server フェールオーバー クラスタリング (WSFC) クラスターにクォーラムがない場合は、可用性グループを削除しないでください。 クラスターのクォーラムがないときに可用性グループを削除すると、クラスターに格納されているメタデータ可用性グループは削除されません。 クラスターのクォーラムが再取得された後、WSFC クラスターから削除するために、可用性グループをもう一度削除する必要があります。  
  
-   セカンダリ レプリカについては、**DROP AVAILABILITY GROUP** は緊急の目的だけに使用してください。 理由は、可用性グループを削除すると可用性グループがオフラインになるためです。 セカンダリ レプリカから可用性グループを削除した場合、プライマリ レプリカは、**OFFLINE** 状態が、クォーラム損失、強制フェールオーバー、または **DROP AVAILABILITY GROUP** コマンドのどの原因で発生したのかを特定できません。 スプリット ブレイン状況の発生を防ぐために、プライマリ レプリカは **RESTORING** 状態に遷移します。 詳細については、「[How It Works:DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx)」 (動作方法: DROP AVAILABILITY GROUP の動作) (CSS SQL Server エンジニアのブログ) を参照してください。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 可用性グループの **ALTER AVAILABILITY GROUP** 権限、**CONTROL AVAILABILITY GROUP** 権限、**ALTER ANY AVAILABILITY GROUP** 権限、または **CONTROL SERVER** 権限が必要です。 ローカル サーバー インスタンスによってホストされていない可用性グループを削除するには、その可用性グループ上の **CONTROL SERVER** 権限または **CONTROL** 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、 `AccountsAG` 可用性グループを削除します。  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [動作方法:DROP AVAILABILITY GROUP の動作](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server エンジニアのブログ)  
  
## <a name="see-also"></a>参照  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [可用性グループの削除 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
