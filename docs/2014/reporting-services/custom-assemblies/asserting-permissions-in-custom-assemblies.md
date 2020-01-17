---
title: カスタム アセンブリでのアクセス許可のアサート | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- secure calls [Reporting Services]
- custom assemblies [Reporting Services], permissions
- permission sets [Reporting Services]
- asserting permissions
- permissions [Reporting Services], custom assemblies
- limited permission sets
- security configuration files [Reporting Services]
ms.assetid: 3afb9631-f15e-405e-990b-ee102828f298
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f66896479ec06d78b94d6fe084ff806e3af67727
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63265381"
---
# <a name="asserting-permissions-in-custom-assemblies"></a>カスタム アセンブリでの権限のアサート
  既定では、カスタム アセンブリ コードは、限定された **Execution** アクセス許可セットに基づいて実行されます。 ただし、場合によっては、(ファイルやレジストリなど) セキュリティ システムで保護されたリソースを安全に呼び出すカスタム アセンブリを実装する必要が生じる場合もあります。 そのためには、次の操作を実行する必要があります。  
  
1.  セキュリティで保護された呼び出しを行うために、コードに必要な正しい権限を識別します。 このメソッドが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ライブラリの一部である場合、この情報をメソッド ドキュメントに含める必要があります。  
  
2.  カスタム アセンブリに必要な権限を与えるために、レポート サーバー ポリシーの構成ファイルを変更します。 セキュリティ ポリシー構成ファイルの詳細については、「[Reporting Services セキュリティ ポリシー ファイルの使用](../extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。  
  
3.  セキュリティで保護された呼び出しを行うメソッドの一部として、必要な権限をアサートします。 レポート サーバーによって呼び出されるカスタム アセンブリ コードは、レポート式のホスト アセンブリの一部であり、既定では **Execution** アクセス許可で実行するため、このアサートが必要です。 **Execution** アクセス許可セットでコードを実行できますが、保護されたリソースを使用することはできません。  
  
4.  カスタム アセンブリが厳密な名前で署名されている場合、カスタム アセンブリを **AllowPartiallyTrustedCallersAttribute** でマークします。 カスタム アセンブリは、レポート式のホスト アセンブリの一部であるレポート式から呼び出され、既定では、**FullTrust** が与えられていない、つまり、"部分的な信頼関係のある" 呼び出し元であるため、このマークが必要です。 詳細については、「[複雑な名前を持つカスタム アセンブリの使用](using-strong-named-custom-assemblies.md)」を参照してください。  
  
## <a name="implementing-a-secure-call"></a>セキュリティで保護された呼び出しの実装  
 ポリシーの構成ファイルを変更して、アセンブリに特定の権限を与えます。 たとえば、通貨換算を処理するためにカスタム アセンブリを書き込んだ場合、現在の通貨換算レートをファイルから読み取らなければならない場合があります。 換算レート情報を取得するには、追加セキュリティ アクセス許可 **FileIOPermission** をアセンブリのアクセス許可セットに追加する必要があります。 ポリシーの構成ファイルで次の追加エントリを作成できます。  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="CurrencyRatesFilePermissionSet"  
   Description="A special permission set that grants read access to my currency rates file.">  
      <IPermission class="FileIOPermission"  
         version="1"  
         Read="C:\CurrencyRates.xml"/>  
      <IPermission class="SecurityPermission"  
         version="1"  
         Flags="Execution, Assertion"/>  
</PermissionSet>  
```  
  
 次のように、アセンブリの権限セットを参照するコード グループを追加します。  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="CurrencyRatesFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\MSSQL\Reporting Services\ReportServer\bin\CurrencyConversion.dll"/>  
</CodeGroup>  
```  
  
 コードに適切な権限を取得するためには、カスタム アセンブリ コード内で権限をアサートする必要があります。 たとえば、XML ファイル C:\CurrencyRates.xml の読み取り専用アクセスを追加する場合、次のコードをメソッドに追加する必要があります。  
  
```  
// C#  
FileIOPermission permission = new FileIOPermission(FileIOPermissionAccess.Read, @"C:\CurrencyRates.xml");  
try  
{  
   permission.Assert();  
   // Load the XML currency rates file  
   XmlDocument doc = new XmlDocument();  
   doc.Load(@"C:\CurrencyRates.xml");  
...  
```  
  
 次のように、アサーションをメソッド属性として追加することもできます。  
  
```  
[FileIOPermissionAttribute(SecurityAction.Assert, Read=@"C:\CurrencyRates.xml")]  
```  
  
 詳細については、『.NET Framework 開発者ガイド』の「.NET Framework セキュリティ」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポートでのカスタム アセンブリの使用](using-custom-assemblies-with-reports.md)  
  
  
