---
title: MSSQLSERVER_14421 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 14421 (Database Engine error)
ms.assetid: 03e76d4a-d463-4673-8843-08e4ecaefe27
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 495150983eefbd40515bbd35985d31f9ae3f3769
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033530"
---
# <a name="mssqlserver14421"></a>MSSQLSERVER_14421
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14421|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum14421|  
|メッセージ テキスト|ログ配布のセカンダリ データベース %s.%s は復元のしきい値が %d 分間ですが、同期されていません。復元は %d 分間実行されていません。 復元される待機時間は %d 分間です。 エージェント ログおよびログ配布モニターの情報を調べてください。|  
  
## <a name="explanation"></a>説明  
このメッセージは、復元のしきい値を超えてもログ配布が同期されていないことを示しています。 復元のしきい値は、復元操作が完了するまでの許容時間 (分数) です。この時間が経過すると警告メッセージが生成されます。  
  
### <a name="possible-causes"></a>考えられる原因  
このメッセージは、必ずしもログ配布に関する問題を示しません。 このメッセージは次の問題のいずれかを示す可能性があります。  
  
-   復元ジョブが実行されていない。  
  
    原因として、セカンダリ サーバー インスタンスで SQL Server エージェント サービスが実行されていないか、復元ジョブが無効になっているか、または復元ジョブのスケジュールが変更されていることが考えられます。  
  
-   復元ジョブが失敗している。  
  
    原因として、復元フォルダーのパスが有効でないか、ディスクがいっぱいになっているか、またはその他の理由で RESTORE ステートメントが失敗したことが考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
このメッセージが表示された場合は、次の方法で対処してください。  
  
-   セカンダリ サーバー インスタンスで SQL Server エージェント サービスが実行されていることを確認します。また、セカンダリ データベースの復元ジョブが有効になっており、適切な頻度で実行するようにスケジュール設定されていることを確認します。  
  
-   セカンダリ サーバーの復元ジョブが失敗している可能性があります。 この場合は、復元ジョブのジョブ履歴を参照して原因を探してください。  
  
-   セカンダリ サーバー インスタンスでログ配布の復元ジョブを実行する際、監視サーバー インスタンスに接続して **log_shipping_monitor_secondary** テーブルを更新できない可能性があります。 その場合、監視サーバー インスタンスとセカンダリ サーバー インスタンス間での認証に問題があると思われます。  
  
-   バックアップの警告のしきい値に、正しくない値が設定されている可能性があります。 この値は、復元ジョブの少なくとも 3 倍の頻度に設定するのが理想的です。 ログ配布を構成して有効にした後で、復元ジョブの頻度を変更した場合は、それに合わせて復元の警告しきい値も更新する必要があります。  
  
-   監視サーバー インスタンスがオフラインになり、その後オンラインに戻ったとき、警告メッセージ ジョブが実行される前に、**log_shipping_monitor_secondary** テーブルが現在の値に更新されません。 復元ジョブに成功し、"セカンダリ データベースに適用できるログ バックアップ ファイルが見つかりませんでした。" というメッセージが表示された場合に、エラー 14421 が発生することがあります。 このエラーが発生すると、復元時間は更新されません。 この場合のエラーの原因は、コピー ジョブに問題があります。  
  
    監視テーブルを更新して、セカンダリ データベースの最新データを反映させるには、セカンダリ サーバー インスタンスで **sp_refresh_log_shipping_monitor** を実行します。  
  
-   セカンダリ サーバー インスタンスまたは監視サーバー インスタンスで、日付または時刻が正しく設定されていません。 これが原因で、警告メッセージが生成される場合もあります。 これらいずれかのサーバーで、システムの日付または時刻が変更された可能性があります。  
  
    > [!NOTE]  
    > 2 つのサーバー インスタンスでタイム ゾーンが異なることによって、問題が発生することはありません。  
  
## <a name="see-also"></a>参照  
[log_shipping_monitor_secondary &#40;Transact-SQL&#41;](~/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)  
[ログ配布について &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
[sp_help_log_shipping_monitor_secondary &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)  
[sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)  
[ログ配布について &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
