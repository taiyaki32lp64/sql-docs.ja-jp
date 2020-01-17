---
title: アドレス帳の SQL スクリプトを実行している |。Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5adc631a3c3f7a66c02f9ebfe541fa5e923deb0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922237"
---
# <a name="running-the-address-book-sql-script"></a>アドレス帳の SQL スクリプトの実行
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 ISQL/クエリ アナライザーのコマンド ライン ユーティリティまたは SQL Server の Enterprise Manager を使用する必要があります (Sampleemp.sql) 付属の SQL スクリプトを実行します。  
  
-   既定のデバイスに AddrBookDB、新しいデータベースを作成します。  
  
-   AddrBookDB、データベースに接続します。  
  
-   Employee テーブルを作成します。  
  
-   テーブルにサンプル データを設定します。  
  
-   データベース テーブルの作成を確認する単純な SELECT ステートメントを実行します。  
  
-   "Adcdemo"パスワード"adcdemo"と呼ばれるユーザー アカウントを設定します。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5 で Sampleemp.sql スクリプトを実行するには  
  
1.  クリックして**開始**、 をポイント**プログラム**、順にポイント**Microsoft SQL Server 6.5**します。 クリックして**SQL Enterprise Manager**します。  
  
2.  **ツール** メニューのをクリックして**SQL クエリ ツール**します。  
  
3.  クリックして**SQL スクリプトの読み込み**c:\Platform SDK\Samples\DataAccess\RDS\AddressBook を参照します。  
  
4.  Sampleemp.sql ファイルを選択します。 **[開く]** をクリックします。  
  
5.  をクリックして、**クエリの実行**(ツールバーの緑色の矢印) ボタンをクリックします。  
  
6.  を実行すると、閉じる、**クエリ**と**Enterprise Manager** windows。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0 で Sampleemp.sql スクリプトを実行するには  
  
1.  クリックして**開始**、 をポイント**プログラム**、順にポイント**Microsoft SQL Server 7.0**します。 クリックして**Enterprise Manager**します。  
  
2.  Enterprise Manager で登録済みサーバーの一覧から使用する SQL Server が選択されていることを確認します。  
  
3.  **ツール** メニューのをクリックして**SQL Server クエリ アナライザー**します。  
  
4.  をクリックして、 **SQL スクリプトの読み込み**c:\Platform SDK\Samples\DataAccess\RDS\AddressBook を参照し、ボタン (ツールバーの開いているフォルダー)。  
  
5.  Sampleemp.sql ファイルを選択します。 **[開く]** をクリックします。  
  
6.  をクリックして、**クエリの実行**ボタン (ツールバーの緑色の矢印) または**F5**します。  
  
7.  を実行すると、閉じる、**クエリ**、**クエリ アナライザー**、および**Enterprise Manager** windows。  
  
## <a name="see-also"></a>関連項目  
 [アドレス帳のサンプル アプリケーションの実行](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


