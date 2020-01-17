---
title: SQL Server スキーマ (OracleToSQL) への Oracle スキーマのマッピング |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e375c07ceddc995b599930c14f00710af040d6c0
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262910"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>SQL Server スキーマへの Oracle スキーマのマッピング (OracleToSQL)
Oracle は、各データベースは、1 つまたは複数のスキーマを持っています。 SSMA は既定では、Oracle スキーマのすべてのオブジェクトを移行、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマという名前のデータベース。 ただし、Oracle スキーマ間のマッピングをカスタマイズすることができますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle および SQL Server スキーマ  
Oracle データベースには、スキーマが含まれています。 インスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]複数のスキーマがそれぞれの複数のデータベースが含まれています。  
  
マップ、スキーマの Oracle の概念、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースとそのスキーマのいずれかの概念です。 たとえば、Oracle のという名前のスキーマがある**HR**します。 インスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]という名前のデータベースがあります。 **HR**、そのデータベースは、スキーマとします。 1 つのスキーマは、 **dbo** (またはデータベース所有者) スキーマ。 既定では、Oracle スキーマ**HR**にマップされます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースおよびスキーマ**HR.dbo**します。 SSMA を指す、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマとしてデータベースとスキーマの組み合わせ。  
  
Oracle の間のマッピングを変更して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマ。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲット データベースおよびスキーマの変更  
SSMA では、使用可能な任意に、Oracle スキーマをマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマ。  
  
**データベースとスキーマを変更するには**  
  
1.  Oracle メタデータ エクスプ ローラーで選択**スキーマ**します。  
  
    **スキーマ マッピング** タブは、個々 のデータベースを選択した場合にも使用可能な**スキーマ**フォルダー、または個別のスキーマ。 一覧で、**スキーマ マッピング** タブを選択したオブジェクトのカスタマイズします。  
  
2.  右側のウィンドウでをクリックして、**スキーマ マッピング**タブ。  
  
    対象の値を後に、すべての Oracle スキーマの一覧が表示されます。 このターゲットは、2 部構成の表記法で示されます (*database.schema*) で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトとデータを移行します。  
  
3.  変更、およびクリックするマッピングが含まれている行を選択**変更**します。  
  
    **ターゲット スキーマの選択**ダイアログ ボックスで、使用可能なターゲット データベース スキーマや型、データベースとスキーマの 2 部構成の表記 (database.schema) で、テキスト ボックスに名前をクリックを参照することがあります**OK**.  
  
4.  ターゲットの変更、**スキーマ マッピング**タブ。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソース データベースは、任意のターゲット データベースにマップできます。 既定では、ソース データベースがマップされているターゲットに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA を使用してを接続したデータベース。 マップされるターゲット データベースでは、非既存ではかどうか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、メッセージが表示されますが、 **"、データベースやスキーマがターゲットに存在しません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ。これが同期中に作成されます。続行することでしょうか。"** [はい] をクリックします。 同様に、ターゲットの存在しないスキーマをスキーマにマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同期中に作成されるデータベース。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>既定のデータベースとスキーマを元に戻す  
Oracle スキーマ間のマッピングをカスタマイズする場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマでは、既定値にマッピングを戻すことができます。  
  
**既定のデータベースとスキーマに戻すには**  
  
1.  スキーマ マッピング タブで、任意の行を選択し をクリックして**既定値にリセット**既定のデータベースとスキーマに戻す。  
  
## <a name="next-steps"></a>次の手順  
Oracle オブジェクトの変換を分析する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトを実行できます[変換レポートを作成する](assessing-oracle-schemas-for-conversion-oracletosql.md)します。 それ以外の場合できます[Oracle データベースのオブジェクトの定義の変換](converting-oracle-schemas-oracletosql.md)に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト定義。  
  
## <a name="see-also"></a>関連項目  
[SQL Server に接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
