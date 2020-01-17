---
title: Oracle CDC Service | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f3f3967b31331471d1ad0a886cc9eda853a25931
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771078"
---
# <a name="the-oracle-cdc-service"></a>Oracle CDC Service
  Oracle CDC Service は、プログラム xdbcdcsvc.exe を実行する Windows サービスです。 それぞれ異なる Windows サービス名を持つ複数の Windows サービスを、同じコンピューターで実行するように構成できます。 1 つのコンピューターで複数の Oracle CDC Windows サービスを作成する場合としては、サービス間の分離を強化したい場合や、各サービスでそれぞれ異なる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用する必要がある場合などが一般的です。  
  
 Oracle CDC Service は、Oracle CDC Service 構成コンソールを使用して作成されるか、xdbcdcsvc.exe プログラムに組み込まれているコマンド ライン インターフェイスを使用して定義されます。 どちらの場合も、作成された各 Oracle CDC Service は、1 つに関連付け[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス (クラスター化またはでミラー化された可能性がありますいる**AlwaysOn**セットアップ) と接続情報 (接続文字列とアクセス資格情報) はサービスの構成の一部です。  
  
 Oracle CDC Service が開始されると、関連付けられている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続が試行され、処理する必要がある Oracle CDC インスタンスの一覧が取得されて、環境の最初の検証が実行されます。 サービス開始時のエラーと、開始/停止の情報は、常に Windows アプリケーション イベント ログに書き込まれます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続が確立されると、すべてのエラーと情報メッセージが、 **インスタンスの MSXDBCDC データベースの** dbo.xdbcdc_trace [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに書き込まれます。 サービス開始時の検証では、たとえば、同じ名前の Oracle CDC Service が現在実行されていないかどうかが確認されます。 同じ名前のサービスが別のコンピューターから現在接続している場合は、Oracle CDC Service が wait ループに入り、そのサービスが切断されるのを待ってから処理が開始されます。  
  
 開始時の検証にすべて合格すると、MSXDBCDC データベースの **dbo.xdbcdc_databases** テーブルで、有効な Oracle CDC インスタンスがないかどうかが確認されます。 有効な Oracle CDC インスタンスが見つかるたびに、その Oracle CDC インスタンスを処理するサブプロセスが開始されます。  
  
 開始された Oracle CDC インスタンスは、同名の SQL Server CDC データベースにアクセスして、前回実行時の状態を取得します。 さらに、すべてが正常に実行されていることを確認します。 その後、変更の処理を再開して、Oracle トランザクション ログを読み取り、変更を CDC データベースに書き込みます。  
  
 Oracle CDC Service は、MSXDBCDC データベースの **dbo.xdbcdc_tables** テーブルを定期的に監視して、Oracle CDC インスタンスの構成に変更がないかどうかを確認します。 変更が見つかった場合は、構成の変更を確認する必要があることを Oracle CDC インスタンスに通知します。 ほとんどの構成変更 (キャプチャ インスタンスの追加や削除など) は、Oracle CDC インスタンスが有効な状態で適用できますが、Oracle CDC インスタンスを再起動する必要がある変更もあります。  
  
 Oracle CDC デザイナー コンソールを使用すると、変更が自動的に検出されます。 SQL を使用して直接 Oracle CDC の構成を更新する場合は、その構成変更が Oracle CDC Service によって検出されるように、次のプロシージャを呼び出す必要があります。  
  
```  
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 Oracle CDC インスタンス プロセスは、システム テーブル **cdc.xdbcdc_state** の状態を更新し、 **cdc.xdbcdc_trace** テーブルにエラー情報を書き込みます。 **xdbcdc_state** テーブルは、Oracle CDC インスタンスの状態を監視するのに役立ちます。 このテーブルには、最新の状態、さまざまなカウンター (Oracle から読み取られた変更の数、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に書き込まれた変更の数、書き込まれたコミット済みトランザクションの数、現在のインフライト トランザクションの数など)、および待機時間を示すデータが含まれています。  
  
 Oracle CDC インスタンスの構成は、 **cdc.xdbcdc_config** テーブルに保存されます。これは、Oracle CDC デザイナー コンソールによって操作されるテーブルです。 ターゲット [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと CDC データベースに Oracle CDC インスタンスのすべての構成が含まれているため、Oracle CDC インスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置スクリプトを作成することができます。 そのためには、Oracle CDC Service 構成コンソールと Oracle CDC デザイナー コンソールを使用します。  
  
## <a name="security-considerations"></a>セキュリティに関する考慮事項  
 CDC Service for Oracle を使用するためのセキュリティの要件を次に示します。  
  
### <a name="protection-of-source-oracle-data"></a>ソース Oracle のデータの保護  
 Oracle CDC Service は、Oracle ソース データへのアクセスを必要としません。保護のために、ログ マイニングの資格情報では顧客の Oracle テーブルに対する SELECT 権限が与えられないようになっています。  
  
### <a name="protection-of-source-oracle-change-data"></a>ソース Oracle の変更データの保護  
 Oracle CDC Service には、Oracle データベースの任意のテーブルに対する変更をキャプチャできるログ マイニングの資格情報が与えられています。 変更データには、通常のテーブルのような詳細なアクセス許可はないため、変更データにアクセスするときには、Oracle に組み込まれているアクセス制御がバイパスされます。  
  
 CDC データベースには、キャプチャ対象のソース Oracle テーブルと同じスキーマ名とテーブル名を持つ空のミラー テーブルがあります。 キャプチャされたデータは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のキャプチャ インスタンスに格納され、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからキャプチャされた変更と同じように保護されます。 キャプチャ インスタンスに関連付けられた変更データにアクセスするには、関連付けられたミラー テーブルのすべてのキャプチャ対象列に対する選択アクセスがユーザーに許可されている必要があります。 また、キャプチャ インスタンスの作成時にゲーティング ロールが指定されている場合、呼び出し元は、指定されたゲーティング ロールのメンバーである必要もあります。 メタデータにアクセスするためのその他の一般的な変更データ キャプチャ関数には、public ロールですべてのデータベース ユーザーがアクセスできます。ただし、通常は、返されるメタデータへのアクセスも、基になるソース テーブルに対する選択アクセス、および定義されたすべてのゲーティング ロールのメンバーシップに基づいて制限されます。  
  
 したがって、 **sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールを持つユーザーには、キャプチャされたデータへのフル アクセス権が (既定で) 与えられ、さらなるアクセスは、ゲーティング ロールを使用するか、キャプチャ対象列に対する選択アクセスを許可することによって許可できます。  
  
### <a name="protection-of-source-oracle-log-mining-credentials"></a>ソース Oracle のログ マイニングの資格情報の保護  
 CDC データベース (の cdc.xdbcdc_config テーブル) に格納されている Oracle CDC Service の構成には、ログ マイニング ユーザー名と、関連付けられているパスワードが含まれています。  
  
 ログ マイニング パスワードは、次のコマンドによって自動的に作成される、 `xdbcdc_asym_key` という固定名を持つ非対称キーを使用して暗号化されて格納されます。  
  
```  
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 別のアルゴリズムを使用する場合は、このキーを削除して、同じパスワードで暗号化される同じ名前の新しいキーを作成します。  
  
 非対称キーのパスワードは、レジストリのパス **HKLM\Software\Microsoft\XDBCDCSVC\\<service-name>** に保存されているマスター パスワードです。 このレジストリ キーにアクセスできるのは、ローカル管理者と Oracle CDC Windows サービス アカウントだけです。 このレジストリ キーには、非対称キーのパスワードを格納する、暗号化されたバイナリ値 **AsymmetricKeyPassword** が含まれています。 Oracle ログ マイニングの資格情報にアクセスするには、このレジストリ キーにアクセスできる必要があります。  
  
 ENCRYPTION BY PASSWORD 句を使用するには、パスワードが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピューターの Windows パスワード ポリシーの要件を満たしている必要があります。 したがって、そのポリシーに従って非対称キーのパスワードを選択する必要があります。  
  
 非対称キーのパスワードが失われた場合は、Oracle CDC Service デザイナーで、各 Oracle CDC インスタンスのログ マイニングの資格情報を指定し直す必要があります。  
  
 この非対称キーがない Oracle インスタンス CDC データベースが検出された場合や、キーはあってもパスワードが一致しない場合は、非対称キーが自動的に CDC データベースに作成されます。  
  
### <a name="oracle-cdc-service-windows-service-account"></a>Oracle CDC Service の Windows サービス アカウント  
 Oracle CDC Windows サービスで使用するサービス アカウントには、その他の特権は不要です。 このアカウントは、Oracle Native Client API と SQL Server Native Client ODBC API の両方を使用できる必要があります。 また、レジストリのサービス構成キーにアクセスできる必要もあります (この CDC Service 構成コンソールでは、そのための ACL が設定されます)。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [高可用性のサポート](high-availability-support.md)  
  
-   [CDC Service で使用する SQL Server 接続に必要なアクセス許可](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [Change Data Capture Service for Oracle by Attunity のユーザー ロール](user-roles.md)  
  
-   [Oracle CDC Service を使用する](the-oracle-cdc-service.md)  
  
## <a name="see-also"></a>関連項目  
 [ローカルの CDC Service を管理する方法](how-to-manage-a-local-cdc-service.md)   
 [Oracle CDC Service の管理](manage-an-oracle-cdc-service.md)  
  
  
