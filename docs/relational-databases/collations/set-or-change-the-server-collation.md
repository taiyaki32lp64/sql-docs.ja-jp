---
title: サーバーの照合順序の設定または変更 | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: carlrab
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 019c62424398b05dfaa6efe2f91ab4c08b333cd2
ms.sourcegitcommit: 0d34b654f0b3031041959e87f5b4d4f0a1af6a29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74901914"
---
# <a name="set-or-change-the-server-collation"></a>サーバーの照合順序の設定または変更

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  サーバー照合順序は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスと一緒にインストールされているすべてのシステム データベースだけではなく、新しく作成したユーザー データベースの既定の照合順序になります。 サーバーレベルの照合順序は慎重に選択してください。以下に影響を与えます。
 - `=`、`JOIN`、`ORDER BY`、ならびにテキスト データを比較するその他の演算子の並べ替えルールと比較ルール。
 - システム ビュー、システム関数、TempDB のオブジェクト (一時テーブルなど) の `CHAR`、`VARCHAR`、`NCHAR`、`NVARCHAR` 列の照合順序。
 - 変数、カーソル、`GOTO` ラベルの名前。 変数の @pi と @PI は、サーバーレベルの照合順序で大文字と小文字が区別される場合は異なる変数であると、区別されない場合は同じ変数であると見なされます。
  
## <a name="setting-the-server-collation-in-sql-server"></a>SQL Server でサーバー照合順序を設定する

  サーバー照合順序は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時に指定します。 サーバーレベルの既定の照合順序は **SQL_Latin1_General_CP1_CI_AS** です。 Unicode 専用の照合順序はサーバーレベルの照合順序として指定できません。 詳細については、「 [Collation and Unicode Support](collation-and-unicode-support.md)」を参照してください。
  
## <a name="changing-the-server-collation-in-sql-server"></a>SQL Server でサーバー照合順序を変更する

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの既定の照合順序を変更する操作は複雑で、次の手順が含まれます。  
  
- ユーザー データベースおよびユーザー データベース内のすべてのオブジェクトを再作成するのに必要なすべての情報またはスクリプトがあることを確認します。  
  
- [bcp ユーティリティ](../../tools/bcp-utility.md)などのツールを使用して、すべてのデータをエクスポートします。 詳細については、「[データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)」を参照してください。  
  
- すべてのユーザー データベースを削除します。  
  
- **setup** コマンドの SQLCOLLATION プロパティで新しい照合順序を指定して、master データベースを再構築します。 次に例を示します。  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]
    /SQLCOLLATION=CollationName  
    ```  
  
     詳細については、「 [システム データベースの再構築](../../relational-databases/databases/rebuild-system-databases.md)」を参照してください。  
  
- すべてのデータベースとデータベース内のすべてのオブジェクトを作成します。  
  
- すべてのデータをインポートします。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの既定の照合順序を変更する代わりに、新しく作成するデータベースごとに既定の照合順序を指定することができます。  
  
## <a name="setting-the-server-collation-in-managed-instance"></a>Managed Instance でサーバー照合順序を設定する
Azure SQL Managed Instance のサーバーレベルの照合順序は、インスタンスの作成時に指定できますが、後で変更することはできません。 インスタンスを作成しているときに、[Azure Portal](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started#create-a-managed-instance) または [PowerShell と Resource Manager テンプレート](https://docs.microsoft.com/azure/sql-database/scripts/sql-managed-instance-create-powershell-azure-resource-manager-template)を使用してサーバーレベルの照合順序を設定できます。 サーバーレベルの既定の照合順序は **SQL_Latin1_General_CP1_CI_AS** です。 Unicode 専用の照合順序と新しい UTF-8 の照合順序はサーバーレベルの照合順序として指定できません。
SQL Server から Managed Instance にデータベースを移行する場合、`SERVERPROPERTY(N'Collation')` 関数を使用してソース SQL Server でサーバー照合順序を確認し、ご利用の SQL Server の照合順序に一致する Managed Instance を作成します。 一致しないサーバーレベル照合順序で SQL Server から Managed Instance にデータベースを移行すると、クエリで予想外のエラーがいくつか発生することがあります。 既存の Managed Instance のサーバー レベル照合順序を変更することはできません。

## <a name="see-also"></a>参照

 [照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)   
 [データベースの照合順序の設定または変更](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [列の照合順序の設定または変更](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [システム データベースの再構築](../../relational-databases/databases/rebuild-system-databases.md)  
 
