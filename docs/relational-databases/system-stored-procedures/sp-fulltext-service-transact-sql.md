---
title: sp_fulltext_service (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_service
- sp_fulltext_service_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- sp_fulltext_service
- Full-Text Search Upgrade Option
ms.assetid: 17a91433-f9b6-4a40-88c4-8c704ec2de9f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9ede8b65cb3f11ed6640121031ea6a2fe5b57b83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124189"
---
# <a name="spfulltextservice-transact-sql"></a>sp_fulltext_service (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフルテキスト検索のサーバー プロパティを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_service [ [@action=] 'action'   
     [ , [ @value= ] value ] ]  
```  
  
## <a name="arguments"></a>引数  
`[ @action = ] 'action'` 変更またはリセットするプロパティです。 *アクション*は**nvarchar(100)、** 既定値はありません。 一覧については、*c*アクション プロパティ、その説明、および設定できる値は、下の表を参照してください、*値*引数。 この引数によって返されるプロパティには、データ型、現在の実行値、最小値または最大値、非推奨のステータスなどがあります。  
  
`[ @value = ] value` 指定したプロパティの値です。 *値*は**sql_variant**既定値は NULL です。 場合@valueが null、 **sp_fulltext_service**現在の設定を返します。 次の表は、アクション プロパティとその説明、および設定できる値の一覧です。  
  
> [!NOTE]  
>  次の操作は、の将来のリリースで削除される予定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **clean_up**、 **connect_timeout**、 **data_timeout**、および**resource_使用状況**します。 新しい開発作業でこれらのアクションを使用しないようにして、現在これらのいずれかを使用しているアプリケーションの変更を検討してください。  
  
|操作|データの種類|説明|  
|------------|---------------|-----------------|  
|**clean_up**|**int**|旧バージョンとの互換性のためにのみサポートされています。 値は常に 0 です。|  
|**connect_timeout**|**int**|旧バージョンとの互換性のためにのみサポートされています。 値は常に 0 です。|  
|**data_timeout**|**int**|旧バージョンとの互換性のためにのみサポートされています。 値は常に 0 です。|  
|**load_os_resources**|**int**|オペレーティング システムのワード ブレーカー、ステミング機能、およびフィルターを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに登録し、使用するかどうかを指定します。 次のいずれかです。<br /><br /> 0 = この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス固有のフィルターとワード ブレーカーのみを使用<br /><br /> 1 = オペレーティング システムのフィルターとワード ブレーカーを読み込む<br /><br /> オペレーティング システムに行われた更新によって予期しない動作が起こるのを防ぐため、既定ではこのプロパティは無効になっています。 言語のリソースへのアクセスを提供するオペレーティング システム リソースの使用を有効にし、登録されているドキュメントの種類[!INCLUDE[msCoName](../../includes/msconame-md.md)]Indexing Service にインストールされているインスタンス固有のリソースはありません。 オペレーティング システム リソースの読み込みを有効にした場合は、オペレーティング システム リソースが信頼された署名付きバイナリ; であることを確認します。それ以外の場合、読み込みができなくなる場合に**verify_signature** (下記参照) が 1 に設定します。|  
|**master_merge_dop**|**int**|マスター マージ プロセスで使用されるスレッドの数を指定します。 この値が使用可能な Cpu または CPU の数を超えないコアです。<br /><br /> サービスを使用して、4、または使用可能な Cpu または CPU の数より小さくこの引数が指定されていない場合のコア。|  
|**pause_indexing**|**int**|現在一時停止している場合は、かどうか、フルテキスト インデックス作成する必要がありますが現在実行されている場合、一時停止または再開されるを指定します。<br /><br /> 0 = サーバー インスタンスのフルテキスト インデックス作成を再開する<br /><br /> 1 = サーバー インスタンスのフルテキスト インデックス作成アクティビティの一時停止します。|  
|**resource_usage**|**int**|関数を持たない[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降のバージョンは無視されます。|  
|**update_languages**|NULL|フルテキスト検索に登録された言語の一覧を更新します。 インデックスやフルテキスト クエリで構成するときに、言語が指定されます。 などのデータ型で格納されている .docx などの対応するファイル形式からテキストの情報を抽出するフィルターを使用して、フィルター デーモン ホスト**varbinary**、 **varbinary (max)** 、**イメージ**、または**xml**、フルテキスト インデックス作成。<br /><br /> 詳細については、「 [登録済みのフィルターおよびワード ブレーカーの表示または変更](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)」を参照してください。|  
|**upgrade_option**|**int**|データベースを [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] からそれより新しいバージョンにアップグレードする際のフルテキスト インデックスの移行方法を制御します。 このプロパティは、データベースのインポート、データベース バックアップの復元、ファイル バックアップの復元、またはデータベース コピー ウィザードを使用したデータベースのコピーによってアップグレードする場合に適用されます。<br /><br /> 次のいずれかです。<br /><br /> 0 = フルテキスト カタログは、新しい強化されたワード ブレーカーを使用して再構築されます。 インデックスの再構築には時間がかかり、アップグレード後にかなりの量の CPU とメモリが必要になる可能性があります。<br /><br /> 1 = フルテキスト カタログがリセットされます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のフルテキスト カタログ ファイルは削除されますが、フルテキスト カタログのメタデータおよびフルテキスト インデックスは保持されます。 アップグレード後、すべてのフルテキスト インデックスで変更の追跡は無効化されており、クロールは自動的には開始されません。 アップグレードの完了後、手動で完全作成を実行するまで、カタログは空のままになります。<br /><br /> 2 = フルテキスト カタログがインポートされます。 通常、インポートの方が再構築よりもかなり高速に処理されます。 たとえば、CPU を 1 つだけ使用している場合、インポートは、再構築の約 10 倍の速さで実行されます。 ただし、最終的にフルテキスト カタログの再構築するため、インポートされたフルテキスト カタログは、新しい強化されたワード ブレーカーを使用できません。<br /><br /> 注:再構築はマルチスレッド モードで実行できます。10 を超える CPU が使用可能な場合に、再構築でそれらの CPU をすべて使用できるようにすると、再構築の方がインポートよりも高速に実行されることがあります。<br /><br /> フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。 このオプションは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースでのみ使用できます。<br /><br /> フルテキスト アップグレード オプションの選択については、「[フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)」をご覧ください。<br /><br /> 注:このプロパティを設定する[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、**フルテキスト アップグレード オプション**プロパティ。 詳細については、「 [サーバー インスタンスでのフルテキスト検索の管理と監視](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)」を参照してください。|  
|**verify_signature**|**int**|署名付きバイナリのみがフルテキスト エンジンによって読み込まれるかどうかを示します。 既定では、信頼された署名付きバイナリのみが読み込まれます。<br /><br /> 1 = 信頼された署名付きバイナリのみを確認して読み込む (既定値)<br /><br /> 0 = バイナリが署名付きかどうかを確認しない|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **serveradmin**固定サーバー ロールまたはシステム管理者が実行できる**sp_fulltext_service**します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-updating-the-list-of-registered-languages"></a>A. 登録された言語の一覧を更新します。  
 次の例では、フルテキスト検索に登録された言語の一覧を更新します。  
  
```  
EXEC sp_fulltext_service 'update_languages';  
GO  
```  
  
### <a name="b-changing-the-full-text-upgrade-option-to-reset-full-text-catalogs"></a>B. フルテキスト カタログをリセットするようにフルテキスト アップグレード オプションを変更する  
 次の例では、フルテキスト カタログをリセットするフルテキスト アップグレード オプションを変更します。 これに完全に削除されます。 この例で、省略可能な指定`@action`と`@value`キーワード。  
  
```  
EXEC sp_fulltext_service @action='upgrade_option', @value=1;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
