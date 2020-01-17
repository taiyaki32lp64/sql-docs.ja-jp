---
title: データベース エンジンの非推奨の機能 | Microsoft Docs
titleSuffix: SQL Server 2019
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [SQL Server]
- Database Engine [SQL Server], backward compatibility
- deprecation [SQL Server], feature list
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e9616620b0d8683d0158bfb76b5145f1bff52054
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258016"
---
# <a name="deprecated-database-engine-features-in-sql-server-2017"></a>SQL Server 2017 データベース エンジンの非推奨の機能
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  このトピックでは、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] でまだ使用できるものの、非推奨とされた [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]の機能について説明します。 非推奨の機能を新しいアプリケーションで使用しないでください。  
  
機能に非推奨の印が付いている場合、それは次のことを意味します。
-  その機能は保守管理状態にあり、それ以外では利用されていません。 新しい変更は行われません。新しい機能との相互運用性に関する変更もありません。
-  Microsoft は、アップグレードを容易にする目的で、今後のリリースから非推奨機能を外さないように努めます。 ただし、非推奨機能が将来の技術革新を制限してしまう場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からそれを永久的に外すことをまれに選択することがあります。
-  新しい開発作業に非推奨機能を使用することはお勧めしません。      
  
非推奨の機能の使用は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Deprecated Features オブジェクトのパフォーマンス カウンターおよびトレース イベントを使用して監視できます。 詳細については、「 [SQL Server オブジェクトの使用](../relational-databases/performance-monitor/use-sql-server-objects.md)」を参照してください。  
  
これらのカウンターの値は、次のステートメントを実行して入手することもできます。  
  
