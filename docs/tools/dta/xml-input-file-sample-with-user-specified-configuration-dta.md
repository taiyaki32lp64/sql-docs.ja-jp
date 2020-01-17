---
title: ユーザー指定の構成を指定した XML 入力ファイルのサンプル (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ebe9fd101be343c5fb07e713e02351f6f5c9828f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105902"
---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>ユーザー指定の構成を指定した XML 入力ファイルのサンプル (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  この XML 入力ファイルのサンプルでは、ユーザー指定の構成を **Configuration** 要素を使用して指定しています。このサンプルをコピーして、お使いの XML エディターやテキスト エディターに貼り付けてください。 これにより、"what-if" 分析を行うことができます。 "What-if" 分析では、 **Configuration** 要素を使用して、チューニング対象のデータベースに対して仮想的な物理設計構造のセットを指定します。 その後、データベース エンジン チューニング アドバイザーを使用して、この仮想的な構成に対してワークロードを実行した場合の影響を分析し、クエリ処理のパフォーマンスが向上するかどうかを調べます。 このタイプの分析には、実際に実装しなくても新しい構成を評価できるという利点があります。 仮想の構成で、期待したパフォーマンスの向上が得られなかった場合は、簡単に構成を変更でき、望ましい結果を生成する構成になるまで分析を繰り返し行えます。  
  
 このサンプルを編集ツールにコピーした後に、 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、 **TuningOptions**、および **Configuration** 要素で指定する値を、特定のチューニング セッションの値に置き換えてください。 これらの要素で使用できるすべての属性および子要素の詳細については、「 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)」を参照してください。 以下のサンプルでは、使用できる属性や子要素の一部だけを使用しています。  
  
## <a name="code"></a>コード  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<DTAXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="https://schemas.microsoft.com/sqlserver/2004/07/dta">  
  <DTAInput>  
    <Server>  
      <Name>MyServerName</Name>  
<!-- To tune multiple databases, list them and their associated tables in the following section. -->  
      <Database>  
        <Name>MyDatabaseName</Name>  
        <Schema>  
          <Name>MyDatabaseSchemaName</Name>  
<!-- You can list as many tables as necessary in the following section. -->  
          <Table>  
            <Name>MyTableName1</Name>  
          </Table>  
          <Table>  
            <Name>MyTableName2</Name>  
          </Table>  
        </Schema>  
      </Database>  
    </Server>  
    <Workload>  
<!-- The following element specifies a workload file, which can be a trace file or a Transact-SQL script file. -->  
      <File>c:\PathToYourWorkloadFile</File>  
    </Workload>  
    <TuningOptions>  
      <TuningTimeInMin>180</TuningTimeInMin>  
      <StorageBoundInMB>10000</StorageBoundInMB>  
      <FeatureSet>IDX_IV</FeatureSet>  
      <Partitioning>NONE</Partitioning>  
      <KeepExisting>NONE</KeepExisting>  
      <OnlineIndexOperation>OFF</OnlineIndexOperation>  
    </TuningOptions>  
    <Configuration SpecificationMode="Absolute">  
      <Server>  
        <Name>MyServerName</Name>  
          <Database>  
            <Name>MyDatabaseName</Name>  
            <Schema>  
              <Name>MyDatabaseSchemaName</Name>  
                <Table>  
                  <Name>MyTableName1</Name>  
                  <Recommendation>  
                    <Create>  
                      <Index Clustered="true" Unique="false" Online="false" IndexSizeInMB="873.75">  
                        <Name>MyIndexName</Name>  
                        <Column Type="KeyColumn" SortOrder="Ascending">  
                          <Name>MyColumnName1</Name>  
                        </Column>  
                        <Filegroup>MyFileGroupName1</FileGroup>  
                      </Index>  
                    </Create>  
                  </Recommendation>  
                </Table>  
            </Schema>  
          </Database>  
      </Server>  
    </Configuration>  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="comments"></a>コメント  
  
-   **Configuration** 要素に **Absolute** モードを指定した場合 (`Configuration SpecificationMode="Absolute"`)、物理設計構造の削除はサポートされません。  
  
-   **Configuration** 要素のいずれのモードでも ( **Relative**または **Absolute** )、同一の物理設計構造の作成と削除はできません。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [データベース エンジン チューニング アドバイザーからの出力の表示および操作](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
