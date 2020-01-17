---
title: DBCC FLUSHAUTHCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 00497dfe67c03eab4d9d0bc1798f6d5537628ed7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101942"
---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] の現在のユーザー データベースで、ログインとファイアウォール ルールに関する情報を含むデータベース認証キャッシュを空にします。 このステートメントは、論理データベースには適用されません。これは、マスター データベースに、ログインおよびファイアウォール ルールに関する情報の物理ストレージが含まれているためです。 ステートメントを実行しているユーザーおよび現在接続されている他のユーザーの接続状態は維持されます ([!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] では、DBCC FLUSHAUTHCACHE は現在サポートされていません)。
 
![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>引数  
[なし] :
  
## <a name="remarks"></a>Remarks  
認証キャッシュは、マスターに格納されているログインおよびサーバー ファイアウォール ルールのコピーを作成し、ユーザー データベースのメモリに配置します。  含まれているデータベース ユーザーに関する情報は、既にユーザー データベースに格納されているため、含まれているデータベース ユーザーは認証キャッシュの一部ではありません。
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続を継続的にアクティブにするには、少なくとも 10 時間ごとに ([!INCLUDE[ssDE](../../includes/ssde-md.md)] によって実行される) 再認証が必要です。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、最初に送信されたパスワードを使用して再認証を試行するので、ユーザー入力は不要です。 パスワードが [!INCLUDE[ssSDS](../../includes/sssds-md.md)] でリセットされた場合、接続プーリングのために接続がリセットされても、パフォーマンス上の理由から接続は再認証されません。 この動作は、オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の動作とは異なります。 接続が最初に承認された後でパスワードが変更されている場合は、接続を終了し、新しいパスワードを使用して新しい接続を行う必要があります。 KILL DATABASE CONNECTION アクセス許可を持つユーザーは、[KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md) コマンドを使用して、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続を明示的に終了できます。
  
## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 管理者アカウントが必要です。
  
## <a name="example"></a>例  
次のステートメントは、現在のデータベースの認証キャッシュをクリアします。
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
