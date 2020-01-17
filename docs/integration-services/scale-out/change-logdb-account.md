---
title: Scale Out ログのアカウントの変更 | Microsoft Docs
description: この記事では、SSIS Scale Out ログのユーザー アカウントを変更する方法について説明します
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 92cf3e13f1e386a77ba4621b817567af95b42884
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896982"
---
# <a name="change-the-account-for-scale-out-logging"></a>Scale Out ログのアカウントの変更

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Scale Out で SSIS パッケージを実行すると、イベント メッセージが、 **##MS_SSISLogDBWorkerAgentLogin##** という名前の自動作成ユーザー アカウントで SSISDB データベースにログ記録されます。 このユーザーのログインでは、SQL Server 認証が使用されます。

Scale Out ログ記録で使用されるアカウントを変更する場合は、以下の操作を行います。

> [!NOTE]
> ログ記録に Windows ユーザー アカウントを使用する場合は、Scale Out Worker サービスを実行するアカウントと同じアカウントを使用します。 それ以外の場合は、SQL Server にログインできません。

## <a name="1-create-a-user-for-ssisdb"></a>1.SSISDB のユーザーを作成する
データベース ユーザーの作成手順については、「[データベース ユーザーの作成](../../relational-databases/security/authentication-access/create-a-database-user.md)」を参照してください。

## <a name="2-add-the-user-to-the-database-role-ssisclusterworker"></a>2.データベース ロール ssis_cluster_worker にユーザーを追加する

データベース ロールの追加手順については、「[ロールの追加](../../relational-databases/security/authentication-access/join-a-role.md)」を参照してください。

## <a name="3-update-the-logging-information-in-ssisdb"></a>3.SSISDB のログイン情報を更新する
以下の例に示すように、パラメーターとして SQL Server 名と接続文字列を指定してストアド プロシージャ `[catalog].[update_logdb_info]` を呼び出します。

    ```sql
    SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
    SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
    EXEC [internal].[update_logdb_info] @serverName, @connectionString
    GO
    ```

## <a name="4-restart-the-scale-out-worker-service"></a>4.Scale Out Worker サービスを再起動する
Scale Out Worker サービスを再起動して、変更を有効にします。

## <a name="next-steps"></a>次の手順
-   [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md)
