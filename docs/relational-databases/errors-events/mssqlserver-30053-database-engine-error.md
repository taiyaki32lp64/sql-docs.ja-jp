---
title: MSSQLSERVER_30053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
ms.assetid: 8ad23889-e243-4bd7-bc3e-150403399d89
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2773c43695f67cc6d3878f1885686e74e84e67c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039311"
---
# <a name="mssqlserver30053"></a>MSSQLSERVER_30053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|30053|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|メッセージ テキスト|フルテキスト クエリ文字列の単語区切り処理がタイムアウトしました。 このタイムアウトは、ワード ブレーカーによるフルテキスト クエリ文字列の処理が長時間かかったか、サーバー上で実行されているクエリ数が多い場合に発生する可能性があります。 負荷を少なくしてクエリの再実行を試みてください。|  
  
## <a name="explanation"></a>説明  
単語区切りのタイムアウト エラーは、次の状況で発生する可能性があります。  
  
-   クエリ言語のワード ブレーカーが正しく構成されていない場合。たとえば、レジストリ設定が正しくない場合です。  
  
-   ワード ブレーカーが特定のクエリ文字列に対して誤動作する。  
  
-   ワード ブレーカーが特定のクエリ文字列に対して過剰なデータを返す。 過剰なデータは、バッファー オーバーラン攻撃を引き起こす可能性のあるものとして処理されます。これにより、単語区切りサービスをホストする、フィルター デーモン プロセス (fdhost.exe) がシャットダウンされます。  
  
-   フィルター デーモン プロセスの構成が正しくない。  
  
    パスワードの期限が切れている場合、またはドメイン ポリシーが原因でフィルター デーモン アカウントがログオンできない場合。この 2 つは、最も一般的な構成上の問題です。  
  
-   クエリが集中的に行われるワークロードをサーバー インスタンスで実行している場合。たとえば、ワード ブレーカーによるフルテキスト クエリ文字列の処理が長時間かかったり、多数のクエリがサーバー上で実行されている場合です。 この状況がエラーの原因になることはまれです。  
  
## <a name="user-action"></a>ユーザーの操作  
次に示すように、タイムアウトについて考えられる原因に適した、ユーザーのアクションを選択してください。  
  
|考えられる原因|ユーザーのアクション|  
|------------------|---------------|  
|クエリ言語のワード ブレーカーが正しく構成されていない。|サード パーティ製のワード ブレーカーを使用しているとき、ワード ブレーカーがオペレーティング システムに正しく登録されていない場合があります。 この場合は、ワード ブレーカーを再登録してください。 詳細については、「[Revert the Word Breakers Used by Search to the Previous Version](~/relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)」(検索で使用するワード ブレーカーを以前のバージョンに戻す) を参照してください。|  
|ワード ブレーカーが特定のクエリ文字列に対して誤動作する。|ワード ブレーカーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされている場合は、マイクロソフト カスタマー サポート サービスに問い合わせてください。|  
|ワード ブレーカーが特定のクエリ文字列に対して過剰なデータを返す。|ワード ブレーカーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされている場合は、マイクロソフト カスタマー サポート サービスに問い合わせてください。|  
|フィルター デーモン プロセスの構成が正しくない。|正しいパスワードを使用していることと、フィルター デーモン アカウントのログオンがドメイン ポリシーによって拒否されていないことを確認してください。|  
|クエリが集中的に行われるワークロードをサーバー インスタンスで実行している。|負荷を少なくしてクエリの再実行を試みてください。|  
  
## <a name="see-also"></a>参照  
[フルテキスト フィルター デーモン ランチャーのサービス アカウントの設定](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[フルテキスト検索](~/relational-databases/search/full-text-search.md)  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[検索用のワード ブレーカーとステミング機能の構成と管理](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[検索用フィルターの構成と管理](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
