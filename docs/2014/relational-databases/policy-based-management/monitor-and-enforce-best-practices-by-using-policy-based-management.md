---
title: ポリシー ベースの管理を使用したベスト プラクティスの監視と実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bfc7cc16c9751ebdf64a8e9cd110547255c944ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62626049"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>ポリシー ベースの管理を使用したベスト プラクティスの監視と実行
  ポリシー ベースの管理を許可するためのベスト プラクティスの監視、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ベスト プラクティスのポリシーとしてインポートし、インスタンス、インスタンス オブジェクト、データベース、またはデータベース オブジェクトを含む対象セットに対してポリシーを評価できる一連のポリシー ファイルを提供します。 ポリシーを手動で評価したり、スケジュールまたはイベントに従って対象セットを評価するようにポリシーを設定したりできます。 条件と各ファセットおよびポリシーとの関係の詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](administer-servers-by-using-policy-based-management.md)」を参照してください。  
  
## <a name="policy-and-rules-for-database-engine"></a>データベース エンジンのポリシーとルール  
 次の表に、ポリシーのインストールに含まれている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と各ポリシーで評価するベスト プラクティス ルールに関する情報が含まれています。 ポリシーは XML ファイルとして格納され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にインポートする必要があります。 ポリシーのインポート方法については、「 [ポリシー ベースの管理ポリシーのインポート](import-a-policy-based-management-policy.md)」を参照してください。  
  
|ポリシー名|ベスト プラクティス ルール|  
|-----------------|------------------------|  
|非対称キーの暗号化アルゴリズム|[非対称キー暗号化の強度](asymmetric-keys-encryption-strength.md)|  
|バックアップ ファイルとデータ ファイルの場所|[バックアップ ファイルはデータベース ファイルとは別のデバイスに配置する](../../database-engine/backup-files-must-be-on-separate-devices-from-the-database-files.md)|  
|データ ファイルとログ ファイルの場所|[別々のドライブへのデータ ファイルとログ ファイルの配置](place-data-and-log-files-on-separate-drives.md)|  
|データベースの自動終了|[AUTO_CLOSE データベース オプションを OFF に設定](set-the-auto-close-database-option-to-off.md)|  
|データベースの自動圧縮|[AUTO_SHRINK データベース オプションを OFF に設定](set-the-auto-shrink-database-option-to-off.md)|  
|データベースの照合順序|[ユーザー定義データベースの照合順序が master データベースおよび model データベースの照合順序と一致するように設定](../../database-engine/set-collation-user-defined-databases-match-master-model-databases.md)|  
|データベースのページ検証|[PAGE_VERIFY データベース オプションを CHECKSUM に設定](set-the-page-verify-database-option-to-checksum.md)|  
|データベースのページの状態|[問題のあるページを含むデータベースの整合性のチェック](check-integrity-of-database-with-suspect-pages.md)|  
|guest の権限|[ユーザー データベースに対する guest の権限](guest-permissions-on-user-databases.md)|  
|最後にバックアップが正常終了した日付|[期限切れのバックアップ](outdated-backup.md)|  
|パブリックに許可されていないサーバー権限|[サーバーのパブリック権限](server-public-permissions.md)|  
|SQL Server の 32 ビットの関係マスクの重複|[正しい Affinity Mask オプションと関係マスクの重複の入出力](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server 64 ビットの関係マスクの重複|[正しい Affinity Mask オプションと関係マスクの重複の入出力](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server 関係マスク|[関係マスクの既定値の保持](keep-the-affinity-mask-default-value.md)|  
|SQL Server のブロック対象プロセスのしきい値|[blocked process threshold の増加または無効化](increase-or-disable-blocked-process-threshold.md)|  
|SQL Server の既定のトレース|[既定のトレース ログ ファイルの無効化](default-trace-log-files-disabled.md)|  
|SQL Server の動的ロック|[locks 構成オプションの既定値の保持](keep-the-locks-configuration-option-default-value.md)|  
|SQL Server の簡易プーリング|[簡易プーリングの無効化](disable-lightweight-pooling.md)|  
|SQL Server のログイン モード|[認証モードの選択](../security/choose-an-authentication-mode.md)|  
|SQL Server の並列処理の最大限度|[最適なパフォーマンスを実現するための max degree of parallelism オプションの設定](set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|SQL Server のワーカー スレッドの最大数 (32 ビット版 SQL Server 2000)|[max worker threads 設定の検証](verify-max-worker-threads-setting.md)|  
|SQL Server のワーカー スレッドの最大数 (64 ビット版 SQL Server 2000)|[max worker threads 設定の検証](verify-max-worker-threads-setting.md)|  
|SQL Server のワーカー スレッドの最大数 (SQL Server 2005 以降)|[max worker threads 設定の検証](verify-max-worker-threads-setting.md)|  
|SQL Server のネットワーク パケット サイズ|[ネットワーク パケット サイズは 8060 バイトを超えることはできない](network-packet-size-should-not-exceed-8060-bytes.md)|  
|SQL Server のパスワードの期限|[SQL Server ログイン パスワードの有効期限](sql-server-login-password-expiration.md)|  
|SQL Server のパスワード ポリシー|[SQL Server ログイン パスワードの強度](sql-server-login-password-strength.md)|  
|ユーザー データベースの対称キー暗号化|[ユーザー データベースの対称キー](symmetric-keys-on-user-databases.md)|  
|master データベースの対称キー|[システム データベースの対称キー](symmetric-keys-on-system-databases.md)|  
|システム データベースの対称キー|[システム データベースの対称キー](symmetric-keys-on-system-databases.md)|  
|信頼可能データベース|[信頼可能なビット](trustworthy-bit.md)|  
|Windows イベント ログのクラスター ディスク リソース破損エラー|[SCSI ホスト アダプターの問題の検出](detect-scsi-host-adapter-issues.md)|  
|Windows イベント ログのデバイス ドライバー制御エラー|[デバイス ドライバー制御エラー](device-driver-control-error.md)|  
|Windows イベント ログのデバイス準備未完了エラー|[デバイス準備未完了エラー](device-not-ready-error.md)|  
|Windows イベント ログの I_O 要求失敗エラー|[失敗した入出力要求を検出します。](detect-failed-input-and-output-requests.md)|  
|Windows イベント ログの I_O 遅延警告|[ディスク I/O サブシステムの I/O 遅延問題の確認](check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Windows イベント ログのハード ページ フォールト エラー時の I_O エラー|[ハード ページ フォールト中の I/O エラー](input-and-output-error-during-hard-page-fault.md)|  
|Windows イベント ログの読み取り再試行エラー|[ディスク I/O サブシステムの読み取り再試行の問題の確認](check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Windows イベント ログのストレージ システム I_O タイムアウト エラー|[ストレージ システムの入出力のタイムアウト](storage-system-input-output-time-out.md)|  
|Windows イベント ログのシステム障害エラー|[予期しないシステム障害](unexpected-system-failures.md)|  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理ファセットの操作](working-with-policy-based-management-facets.md)  
  
  
