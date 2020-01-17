---
title: 修正済みバグの一覧 |Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 2b939db6ac0f89075b39ba74eadb0e86e63e3980
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041225"
---
# <a name="list-of-bugs-fixed"></a>修正済みバグの一覧

このページには、各リリースで修正されたバグの一覧が含まれています。 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-1742-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

 - プロセス ID とアプリケーション名が SQL Server に正しく送信されない問題を修正しました (_exec_sessions 分析の場合) (Linux)
 - Libuuid の冗長な依存関係が削除されました (Linux)
 - SQL Server 2019 に UTF8 データを送信するバグの修正
 - "@euro" で終わるロケールが正しく検出されなかったバグを修正しました (Linux)
 - を使用しているときに、出力パラメーターとしてフェッチされたときに XML データが誤って返されることを修正しました Always Encrypted

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-174-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC ドライバー17.4 でのバグ修正

- 複数のアクティブな結果セット (MARS) が有効になっている場合に断続的にハングするように修正
- 非同期通知が有効になっているときに接続の復元がハングする問題を修正する
- マルチスレッド接続試行の診断レコードを取得するときのクラッシュを修正します
- SQL_USER_NAME および SQL_DATA_SOURCE_READ_ONLY で SQLGetInfo () を呼び出した後、再接続時に ' 暗号化がサポートされていない ' を修正します。
- Azure Active Directory 対話型認証の実行中の COM 初期化エラーを修正します
- 複数バイトの UTF8 データの SQLGetData () を修正します。
- SQLGetData () を使用した sql_variant 列の長さの取得を修正しています
- Bcp を使用して、7992バイトを超える sql_variant 列のインポートを修正します。
- ナロー文字データの正しいエンコードをサーバーに送信することを修正しています

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用の [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC ドライバー17.3 でのバグ修正

- TCP 送信通知イベントハンドルのメモリリークを修正します。
- Msodbcsql .h ヘッダーファイルの enum _SQL_FILESTREAM_DESIRED_ACCESS の再定義の問題を修正した
- Linux 用の msodbcsql .h ヘッダーファイルで、不足している ACCESS_TOKEN と認証に関連する定義を修正した

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用の [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC ドライバー17.2 でのバグ修正

- Azure Active Directory 認証に関するエラーメッセージを修正した
- ロケール環境変数の設定が異なる場合のエンコード検出を修正します。
- 接続の回復が進行中の切断時のクラッシュを修正した
- 接続の活性の検出を修正した
- 閉じたソケットの誤った検出を修正しました
- 復旧に失敗したときにステートメントハンドルを解放しようとしたときに無期限に待機することを修正しました
- Windows にバージョン13と17の両方がインストールされている場合に、正しくないアンインストール動作を修正しました
- 以前の Windows プラットフォーム (Windows 7、8、および Server 2012) での復号化動作を修正した
- Windows で ADAL 認証を使用するときのキャッシュの問題を修正した
- Windows 上のトレースログをロックして上書きしていた問題を修正しました

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用の [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC ドライバー17.1 でのバグ修正

- MARS が有効になっている SQLFreeHandle と接続属性 "Encrypt = yes" を呼び出したときの1秒の遅延を修正しました
- 渡されたバッファーのサイズが小さい場合、SQLGetData でエラー22003クラッシュが発生する問題を修正しました (Windows)
- 切り詰められた ADAL エラーメッセージを修正しました
- 浮動小数点数を整数に変換するときに、32ビット Windows でのまれなバグを修正した
- Always Encrypted on にして double を decimal フィールドに挿入すると、データの切り捨てエラーが返される問題を修正した
- MacOS インストーラーの警告を修正します。
- 接続の回復性と接続プールの両方が有効になっていて、サーバーによってセッションが削除される場合に、セッションの回復試行中に SQL Server に正しくない状態を送信することを修正しました

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- Kerberos 認証を使用すると、一括挿入が "アクセスが拒否されました" というエラーで失敗するバグを修正しました
- 2\.3.1 より前のバージョンに存在する unixODBC バグの回避策を削除しました (ドライバーは、unixODBC に渡された特定のバッファーのサイズを2倍にしました)
- ColumnEncryption = enabled を使用したときの接続の回復性 (再接続) の切断を修正しました
- DSN 作成のバグを修正しました。 [対話型認証を Active Directory する] オプションを使用すると、Azure 認証ウィンドウが応答しなくなる可能性があります (Windows)
- 非同期実行が有効になっている (接続ハンドルのクリア時に発生する) ときの ODBC シャットダウン中のまれなクラッシュを修正しました。
- 長いストアドプロシージャの実行中に SQL ドライバーが CPU 使用率が高くなる問題を修正しました。
- 暗号化された varbinary (max) 列のデータを変換せずに取得できないことを修正した
- 静的カーソルで SQLGetData () を使用して null の varchar (max) 暗号化列がフェッチされた後で、データがある場合でも、次の列も nulled する問題を修正しました。
- Always Encrypted での varbinary (max) フィールドのフェッチに関する問題を修正しています
- Always Encrypted で動作しない setlocale () の問題を修正した
- Always Encrypted を含む XML 型のストアドプロシージャパラメーターで呼び出されたときに、SQLDescribeParam () によってエラーが返される問題を修正しました
- SQLTables で動作しないエスケープされたアンダースコアを修正
- Linux でワイド文字として返されたときにヘブライ語データ (varchar) が切り捨てられるバグを修正しました
- UTF-8 アプリケーションからの shift-jis でエンコードされた char/varchar のクエリに関する問題を修正した
- SQL_DRIVER_NAME parameter で SQLGetInfo を呼び出して MacOS で Linux 形式のファイル名が返されるバグを修正しました
- BCP ユーティリティを使用して、32k バイトを超える入力ファイルを使用して VARCHAR 列に Windows-1252 文字データを読み込むとエラーが発生する問題を修正しています。
