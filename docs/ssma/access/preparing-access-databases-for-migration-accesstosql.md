---
title: 移行 (AccessToSQL) を Access データベースを準備する |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 58988d31687cacdce2954d8e4098d509a9dcbb2b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260218"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>移行 (AccessToSQL) を Access データベースを準備します。
Access データベースを移行する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、移行し、これらのデータベースが移行の準備ができていることを確認するデータベースを決定する必要があります。  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>SQL Server に移行する場合を判断します。  
アクセスするため、データベース エンジンとして使用される、Jet データベース エンジンとは、データ管理のための柔軟で使いやすいソリューションです。 ただし、データベースのサイズが大きくなる複数のミッション クリティカルとして多くのユーザーを検索パフォーマンスの向上、セキュリティ、または可用性が必要です。 堅牢なデータ プラットフォームを必要とするアプリケーションでは、それらのアプリケーションの基になるデータベースの移動を検討してください[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 移行するタイミングを決定する方法の詳細については、次を参照してください。、[移行情報ページ](https://go.microsoft.com/fwlink/?LinkId=68571)上、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Web サイト。  
  
データベースを移行した後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]リンク テーブルを使用して、アクセスを使用を継続できますしたりするようにアプリケーションを手動で移行することができます[!INCLUDE[msCoName](../../includes/msconame_md.md)]と直接やり取りするコードを .NET Framework に基づく[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
## <a name="determining-which-databases-to-migrate"></a>移行対象のデータベースを決定します。  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) のアクセスは、の Access データベースを検索できます。 そのデータベースに関するメタデータをエクスポートできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 エクスポートのメタデータを照会する方法の詳細については、次を参照してください。 [Access インベントリのエクスポート](exporting-an-access-inventory-accesstosql.md)します。  

   > [!NOTE]
   > 、でサポートされていないすべてのアクセス機能と設定、または、簡単に変換できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 データベースの移行を開始する前に、次を参照してください。[互換性のないアクセス機能](incompatible-access-features-accesstosql.md)します。
  
## <a name="preparing-for-migration"></a>移行の準備  
移行を Access データベースを準備できるように、次のガイドラインを使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
### <a name="upgrading-older-access-databases"></a>以前の Access データベースをアップグレードします。  
アクセス用の SSMA は、Access 97 以降のバージョンをサポートします。 以前のバージョンの Access データベースがある場合は、開くし、Access 97 以降のバージョンでデータベースを保存します。  
  
### <a name="removing-workgroup-protection"></a>ワークグループの保護の削除  
SSMA は、ワークグループの保護を使用するデータベースを移行できません。 ワークグループの保護を Access データベースから削除するには、次の手順を実行します。  
  
1.  Access データベース ファイルを別の場所にコピーします。  
  
2.  データベースのコピーを開きます。  
  
3.  **ツール**メニューで、**セキュリティ**、し、**ユーザーとグループ権限**します。  
  
4.  選択、**ユーザー**オプションを選択し、**管理者**ユーザー、ことを確認、 **Administer**アクセス許可が選択されています。  
  
5.  選択、**グループ**オプションを選択し、**ユーザー**グループ化、およびことを確認します、**管理**アクセス許可を選択します。  
  
6.  をクリックして**OK**、し、**ファイル** メニューのをクリックして**終了**します。  
  
SSMA を使用して、データベースのコピーを移行することができますようになりました。 スキーマの読み込み後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、手動でのデータベースを保護することができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
### <a name="backing-up-databases"></a>データベースのバックアップ  
データベースのアクセスを移行する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、移行する場合は両方、Access データベースをバックアップする必要がありますだけでなく[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は移行先のデータベース オブジェクトとデータにアクセスします。  
  
Access データベースをバックアップする、**ツール**メニューで、**データベース ユーティリティ**、し、**データベースのバックアップ**します。  
  
バックアップを作成する方法については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースを参照してください"でデータベースを復元するバックアップと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
### <a name="documenting-databases"></a>データベースを文書化  
データベース オブジェクト、ファイル サイズ、および Access データベースのアクセス許可の一覧など、プロパティを文書化することも可能性があります。 Access では、このドキュメントを生成する、**ツール**メニューで、**分析**、 をクリックし、 **Documented**します。  
  
## <a name="see-also"></a>関連項目  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[SQL Server への Access アプリケーションのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