```sql  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

> [!NOTE]  
> このリストは、[!INCLUDE[sssql15-md](../includes/sssql15-md.md)] のリストと同じです。 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] で提供が終了または中止されることが新しく発表されたデータベース エンジン機能はありません。

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>SQL Server の次のバージョンで非推奨となっている機能  
次の [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 機能は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の次のバージョンでは非推奨となります。 新規の開発作業ではこれらの機能を使用しないようにし、現在これらの機能を使用しているアプリケーションはできるだけ早く修正してください。 **機能名**の値は、トレース イベントには ObjectName として表示され、パフォーマンス カウンターと `sys.dm_os_performance_counters` にはインスタンス名として表示されます。 **機能 ID** の値は、トレース イベントに ObjectId として表示されます。  
  
|カテゴリ|非推奨の機能|代替|機能名|機能 ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|バックアップと復元|RESTORE { DATABASE &#124; LOG } WITH [MEDIA]PASSWORD はこれまでどおり非推奨とされます。 BACKUP { DATABASE &#124; LOG } WITH PASSWORD および BACKUP { DATABASE &#124; LOG } WITH MEDIAPASSWORD は廃止されました。|[なし] :|BACKUP DATABASE または LOG WITH PASSWORD<br /><br /> BACKUP DATABASE または LOG WITH MEDIAPASSWORD|104<br /><br /> 103|  
|互換性レベル|バージョン 100 ([!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]) からのアップグレード。|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] バージョンが[サポート](https://aka.ms/sqllifecycle)対象外になったとき、関連するデータベース互換性レベルには非推奨の印が付きます。 しかしながら、Microsoft は、アップグレードを簡単にする目的で、サポートされているあらゆるデータベース互換性レベルで認められているアプリケーションのサポートを可能な限り継続します。 互換性レベルの詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。|Database compatibility level 100|108|  
|データベース オブジェクト|トリガーから結果セットを返す機能|なし|トリガーから結果を返す|12|  
|暗号化|RC4 または RC4_128 を使用した暗号化は非推奨とされており、次のバージョンで削除される予定です。 RC4 および RC4_128 の暗号化解除は非推奨とされます。|AES など、別の暗号化アルゴリズムを使用してください。|非推奨の暗号化アルゴリズム|253|    
|ハッシュ アルゴリズム|MD2、MD4、MD5、SHA、および SHA1 の使用は非推奨とされます。|代わりに SHA2_256 または SHA2_512 を使用してください。 以前のアルゴリズムは引き続き機能しますが、Deprecation イベントが発生します。|非推奨のハッシュ アルゴリズム|なし|  
|リモート サーバー|sp_addremotelogin<br /><br /> sp_addserver<br /><br /> sp_dropremotelogin<br /><br /> sp_helpremotelogin<br /><br /> sp_remoteoption|リンク サーバーを使用してリモート サーバーを置き換えてください。 sp_addserver は、ローカル オプションでのみ使用できます。|sp_addremotelogin<br /><br /> sp_addserver<br /><br /> sp_dropremotelogin<br /><br /> sp_helpremotelogin<br /><br /> sp_remoteoption|70<br /><br /> 69<br /><br /> 71<br /><br /> 72<br /><br /> 73|  
|リモート サーバー|\@\@remserver|リンク サーバーを使用してリモート サーバーを置き換えてください。|なし|なし|  
|リモート サーバー|SET REMOTE_PROC_TRANSACTIONS|リンク サーバーを使用してリモート サーバーを置き換えてください。|SET REMOTE_PROC_TRANSACTIONS|110|  
|SET オプション|**SET ROWCOUNT** 、 **INSERT**、および **UPDATE**ステートメントの **DELETE**|TOP キーワード|SET ROWCOUNT|109|  
|テーブル ヒント|HOLDLOCK table hint without parenthesis|かっこ付きの HOLDLOCK を使用します。|HOLDLOCK table hint without parenthesis|167|  
  
## <a name="features-deprecated-in-a-future-version-of-sql-server"></a>SQL Server の将来のバージョンで非推奨となっている機能  
 次の [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の次のバージョンではサポートされますが、その後のバージョンでは非推奨となります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のどのバージョンであるかは決定していません。  
  
|カテゴリ|非推奨の機能|代替|機能名|機能 ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|互換性レベル|sp_dbcmptlevel|ALTER DATABASE ...SET COMPATIBILITY_LEVEL です。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。|sp_dbcmptlevel|80|  
|互換性レベル|データベース互換性レベル 110 および 120。|今後のリリースでデータベースおよびアプリケーションのアップグレードを計画してください。 しかしながら、Microsoft は、アップグレードを簡単にする目的で、サポートされているあらゆるデータベース互換性レベルで認められているアプリケーションのサポートを可能な限り継続します。 互換性レベルの詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。|データベース互換性レベル 110<br /><br /> データベース互換性レベル 120||  
|XML|インライン XDR スキーマの生成|FOR XML オプションに対する XMLDATA ディレクティブは非推奨とされます。 RAW モードと AUTO モードの場合は、XSD 世代を使用してください。 EXPLICIT モードでは、XMLDATA ディレクティブに代わる機能はありません。|XMLDATA|181|  
|バックアップと復元|BACKUP { DATABASE &#124; LOG } TO TAPE<br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape*|BACKUP { DATABASE &#124; LOG } TO DISK<br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk*|BACKUP DATABASE または LOG TO TAPE|235|  
|バックアップと復元|sp_addumpdevice '**tape**'|sp_addumpdevice '**disk**'|ADDING TAPE DEVICE|236|  
|バックアップと復元|sp_helpdevice|sys.backup_devices|sp_helpdevice|100|  
|照合順序|Korean_Wansung_Unicode<br /><br /> Lithuanian_Classic<br /><br /> SQL_AltDiction_CP1253_CS_AS|[なし] : これらの照合順序は [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]に存在しますが、fn_helpcollations には表示されません。|Korean_Wansung_Unicode<br /><br /> Lithuanian_Classic<br /><br /> SQL_AltDiction_CP1253_CS_AS|191<br /><br /> 192<br /><br /> 194|  
|照合順序|ヒンディー語<br /><br /> マケドニア語|これらの照合順序は [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 以降に存在しますが、fn_helpcollations には表示されません。 代わりに Macedonian_FYROM_90 および Indic_General_90 を使用してください。|ヒンディー語<br /><br /> マケドニア語|190<br /><br /> 193|  
|照合順序|Azeri_Latin_90<br /><br /> Azeri_Cyrilllic_90|Azeri_Latin_100<br /><br /> Azeri_Cyrilllic_100|Azeri_Latin_90<br /><br /> Azeri_Cyrilllic_90|232<br /><br /> 233|  
|構成|SET ANSI_NULLS OFF および ANSI_NULLS OFF データベース オプション<br /><br /> SET ANSI_PADDING OFF および ANSI_PADDING OFF データベース オプション<br /><br /> SET CONCAT_NULL_YIELDS_NULL OFF および CONCAT_NULL_YIELDS_NULL OFF データベース オプション<br /><br /> SET OFFSETS|[なし] :<br /><br /> ANSI_NULLS、ANSI_PADDING、および CONCAT_NULLS_YIELDS_NULL は常に ON に設定されます。 SET OFFSETS は使用できなくなります。|SET ANSI_NULLS OFF<br /><br /> SET ANSI_PADDING OFF<br /><br /> SET CONCAT_NULL_YIELDS_NULL OFF<br /><br /> SET OFFSETS<br /><br /> ALTER DATABASE SET ANSI_NULLS OFF<br /><br /> ALTER DATABASE SET ANSI_PADDING OFF<br /><br /> ALTER DATABASE SET CONCAT_NULL_YIELDS_NULL OFF|111<br /><br /> 113<br /><br /> 112<br /><br /> 36<br /><br /> 111<br /><br /> 113<br /><br /> 112|  
|データ型|sp_addtype<br /><br /> sp_droptype|CREATE TYPE<br /><br /> DROP TYPE|sp_addtype<br /><br /> sp_droptype|62<br /><br /> 63|  
|データ型|**timestamp** データ型の **rowversion** 構文|**rowversion** データ型の構文|timestamp|158|  
|データ型|**timestamp** 列に null 値を挿入する機能|代わりに DEFAULT を使用してください。|TIMESTAMP 列への INSERT NULL|179|  
|データ型|'text in row' テーブル オプション|**varchar(max)** 、**nvarchar(max)** 、および **varbinary(max)** データ型を使用してください。 詳細については、「[sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。|Text in row テーブル オプション|9|  
|データ型|データ型:<br /><br /> **text**<br /><br /> **ntext**<br /><br /> **画像**|**varchar(max)** 、**nvarchar(max)** 、および **varbinary(max)** データ型を使用してください。|データ型: **text**、 **ntext** 、または **image**|4|  
|データベースの管理|sp_attach_db<br /><br /> sp_attach_single_file_db|CREATE DATABASE ステートメントで FOR ATTACH オプションを使用します。 複数のログ ファイルを再構築するときに、これらのログ ファイル 1 つ以上に対して新しい場所を指定する場合は、FOR ATTACH_REBUILD_LOG を使用します。|sp_attach_db<br /><br /> sp_attach_single_file_db|81<br /><br /> 82|  
|データベース オブジェクト|CREATE DEFAULT<br /><br /> DROP DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|CREATE TABLE および ALTER TABLE の DEFAULT キーワード|CREATE_DROP_DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|162<br /><br /> 64<br /><br /> 65|  
|データベース オブジェクト|CREATE RULE<br /><br /> DROP RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule|CREATE TABLE および ALTER TABLE の CHECK キーワード|CREATE_DROP_RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule|161<br /><br /> 66<br /><br /> 67|  
|データベース オブジェクト|sp_change_users_login|ALTER USER を使用してください。|sp_change_users_login|231|  
|データベース オブジェクト|sp_depends|sys.dm_sql_referencing_entities および sys.dm_sql_referenced_entities|sp_depends|19|  
|データベース オブジェクト|sp_renamedb|ALTER DATABASE の MODIFY NAME|sp_renamedb|79|  
|データベース オブジェクト|sp_getbindtoken|MARS または分散トランザクションを使用してください。|sp_getbindtoken|98|  
|データベース オプション|sp_bindsession|MARS または分散トランザクションを使用してください。|sp_bindsession|97|  
|データベース オプション|sp_resetstatus|ALTER DATABASE SET { ONLINE &#124; EMERGENCY }|sp_resetstatus|83|  
|データベース オプション|ALTER DATABASE の TORN_PAGE_DETECTION オプション|ALTER DATABASE の PAGE_VERIFY TORN_PAGE_DETECTION オプション|ALTER DATABASE WITH TORN_PAGE_DETECTION|102|  
|DBCC|DBCC DBREINDEX|ALTER INDEX の REBUILD オプション|DBCC DBREINDEX|11|  
|DBCC|DBCC INDEXDEFRAG|ALTER INDEX の REORGANIZE オプション|DBCC INDEXDEFRAG|18|  
|DBCC|DBCC SHOWCONTIG|sys.dm_db_index_physical_stats|DBCC SHOWCONTIG|10|  
|DBCC|DBCC PINTABLE<br /><br /> DBCC UNPINTABLE|機能しません。|DBCC [UN]PINTABLE|189|  
|拡張プロパティ|拡張プロパティをレベル 1 型またはレベル 2 型のオブジェクトに追加するための、Level0type = 'type' および Level0type = 'USER' の使用|Level0type = 'USER' は、拡張プロパティをユーザーまたはロールに直接追加する場合のみ使用します。<br /><br /> Level0type = 'SCHEMA' を使用して、拡張プロパティを TABLE や VIEW のようなレベル 1 型に、または COLUMN や TRIGGER のようなレベル 2 型に追加します。 詳細については、「[sp_addextendedproperty &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)」を参照してください。|EXTPROP_LEVEL0TYPE<br /><br /> EXTPROP_LEVEL0USER|13<br /><br /> 14|  
|拡張ストアド プロシージャのプログラミング|srv_alloc<br /><br /> srv_convert<br /><br /> srv_describe<br /><br /> srv_getbindtoken<br /><br /> srv_got_attention<br /><br /> srv_message_handler<br /><br /> srv_paramdata<br /><br /> srv_paraminfo<br /><br /> srv_paramlen<br /><br /> srv_parammaxlen<br /><br /> srv_paramname<br /><br /> srv_paramnumber<br /><br /> srv_paramset<br /><br /> srv_paramsetoutput<br /><br /> srv_paramstatus<br /><br /> srv_paramtype<br /><br /> srv_pfield<br /><br /> srv_pfieldex<br /><br /> srv_rpcdb<br /><br /> srv_rpcname<br /><br /> srv_rpcnumber<br /><br /> srv_rpcoptions<br /><br /> srv_rpcowner<br /><br /> srv_rpcparams<br /><br /> srv_senddone<br /><br /> srv_sendmsg<br /><br /> srv_sendrow<br /><br /> srv_setcoldata<br /><br /> srv_setcollen<br /><br /> srv_setutype<br /><br /> srv_willconvert<br /><br /> srv_wsendmsg|代わりに CLR Integration を使用してください。|XP_API|20|  
|拡張ストアド プロシージャのプログラミング|sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc|代わりに CLR Integration を使用してください。|sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc|94<br /><br /> 95<br /><br /> 96|  
|拡張ストアド プロシージャ|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|CREATE LOGIN を使用してください。<br /><br /> SERVERPROPERTY の DROP LOGIN IsIntegratedSecurityOnly 引数を使用してください。|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginconfig|44<br /><br /> 45<br /><br /> 59|  
|関数|fn_get_sql|sys.dm_exec_sql_text|fn_get_sql|151|  
|高可用性|データベース ミラーリング (database mirroring)|[!INCLUDE[ssHADR](../includes/sshadr-md.md)]<br /><br /> 使用しているエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で [!INCLUDE[ssHADR](../includes/sshadr-md.md)]がサポートされていない場合は、ログ配布を使用してください。|DATABASE_MIRRORING|267|  
|インデックス オプション|sp_indexoption|ALTER INDEX|sp_indexoption|78|  
|インデックス オプション|オプションがかっこで囲まれていない CREATE TABLE、ALTER TABLE、または CREATE INDEX 構文|現在の構文を使用してステートメントを書き直してください。|INDEX_OPTION|33|  
|インスタンスのオプション|sp_configure の 'allow updates' オプション|システム テーブルは更新できなくなりました。 設定しても何の影響もありません。|sp_configure 'allow updates'|173|  
|インスタンスのオプション|sp_configure オプション:<br /><br /> 'locks'<br /><br /> 'open objects'<br /><br /> 'set working set size'|自動的に構成されるようになりました。 設定しても何の影響もありません。|sp_configure 'locks'<br /><br /> sp_configure 'open objects'<br /><br /> sp_configure 'set working set size'|174<br /><br /> 175<br /><br /> 176|  
|インスタンスのオプション|sp_configure の 'priority boost' オプション|システム テーブルは更新できなくなりました。 設定しても何の影響もありません。 代わりに、Windows start /high ... program.exe オプションを使用してください。|sp_configure 'priority boost'|199|  
|インスタンスのオプション|sp_configure の 'remote proc trans' オプション|システム テーブルは更新できなくなりました。 設定しても何の影響もありません。|sp_configure 'remote proc trans'|37|  
|リンク サーバー|リンク サーバーの SQLOLEDB プロバイダーの指定|SQL Server Native Client (SQLNCLI)|SQLOLEDDB for linked servers|19|  
|ロック|sp_lock|sys.dm_tran_locks|sp_lock|99|  
|メタデータ|FILE_ID<br /><br /> INDEXKEY_PROPERTY|FILE_IDEX<br /><br /> sys.index_columns|FILE_ID<br /><br /> INDEXKEY_PROPERTY|15<br /><br /> 17|  
|ネイティブ XML Web サービス|FOR SOAP オプションを指定した CREATE ENDPOINT または ALTER ENDPOINT ステートメント<br /><br /> sys.endpoint_webmethods<br /><br /> sys.soap_endpoints|代わりに Windows Communications Foundation (WCF) または ASP.NET を使用してください。|CREATE/ALTER ENDPOINT<br /><br /> sys.endpoint_webmethods<br /><br /> EXT_soap_endpoints<br /><br /> sys.soap_endpoints|21<br /><br /> 22<br /><br /> 23|  
|リムーバブル データベース|sp_certify_removable<br /><br /> sp_create_removable|sp_detach_db|sp_certify_removable<br /><br /> sp_create_removable|74<br /><br /> 75|  
|リムーバブル データベース|sp_dbremove|DROP DATABASE|sp_dbremove|76|  
|Security|ALTER LOGIN WITH SET CREDENTIAL 構文|新しい ALTER LOGIN ADD および DROP CREDENTIAL 構文に置き換えられます。|ALTER LOGIN WITH SET CREDENTIAL|230|  
|Security|sp_addapprole<br /><br /> sp_dropapprole|CREATE APPLICATION ROLE<br /><br /> DROP APPLICATION ROLE|sp_addapprole<br /><br /> sp_dropapprole|53<br /><br /> 54|  
|Security|sp_addlogin<br /><br /> sp_droplogin|CREATE LOGIN<br /><br /> DROP LOGIN|sp_addlogin<br /><br /> sp_droplogin|39<br /><br /> 40|  
|Security|sp_adduser<br /><br /> sp_dropuser|CREATE USER<br /><br /> DROP USER|sp_adduser<br /><br /> sp_dropuser|49<br /><br /> 50|  
|Security|sp_grantdbaccess<br /><br /> sp_revokedbaccess|CREATE USER<br /><br /> DROP USER|sp_grantdbaccess<br /><br /> sp_revokedbaccess|51<br /><br /> 52|  
|Security|sp_addrole<br /><br /> sp_droprole|CREATE ROLE<br /><br /> DROP ROLE|sp_addrole<br /><br /> sp_droprole|56<br /><br /> 57|  
|Security|sp_approlepassword<br /><br /> sp_password|ALTER APPLICATION ROLE<br /><br /> ALTER LOGIN|sp_approlepassword<br /><br /> sp_password|55<br /><br /> 46|  
|Security|sp_changeobjectowner|ALTER SCHEMA または ALTER AUTHORIZATION|sp_changeobjectowner|58|  
|Security|sp_control_dbmasterkey_password|マスター キーが存在し、パスワードが正しくなければなりません。|sp_control_dbmasterkey_password|274|  
|Security|sp_defaultdb<br /><br /> sp_defaultlanguage|ALTER LOGIN|sp_defaultdb<br /><br /> sp_defaultlanguage|47<br /><br /> 48|  
|Security|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|ALTER LOGIN DISABLE<br /><br /> CREATE LOGIN<br /><br /> DROP LOGIN|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|42<br /><br /> 41<br /><br /> 43|  
|Security|USER_ID|DATABASE_PRINCIPAL_ID|USER_ID|16|  
|Security|sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|これらのストアド プロシージャは、 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]で正しかった情報を返します。 出力には、 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]に実装された権限階層への変更が反映されません。 詳細については、「 [固定サーバー ロールの権限](https://msdn.microsoft.com/library/ms175892\(SQL.100\).aspx)」を参照してください。|sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|61<br /><br /> 60|  
|Security|GRANT ALL<br /><br /> DENY ALL<br /><br /> REVOKE ALL|特定の権限に対する GRANT、DENY、および REVOKE を使用してください。|ALL 権限|35|  
|Security|PERMISSIONS 組み込み関数|代わりに sys.fn_my_permissions をクエリしてください。|PERMISSIONS|170|  
|Security|SETUSER|EXECUTE AS|SETUSER|165|  
|Security|RC4 および DESX 暗号化アルゴリズム|AES など、別のアルゴリズムを使用してください。|DESX アルゴリズム|238|  
|SET オプション|SET FMTONLY|[sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)、[sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)、[sp_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)、[sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)。|SET FMTONLY|250|  
|サーバー構成オプション|c2 audit オプション<br /><br /> default trace enabled オプション|[common criteria compliance enabled サーバー構成オプション](../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)<br /><br /> [拡張イベント](../relational-databases/extended-events/extended-events.md)|sp_configure 'c2 audit mode'<br /><br /> sp_configure 'default trace enabled'|252<br /><br /> 253|  
|SMO クラス|**Microsoft.SQLServer.Management.Smo.Information** クラス<br /><br /> **Microsoft.SQLServer.Management.Smo.Settings** クラス<br /><br /> **Microsoft.SQLServer.Management.Smo.DatabaseOptions** クラス<br /><br /> **Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger.NotForReplication** プロパティ|**Microsoft.SqlServer.Management.Smo.Server** クラス<br /><br /> **Microsoft.SqlServer.Management.Smo.Server** クラス<br /><br /> **Microsoft.SqlServer.Management.Smo.Database** クラス<br /><br /> なし|なし|なし|  
|SQL Server エージェント|**net send** による通知<br /><br /> ポケットベルによる通知|メール通知<br /><br /> メール通知 |なし|なし|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でのソリューション エクスプローラーの統合||なし|なし|  
|システム ストアド プロシージャ|sp_db_increased_partitions|[なし] : [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]では、増加したパーティションのサポートを既定で使用できます。|sp_db_increased_partitions|253|  
|システム テーブル|sysaltfiles<br /><br /> syscacheobjects<br /><br /> syscolumns<br /><br /> syscomments<br /><br /> sysconfigures<br /><br /> sysconstraints<br /><br /> syscurconfigs<br /><br /> sysdatabases<br /><br /> sysdepends<br /><br /> sysdevices<br /><br /> sysfilegroups<br /><br /> sysfiles<br /><br /> sysforeignkeys<br /><br /> sysfulltextcatalogs<br /><br /> sysindexes<br /><br /> sysindexkeys<br /><br /> syslockinfo<br /><br /> syslogins<br /><br /> sysmembers<br /><br /> sysmessages<br /><br /> sysobjects<br /><br /> sysoledbusers<br /><br /> sysopentapes<br /><br /> sysperfinfo<br /><br /> syspermissions<br /><br /> sysprocesses<br /><br /> sysprotects<br /><br /> sysreferences<br /><br /> sysremotelogins<br /><br /> sysservers<br /><br /> systypes<br /><br /> sysusers|互換性ビュー。 詳細については、「[互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)」を参照してください。<br /><br /> **重要:** 互換性ビューには、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] で導入された機能のメタデータは表示されません。 カタログ ビューを使用するようにアプリケーションをアップグレードすることをお勧めします。 詳細については、「[カタログ ビュー &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)」を参照してください。|sysaltfiles<br /><br /> syscacheobjects<br /><br /> syscolumns<br /><br /> syscomments<br /><br /> sysconfigures<br /><br /> sysconstraints<br /><br /> syscurconfigs<br /><br /> sysdatabases<br /><br /> sysdepends<br /><br /> sysdevices<br /><br /> sysfilegroups<br /><br /> sysfiles<br /><br /> sysforeignkeys<br /><br /> sysfulltextcatalogs<br /><br /> sysindexes<br /><br /> sysindexkeys<br /><br /> syslockinfo<br /><br /> syslogins<br /><br /> sysmembers<br /><br /> sysmessages<br /><br /> sysobjects<br /><br /> sysoledbusers<br /><br /> sysopentapes<br /><br /> sysperfinfo<br /><br /> syspermissions<br /><br /> sysprocesses<br /><br /> sysprotects<br /><br /> sysreferences<br /><br /> sysremotelogins<br /><br /> sysservers<br /><br /> systypes<br /><br /> sysusers|141<br /><br /> なし<br /><br /> 133<br /><br /> 126<br /><br /> 146<br /><br /> 131<br /><br /> 147<br /><br /> 142<br /><br /> 123<br /><br /> 144<br /><br /> 128<br /><br /> 127<br /><br /> 130<br /><br /> 122<br /><br /> 132<br /><br /> 134<br /><br /> 143<br /><br /> 140<br /><br /> 119<br /><br /> 137<br /><br /> 125<br /><br /> 139<br /><br /> 145<br /><br /> 157<br /><br /> 121<br /><br /> 153<br /><br /> 120<br /><br /> 129<br /><br /> 138<br /><br /> 136<br /><br /> 135<br /><br /> 124|  
|システム テーブル|sys.numbered_procedures<br /><br /> sys.numbered_procedure_parameters|なし|numbered_procedures<br /><br /> numbered_procedure_parameters|148<br /><br /> 149|  
|システム関数|fn_virtualservernodes<br /><br /> fn_servershareddrives|sys.dm_os_cluster_nodes<br /><br /> sys.dm_io_cluster_shared_drives|fn_virtualservernodes<br /><br /> fn_servershareddrives|155<br /><br /> 156|  
|システム ビュー|sys.sql_dependencies|sys.sql_expression_dependencies|sys.sql_dependencies|198|  
|テーブル圧縮|vardecimal ストレージ形式の使用|Vardecimal ストレージ形式は非推奨とされます。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のデータ圧縮では、decimal 型の値も他のデータ型と同様に圧縮されます。 vardecimal ストレージ形式ではなくデータ圧縮を使用することをお勧めします。|vardecimal ストレージ形式|200|  
|テーブル圧縮|sp_db_vardecimal_storage_format プロシージャの使用|Vardecimal ストレージ形式は非推奨とされます。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のデータ圧縮では、decimal 型の値も他のデータ型と同様に圧縮されます。 vardecimal ストレージ形式ではなくデータ圧縮を使用することをお勧めします。|sp_db_vardecimal_storage_format|201|  
|テーブル圧縮|sp_estimated_rowsize_reduction_for_vardecimal プロシージャの使用|代わりにデータ圧縮と sp_estimate_data_compression_savings プロシージャを使用してください。|sp_estimated_rowsize_reduction_for_vardecimal|202|  
|テーブル ヒント|UPDATE または DELETE ステートメントの FROM 句での NOLOCK または READUNCOMMITTED の指定|FROM 句から NOLOCK または READUNCOMMITTED のテーブル ヒントを削除します。|NOLOCK or READUNCOMMITTED in UPDATE or DELETE|1|  
|テーブル ヒント|WITH キーワードを使用しないテーブル ヒントの指定|WITH を使用します。|Table hint without WITH|8|  
|テーブル ヒント|INSERT_HINTS||INSERT_HINTS|34|  
|テキスト ポインター|WRITETEXT<br /><br /> UPDATETEXT<br /><br /> READTEXT|なし|UPDATETEXT または WRITETEXT<br /><br /> READTEXT|115<br /><br /> 114|  
|テキスト ポインター|TEXTPTR()<br /><br /> TEXTVALID()|なし|TEXTPTR<br /><br /> TEXTVALID|5<br /><br /> 6|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|:: 関数呼び出しの手順|SELECT *column_list* FROM sys.\<*function_name*>() で置き換えられました。<br /><br /> たとえば、`SELECT * FROM ::fn_virtualfilestats(2,1)` は `SELECT * FROM sys.fn_virtualfilestats(2,1)` に置き換わります。|'::' 関数呼び出し構文|166|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|3 つおよび 4 つの部分で構成された列参照|2 つの部分で構成される名前が標準に準拠した動作です。|3 つ以上の部分で構成される列名|3|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|SELECT リストの式に対して、列の別名として使用される、引用符で囲まれた文字列:<br /><br /> '*string_alias*' = *expression*|*expression* [AS] *column_alias*<br /><br /> *expression* [AS] [*column_alias*]<br /><br /> *expression* [AS] "*column_alias*"<br /><br /> *expression* [AS] '*column_alias*'<br /><br /> *column_alias* = *expression*|列の別名としての文字列リテラル|184|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|番号付きプロシージャ|[なし] : 使用しないでください。|ProcNums|160|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|DROP INDEX での*table_name.index_name* 構文|DROP INDEX での*index_name* ON *table_name* 構文です。|2 部構成の名前が使用された DROP INDEX|163|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|セミコロンで終了しない [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント|[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントをセミコロンで (;) で終了してください。|なし|なし|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|GROUP BY ALL|状況に応じて UNION または派生テーブルを使用したカスタム ソリューションを使用してください。|GROUP BY ALL|169|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|DML ステートメントでの列名としての ROWGUIDCOL の使用|$rowguid を使用してください。|ROWGUIDCOL|182|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|DML ステートメントでの列名としての IDENTITYCOL の使用|$identity を使用してください。|IDENTITYCOL|183|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|一時テーブル名および一時ストアド プロシージャ名としての #、## の使用|別の文字を少なくとも 1 文字は使用してください。|'#' および ' ##' 一時テーブルおよびストアド プロシージャの名前として|185|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|[!INCLUDE[tsql](../includes/tsql-md.md)] 識別子としての \@、\@\@、または \@\@ で始まる名前の使用。|\@、\@\@、または \@\@ で始まる名前を識別子として使用しないでください。|[!INCLUDE[tsql](../includes/tsql-md.md)] 識別子としての '\@' と '\@\@' で始まる名前|186.|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|既定値としての DEFAULT キーワードの使用|DEFAULT キーワードを既定値として使用しないでください。|既定値としての DEFAULT キーワード|187|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|テーブル ヒントの区切り文字としてのスペースの使用|テーブル ヒントはコンマを使用して区切ってください。|コンマで区切られていない複数のテーブル ヒント|168|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|集計インデックス付きビューの選択リストには、互換性モードが 90 の場合、COUNT_BIG (\*) の指定が必要|COUNT_BIG (\*) を使用してください。|COUNT_BIG(\*) がないインデックス付きビューの選択リスト|2|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|ビュー経由で複数ステートメントのテーブル値関数 (TVF) を呼び出す、テーブル ヒントの間接アプリケーション|[なし] :|間接的な TVF ヒント|7|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|ALTER DATABASE 構文:<br /><br /> MODIFY FILEGROUP READONLY<br /><br /> MODIFY FILEGROUP READWRITE|MODIFY FILEGROUP READ_ONLY<br /><br /> MODIFY FILEGROUP READ_WRITE|MODIFY FILEGROUP READONLY<br /><br /> MODIFY FILEGROUP READWRITE|195<br /><br /> 196|  
|その他|DB-Library<br /><br /> Embedded SQL for C|[!INCLUDE[ssDE](../includes/ssde-md.md)] では、DB-Library および Embedded SQL API を使用した既存アプリケーションからの接続が引き続きサポートされますが、これらの API を使用するアプリケーションでのプログラミング作業に必要なファイルやドキュメントは含まれません。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] の今後のバージョンでは、DB-Library アプリケーションや Embedded SQL アプリケーションからの接続はサポートされなくなります。 新しいアプリケーションの開発には DB-Library や Embedded SQL を使用しないでください。 DB-Library や Embedded SQL への依存関係は、既存アプリケーションを変更するときに削除してください。 これらの API の代わりに、SQLClient 名前空間または ODBC などの API を使用します。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] には、これらのアプリケーションの実行に必要な DB-Library DLL が含まれていません。 DB-Library アプリケーションまたは Embedded SQL アプリケーションを実行するには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Version 6.5、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 7.0、または [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]から DB-Library DLL を入手する必要があります。|なし|なし|  
|ツール|SQL Server Profiler for Trace Capture|SQL Server Management Studio に組み込まれている Extended Events Profiler を使用します。|SQL Server プロファイラー|なし|  
|ツール|SQL Server Profiler for Trace Replay|[SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)|SQL Server プロファイラー|なし|  
|トレース管理オブジェクト|Microsoft.SqlServer.Management.Trace namespace (SQL Server の Trace および Replay オブジェクト用の API が含まれています)|トレース構成: <xref:Microsoft.SqlServer.Management.XEvent><br /><br /> トレース読み取り: <xref:Microsoft.SqlServer.XEvent.Linq><br /><br /> トレース再生:なし|||  
|SQL トレースのストアド プロシージャ、関数、およびカタログ ビュー|sp_trace_create<br /><br /> sp_trace_setevent<br /><br /> sp_trace_setfilter<br /><br /> sp_trace_setstatus<br /><br /> fn_trace_geteventinfo<br /><br /> fn_trace_getfilterinfo<br /><br /> fn_trace_getinfo<br /><br /> fn_trace_gettable<br /><br /> sys.traces<br /><br /> sys.trace_events<br /><br /> sys.trace_event_bindings<br /><br /> sys.trace_categories<br /><br /> sys.trace_columns<br /><br /> sys.trace_subclass_values|[拡張イベント](../relational-databases/extended-events/extended-events.md)|sp_trace_create<br /><br /> sp_trace_setevent<br /><br /> sp_trace_setfilter<br /><br /> sp_trace_setstatus<br /><br /> fn_trace_geteventinfo<br /><br /> fn_trace_getfilterinfo<br /><br /> fn_trace_getinfo<br /><br /> fn_trace_gettable<br /><br /> sys.traces<br /><br /> sys.trace_events<br /><br /> sys.trace_event_bindings<br /><br /> sys.trace_categories<br /><br /> sys.trace_columns<br /><br /> sys.trace_subclass_values|258<br /><br /> 260<br /><br /> 261<br /><br /> 259<br /><br /> 256<br /><br /> 257|  
  
> [!NOTE]  
> **sp_setapprole** のクッキーの **OUTPUT** パラメーターは現在、適切な最大長である **varbinary(8000)** としてドキュメントに記載されています。 ただし、現在の実装では **varbinary(50)** を返します。 開発者が **varbinary(50)** を割り当てると、今後のリリースでクッキーの戻り値のサイズが増えた場合にアプリケーションの変更が必要になる可能性があります。 これは廃止の問題ではありませんが、アプリケーションの調整と似ているため、このトピックで説明されています。 詳細については、「[sp_setapprole &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 で廃止されたデータベース エンジンの機能](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)  
  

