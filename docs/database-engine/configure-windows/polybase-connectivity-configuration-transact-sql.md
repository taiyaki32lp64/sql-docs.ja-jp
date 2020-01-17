---
title: PolyBase 接続構成 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
ms.assetid: 82252e4f-b1d0-49e5-aa0b-3624aade2add
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d86483245f8a4f06dfcb357d5d105539dd56f3a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997918"
---
# <a name="polybase-connectivity-configuration-transact-sql"></a>PolyBase 接続構成 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  PolyBase での Hadoop と Azure BLOB ストレージの接続に対するグローバル構成設定を表示または変更します。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
--List all of the configuration options  
sp_configure  
[;]  
  
--Configure Hadoop connectivity  
sp_configure [ @configname = ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ **@configname=** ] **'** _option\_name_ **'**  
 構成オプションの名前を指定します。 *option_name* は **varchar(35)** 、既定値は NULL です。 指定しない場合、オプションの完全な一覧が返されます。  
  
 [ **@configvalue=** ] **'** _value_ **'**  
 新しい構成設定を指定します。 *value* のデータ型は **int**で、既定値は NULL です。 最大値はオプションごとに異なります。  
  
 **'hadoop connectivity'**  
 PolyBase から Hadoop クラスターまたは Azure BLOB ストレージ (WASB) へのすべての接続に Hadoop データ ソースの種類を指定します。 この設定は、外部テーブルに外部データ ソースを作成するために必要です。 詳細については、「 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)」を参照してください。  
  
 Hadoop の接続設定とそれに対応してサポートされる Hadoop データ ソースがあります。 一度に 1 つの設定だけを有効にすることができます。 オプション 1、4、および 7 では、複数の種類の外部データ ソースを作成して、サーバー上のすべてのセッションで使用することができます。  
  
-   オプション 0:Hadoop 接続の無効化  
  
-   オプション 1:Windows Server 上の Hortonworks HDP 1.3  
  
-   オプション 1:Azure BLOB ストレージ (WASB[S])  
  
-   オプション 2:Linux 上の Hortonworks HDP 1.3  
  
-   オプション 3:Linux 上の Cloudera CDH 4.3  
  
-   オプション 4:Windows Server 上の Hortonworks HDP 2.0  
  
-   オプション 4:Azure BLOB ストレージ (WASB[S])  
  
-   オプション 5:Linux 上の Hortonworks HDP 2.0  
  
-   オプション 6:Linux 上の Cloudera 5.1、5.2、5.3、5.4、5.5、5.9、5.10、5.11、5.12、5.13  
  
-   オプション 7:Linux 上の Hortonworks 2.1、2.2、2.3、2.4、2.5、2.6、3.0  
  
-   オプション 7:Windows Server 上の Hortonworks 2.1、2.2、2.3  
  
-   オプション 7:Azure BLOB ストレージ (WASB[S])  
  
 **RECONFIGURE**  
 構成値 (config_value) と一致するように、実行値 (run_value) を更新します。 run_value と config_value の定義については、「 [結果セット](#ResultSets) 」を参照してください。 sp_configure で設定されている新しい構成値は、実行値が RECONFIGURE ステートメントで設定されるまで有効になりません。  
  
 RECONFIGURE を実行した後に、SQL Server サービスを停止して再起動する必要があります。 SQL Server サービスを停止すると、追加された PolyBase エンジンとデータ移動サービスの 2 つが自動的に停止されることにご注意ください。 SQL Server エンジン サービスを再起動した後に、これら 2 つのサービスをもう一度再起動します (自動的には起動されません)。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
##  <a name="ResultSets"></a> 結果セット  
 パラメーターなしで実行されると、 **sp_configure** は 5 つの列を含む結果セットを返します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|構成オプションの名前。|  
|**minimum**|**int**|構成オプションの最小値。|  
|**maximum**|**int**|構成オプションの最大値。|  
|**config_value**|**int**|**sp_configure**を使用して設定された値。|  
|**run_value**|**int**|PolyBase が使用する現在の値。 この値は、RECONFIGURE を実行すると設定されます。<br /><br /> 値が変更中のプロセスではない限り、 **config_value** と **run_value** は、通常は同じ値です。<br /><br /> 再構成が進行中である場合、この実行値を正確にするために、再起動が必要になる可能性があります。|  
  
## <a name="general-remarks"></a>全般的な解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、RECONFIGURE を実行した後に、'hadoop connectivity' の実行値を有効にするために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動する必要があります。  
[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]では、RECONFIGURE を実行した後に、'hadoop connectivity' の実行値を有効にするために、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 領域を再起動する必要があります。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 RECONFIGURE は、明示的または暗黙的なトランザクションでは使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 すべてのユーザーは、パラメーターなし、または **パラメーターを使用して、** sp_configure @configname を実行することができます。  
  
 構成値を変更する、または RECONFIGURE を実行するには、 **sysadmin** 固定サーバー ロールに **ALTER SETTINGS** サーバー レベルの権限またはメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-list-all-available-configuration-settings"></a>A. すべての使用可能な構成設定を一覧表示する  
 次の例では、すべての構成オプションを一覧表示する方法を示します。  
  
```  
EXEC sp_configure;  
```  
  
 結果は、オプションの最小値と最大値が続くオプション名を返します。 **config_value** は、再構成が完了したときに、SQL (または PolyBase) が使用する値です。 **run_value** は、現在使用されている値です。 値が変更中のプロセスではない限り、 **config_value** と **run_value** は、通常は同じ値です。  
  
### <a name="b-list-the-configuration-settings-for-one-configuration-name"></a>B. 1 つの構成名の構成設定を一覧表示する  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="c-set-hadoop-connectivity"></a>C. Hadoop 接続を設定する  
 この例では、PolyBase をオプション 7 に設定します。 このオプションでは、PolyBase は、Linux と Windows Server、および Azure BLOB ストレージ上の Hortonworks 2.1、2.2、および 2.3 の外部テーブルを作成および使用できます。 たとえば、SQL は 30 個の外部テーブルを、Linux 上の Hortonworks 2.1 のデータを参照する 7 個、Linux 上の Hortonworks 2.2 の 4 個、Linux 上の Hortonworks 2.3 の 7 個、Azure BLOB ストレージを参照するその他の 12 個の外部テーブルとして所有することができます。  
  
```  
--Configure external tables to reference data on Hortonworks 2.1, 2.2, and 2.3 on Linux, and Azure blob storage  
  
sp_configure @configname = 'hadoop connectivity', @configvalue = 7;  
GO  
  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
