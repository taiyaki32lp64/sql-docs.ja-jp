---
title: レポート定義スキーマのバージョンを確認する (SSRS) | Microsoft Docs
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 129fcb8e1533162560b88e9400c68c7c863be119
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826843"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>レポート定義スキーマのバージョンを確認する (SSRS)

レポート定義ファイルでは、rdl ファイルの検証に使用されるレポート定義スキーマのバージョンに対応して、RDL 名前空間が指定されます。 レポート作成環境でのレポート デザイナーなどで .rdl ファイルを開く[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、Visual Studio、またはレポート ビルダー。 場合は、レポートの以前の名前空間の作成、バックアップ ファイルが自動的に作成し、レポートは現在の名前空間にアップグレードします。 アップグレードされたレポート定義を保存すると、変換された .rdl ファイルが保存されることになります。 これは、レポート定義をアップグレードする唯一の方法です。 レポート定義そのものはレポート サーバーでアップグレードされません。 コンパイル済みレポートが、レポート サーバーで自動的にアップグレードされます。 詳細については、「 [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md)」を参照してください。  
  
## <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>方法: レポートの RDL スキーマのバージョンを確認する  
  
1. XML を表示できる、メモ帳や XML Notepad などのアプリケーションで、レポートの .rdl ファイルを開きます。  
  
     スキーマ名前空間は XML の Report 要素で指定されます。 たとえば、次の Report 要素では、レポート デザイナーの名前空間とレポート定義の名前空間が指定されています。  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     最新のレポート定義の名前空間は、2016 です。 ただし、2010、次の URL で指定されたは、最新のパブリッシュされたレポート定義の名前空間: `https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`.
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>方法: レポート デザイナーの RDL スキーマのバージョンを確認する  
  
1.  新しいプロジェクトを開きます。 選択したプロジェクトのバージョンにより、RDL スキーマのバージョンが決まります。 SQL Server では、複数のスキーマ バージョンがサポートされています。 詳細については、「[SQL Server データ ツールの配置およびバージョン サポート](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)」を参照してください。  
  
2.  **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
3.  **[テンプレート]** ペインで **[レポート]** をクリックします。  
  
4.  **[名前]** にレポートの名前を入力するか、既定の名前をそのまま使用します。  
  
5.  **[追加]** をクリックします。 レポート デザイナーの [デザイン] ビューに新しい空のレポートが表示されます。  
  
6.  **[表示]** メニューの **[コード]** をクリックします。 レポート定義が XML ファイルとして表示されます。  
  
    スキーマ名前空間は XML の Report 要素で指定されます。 たとえば、次の Report 要素では、レポート デザイナーの名前空間とレポート定義の名前空間が指定されています。  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     レポート定義の名前空間は、 `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>方法: レポート サーバー上で RDL スキーマのバージョンを確認する  
  
-   Web ポータルでは、レポート サーバーの URL を入力します。 たとえば、次の URL はローカル コンピューターのレポート サーバーを指定しています。  
  
     `https://localhost/reportserver/reportdefinition.xsd`  
  
     .xsd ファイルがブラウザーに表示されます。  
  
     スキーマ名前空間は XML の schema 要素で指定されます。 たとえば、次の schema 要素では、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]によって内部的に使用される targetNamespace 参照、スキーマ自体 (xsd) の xsd 参照、およびレポート定義参照の 3 つの名前空間が指定されています。  *年*レポートを使用してスキーマの年を表します。 たとえば、2010 または 2016。
  
    ``` XML  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" elementFormDefault="qualified">  
    ```  
  
     レポート定義の名前空間は、 `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  

## <a name="next-steps"></a>次の手順
[レポートのアップグレード](../../reporting-services/install-windows/upgrade-reports.md)   
[レポート定義言語 (Report Definition Language)](../../reporting-services/reports/report-definition-language-ssrs.md)   

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
