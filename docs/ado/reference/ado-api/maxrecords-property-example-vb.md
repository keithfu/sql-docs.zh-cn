---
title: "最大记录的属性示例 (VB) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- MaxRecords property [ADO], Visual Basic example
ms.assetid: 630a3be4-7a87-41cf-997e-8bb50d89db1e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6bc345e6b09ba099c8b34c74cdd0e57248ac3756
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="maxrecords-property-example-vb"></a>最大记录的属性示例 (VB)
此示例使用[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)以打开[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)包含中的 10 成本最高标题***标题***表。  
  
```  
'BeginMaxRecordsVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim rstTitles As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset containing the 10 most expensive  
    ' titles in the Titles table  
    Set rstTitles = New ADODB.Recordset  
    rstTitles.MaxRecords = 10  
  
    strSQLTitles = "SELECT Title, Price FROM Titles ORDER BY Price DESC"  
    rstTitles.Open strSQLTitles, strCnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    ' Display the contents of the recordset  
    Debug.Print "Top Ten Titles by Price:"  
  
    Do Until rstTitles.EOF  
        Debug.Print "  " & rstTitles!Title & " - " & rstTitles!Price  
        rstTitles.MoveNext  
    Loop  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndMaxRecordsVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [最大记录属性 (ADO)](../../../ado/reference/ado-api/maxrecords-property-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)