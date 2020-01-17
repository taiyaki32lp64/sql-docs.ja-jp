---
title: ポリシーベースの管理を使用したベスト プラクティスの監視と実行
description: ポリシーベースの管理では、ベスト プラクティス ポリシーとしてインポートできる一連のポリシー ファイルが提供され、インスタンス、インスタンス オブジェクト、データベース、またはデータベース オブジェクトを含む対象セットに対してポリシーが評価されます。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54fdfe36da0d590fa2225ab7cc99af640727b000
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557680"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>ポリシー ベースの管理を使用したベスト プラクティスの監視と実行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ポリシー ベースの管理では、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のベスト プラクティスを監視できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はベスト プラクティス ポリシーとしてインポートできる一連のポリシー ファイルを提供し、インスタンス、インスタンス オブジェクト、データベース、またはデータベース オブジェクトを含む対象セットに対してポリシーを評価します。 ポリシーを手動で評価したり、スケジュールまたはイベントに従って対象セットを評価するようにポリシーを設定したりできます。 条件と各ファセットおよびポリシーとの関係の詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)」を参照してください。  
  
## <a name="policy-and-rules-for-database-engine"></a>データベース エンジンのポリシーとルール  
 次の表に、インストールした [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に用意されているポリシーと、各ポリシーで評価するベスト プラクティス ルールに関する情報を示します。 ポリシーは XML ファイルとして格納され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にインポートする必要があります。 ポリシーのインポート方法については、「 [ポリシー ベースの管理ポリシーのインポート](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)」を参照してください。  
  
|ポリシー名|ベスト プラクティス ルール|  
|-----------------|------------------------|  
|非対称キーの暗号化アルゴリズム|[非対称キー暗号化の強度](../../relational-databases/policy-based-management/asymmetric-keys-encryption-strength.md)|  
|バックアップ ファイルとデータ ファイルの場所|[バックアップ ファイルはデータベース ファイルとは別のデバイスに配置する](https://msdn.microsoft.com/library/7039bebb-1f25-4cf3-81f1-393dfb78da12)|  
|データ ファイルとログ ファイルの場所|[別々のドライブへのデータ ファイルとログ ファイルの配置](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)|  
|データベースの自動終了|[AUTO_CLOSE データベース オプションを OFF に設定](../../relational-databases/policy-based-management/set-the-auto-close-database-option-to-off.md)|  
|データベースの自動圧縮|[AUTO_SHRINK データベース オプションを OFF に設定](../../relational-databases/policy-based-management/set-the-auto-shrink-database-option-to-off.md)|  
|データベースの照合順序|[ユーザー定義データベースの照合順序が master データベースおよび model データベースの照合順序と一致するように設定](https://msdn.microsoft.com/library/c686446f-dae1-4b05-a3df-837b3422988d)|  
|データベースのページ検証|[PAGE_VERIFY データベース オプションを CHECKSUM に設定](../../relational-databases/policy-based-management/set-the-page-verify-database-option-to-checksum.md)|  
|データベースのページの状態|[問題のあるページを含むデータベースの整合性のチェック](../../relational-databases/policy-based-management/check-integrity-of-database-with-suspect-pages.md)|  
|guest の権限|[ユーザー データベースに対する guest の権限](../../relational-databases/policy-based-management/guest-permissions-on-user-databases.md)|  
|最後にバックアップが正常終了した日付|[期限切れのバックアップ](../../relational-databases/policy-based-management/outdated-backup.md)|  
|パブリックに許可されていないサーバー権限|[サーバーのパブリック権限](../../relational-databases/policy-based-management/server-public-permissions.md)|  
|SQL Server 64 ビットの関係マスクの重複|[affinity mask と affinity I/O mask の重複の修正](../../relational-databases/policy-based-management/correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server 関係マスク|[関係マスクの既定値の保持](../../relational-databases/policy-based-management/keep-the-affinity-mask-default-value.md)|  
|SQL Server のブロック対象プロセスのしきい値|[blocked process threshold の増加または無効化](../../relational-databases/policy-based-management/increase-or-disable-blocked-process-threshold.md)|  
|SQL Server の既定のトレース|[既定のトレース ログ ファイルの無効化](../../relational-databases/policy-based-management/default-trace-log-files-disabled.md)|  
|SQL Server の動的ロック|[locks 構成オプションの既定値の保持](../../relational-databases/policy-based-management/keep-the-locks-configuration-option-default-value.md)|  
|SQL Server の簡易プーリング|[簡易プーリングの無効化](../../relational-databases/policy-based-management/disable-lightweight-pooling.md)|  
|SQL Server のログイン モード|[認証モードの選択](../../relational-databases/security/choose-an-authentication-mode.md)|  
|SQL Server の並列処理の最大限度|[最適なパフォーマンスを実現するための max degree of parallelism オプションの設定](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|SQL Server のワーカー スレッドの最大数 (32 ビット版 SQL Server 2000)|[max worker threads 設定の検証](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server のワーカー スレッドの最大数 (64 ビット版 SQL Server 2000)|[max worker threads 設定の検証](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server のワーカー スレッドの最大数 (SQL Server 2005 以降)|[max worker threads 設定の検証](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server のネットワーク パケット サイズ|[ネットワーク パケット サイズは 8060 バイトを超えることはできない](../../relational-databases/policy-based-management/network-packet-size-should-not-exceed-8060-bytes.md)|  
|SQL Server のパスワードの期限|[SQL Server ログイン パスワードの有効期限](../../relational-databases/policy-based-management/sql-server-login-password-expiration.md)|  
|SQL Server のパスワード ポリシー|[SQL Server ログイン パスワードの強度](../../relational-databases/policy-based-management/sql-server-login-password-strength.md)|  
|ユーザー データベースの対称キー暗号化|[ユーザー データベースの対称キー](../../relational-databases/policy-based-management/symmetric-keys-on-user-databases.md)|  
|master データベースの対称キー|[システム データベースの対称キー](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|システム データベースの対称キー|[システム データベースの対称キー](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|信頼可能データベース|[信頼可能なビット](../../relational-databases/policy-based-management/trustworthy-bit.md)|  
|Windows イベント ログのクラスター ディスク リソース破損エラー|[SCSI ホスト アダプターの問題の検出](../../relational-databases/policy-based-management/detect-scsi-host-adapter-issues.md)|  
|Windows イベント ログのデバイス ドライバー制御エラー|[デバイス ドライバー制御エラー](../../relational-databases/policy-based-management/device-driver-control-error.md)|  
|Windows イベント ログのデバイス準備未完了エラー|[デバイス準備未完了エラー](../../relational-databases/policy-based-management/device-not-ready-error.md)|  
|Windows イベント ログの I_O 要求失敗エラー|[I/O 要求失敗の検出](../../relational-databases/policy-based-management/detect-failed-input-and-output-requests.md)|  
|Windows イベント ログの I_O 遅延警告|[ディスク I/O サブシステムの I/O 遅延問題の確認](../../relational-databases/policy-based-management/check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Windows イベント ログのハード ページ フォールト エラー時の I_O エラー|[ハード ページ フォールト中の I/O エラー](../../relational-databases/policy-based-management/input-and-output-error-during-hard-page-fault.md)|  
|Windows イベント ログの読み取り再試行エラー|[ディスク I/O サブシステムの読み取り再試行の問題の確認](../../relational-databases/policy-based-management/check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Windows イベント ログのストレージ システム I_O タイムアウト エラー|[ストレージ システムの入出力のタイムアウト](../../relational-databases/policy-based-management/storage-system-input-output-time-out.md)|  
|Windows イベント ログのシステム障害エラー|[予期しないシステム障害](../../relational-databases/policy-based-management/unexpected-system-failures.md)|  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理ファセットの操作](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)  
  
  
