---
title: SQL Server スキーマ (MySQLToSQL) への MySQL データベースのマッピング |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 215833c96fae02ae7877e00173fb5a920a47ee0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908986"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>MySQL データベースの SQL Server スキーマへのマッピング (MySQLToSQL)
既定では、SSMA for MySQL に移行する MySQL スキーマのすべてのオブジェクトを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベースのスキーマの名前します。 ただし、MySQL スキーマ間のマッピングをカスタマイズすることができますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベース。  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL と SQL Server または SQL Azure のスキーマ  
スキーマの MySQL の概念は、データベースとそのスキーマのいずれかの SQL Server の概念にマップされます。 SSMA はスキーマとしてデータベースとスキーマの SQL Server の組み合わせを表します。  
  
スキーマの MySQL の概念は、データベースとそのスキーマのいずれかの SQL Server の概念にマップされます。 たとえば、MySQL のという名前のスキーマがある**HR**します。 という名前のデータベースを SQL Server のインスタンスである可能性があります**HR**、そのデータベースは、スキーマとします。 1 つのスキーマは、 **dbo** (またはデータベース所有者) スキーマ。 既定では、MySQL スキーマ**HR**にマップされます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースおよびスキーマ**HR.dbo**します。 SSMA を指す、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマとしてデータベースとスキーマの組み合わせ。  
  
MySQL の間のマッピングを変更して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure のスキーマ。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲット データベースおよびスキーマの変更  
SSMA では、使用可能な任意に MySQL スキーマをマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のスキーマ。  
  
**データベースとスキーマを変更するには**  
  
1.  MySQL メタデータ エクスプ ローラーで選択**スキーマ**します。  
  
    **スキーマ マッピング** タブは、個別のスキーマを選択したときにも使用可能な。 一覧で、**スキーマ マッピング** タブを選択したオブジェクトのカスタマイズします。  
  
2.  右側のウィンドウでをクリックして、**スキーマ マッピング**タブ。  
  
    対象の値を後に、すべての MySQL スキーマの一覧が表示されます。 このターゲットは、2 部構成の表記法で示されます (*database.schema*) で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure が、オブジェクトとデータを移行します。  
  
3.  変更、およびクリックするマッピングが含まれている行を選択**変更**します。  
  
    **ターゲット スキーマの選択**ダイアログ ボックスで、使用可能なターゲット データベース スキーマや型、データベースとスキーマの 2 部構成の表記 (database.schema) で、テキスト ボックスに名前をクリックを参照することがあります**OK**.  
  
4.  ターゲットの変更、**スキーマ マッピング**タブ。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソース データベースは、任意のターゲット データベースにマップできます。 既定では、ソース データベースがマップされているターゲットに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA を使用してを接続したデータベース。 マップされるターゲット データベースでは、非既存ではかどうか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、メッセージが表示されますが、 **"、データベースやスキーマがターゲットに存在しません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ。これが同期中に作成されます。続行することでしょうか。"** [はい] をクリックします。 同様に、ターゲットの存在しないスキーマをスキーマにマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同期中に作成されるデータベース。  
  
-   SQL Azure へのマッピング  
  
接続されているターゲットをソース データベースにマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースまたは接続されているターゲットのスキーマに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。 ソース スキーマ 接続されているターゲット データベースでは、存在しないスキーマをマップするかどうかは、メッセージが表示されるが **"スキーマが対象のメタデータには存在できません。これが同期中に作成されます。続行しますか?"** はい をクリックします。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>既定のデータベースとスキーマを元に戻す  
MySQL スキーマと SQL Server スキーマ間のマッピングをカスタマイズする場合は、既定値にマッピングを戻すことができます。  
  
**既定のデータベースとスキーマに戻すには**  
  
1.  スキーマ マッピング タブで、任意の行を選択し をクリックして**既定値にリセット**既定のデータベースとスキーマに戻す。  
  
## <a name="next-steps"></a>次の手順  
SQL Server または SQL Azure のオブジェクトへの MySQL のオブジェクトの変換を分析する場合は、[変換レポートを作成する](assessing-mysql-databases-for-conversion-mysqltosql.md)できますそれ以外の場合[MySQL データベースのオブジェクトの定義の変換](converting-mysql-databases-mysqltosql.md)SQL にサーバーまたは SQL Azure のスキーマ  
  
## <a name="see-also"></a>関連項目  
[プロジェクトの設定&#40;変換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Azure SQL DB に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[SQL Server に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
