---
title: Oracle (OracleToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 42ab1e77dbdb7cee237a9ec22c49a725a64390c0
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264480"
---
# <a name="connect-to-oracle-oracletosql"></a>Oracle への接続 (OracleToSQL)
使用して、 **Connect to Oracle**を移行する Oracle データベースに接続するためのダイアログ ボックス。  
  
このダイアログ ボックスにアクセスする、**ファイル**メニューの  **Oracle への接続**します。 以前接続した場合、コマンドは**Oracle への再接続**します。  
  
## <a name="options"></a>および  
**Provider**  
Oracle データベースへの接続のデータ アクセス プロバイダーを選択します。 利用可能なプロバイダーには、Oracle クライアント プロバイダーと OLE DB プロバイダーです。 既定では Oracle Client プロバイダーです。  
  
**モード**  
Standard、TNSNAME、または接続文字列のいずれかのモードを選択します。  
  
-   標準モードでは、入力またはプロバイダー、サーバー名、サーバーのポート、Oracle SID、ユーザー名、およびパスワードの値を選択します。  
  
-   TNSNAME モードでは、Oracle データベース、ユーザー名、およびパスワードの接続識別子 (TNS 別名) を入力します。  
  
-   接続文字列のモードでは、接続文字列を指定します。  
  
    > [!IMPORTANT]  
    > テキストは、パスワードを含めることができ、クリア テキストとして送信されるため、接続文字列モードを使用することはお勧めできません。  
  
既定では標準モードです。  
  
**サーバー名**  
Oracle サーバー名を入力します。 既定のサーバー名は、コンピューター名と同じです。 これは、標準モードのオプションです。  
  
**[サーバー ポート]**  
Oracle への接続を 1521 (既定値) 以外のポート番号を使用している場合は、ポート番号を入力します。 これは、標準モードのオプションです。  
  
**識別子を接続します。**  
Oracle の入力の識別子を接続します。 これは、ローカルの tnsnames.ora ファイルで定義されているデータベースのエイリアスです。  
  
これは、TNSNAME モード オプションです。  
  
**Oracle SID**  
データベースの SID を入力します。 SID は、コンピューター上の Oracle データベースを区別する識別子です。 データベースの既定の SID は、データベース名の最初の 8 文字です。  
  
これは、標準モードのオプションです。  
  
**ユーザー名**  
SSMA が Oracle データベースへの接続に使用するユーザー名を入力します。  
  
**Password**  
ユーザー名に対応するパスワードを入力します。  
  
**[接続文字列]**  
> [!IMPORTANT]  
> テキストは、パスワードを含めることができ、クリア テキストとして送信されるため、接続文字列モードを使用することはお勧めできません。  
  
接続文字列モードを使用する場合は、Oracle への接続の完全な接続文字列を入力します。  
  
接続文字列は、パラメーターの名前と値のペアで構成されます。  
  
-   OLE DB 接続文字列については、次を参照してください。 [Microsoft OLE DB Provider for Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) 、MSDN ライブラリの記事。  
  
SSMA 接続文字列の場合に、プロバイダーのパラメーターを常に含めます。 また、Oracle に接続するときに、ポート パラメーターを含めることを確認します。  
  
