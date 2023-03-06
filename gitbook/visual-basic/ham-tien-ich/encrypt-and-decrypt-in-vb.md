---
description: Encrypt and Decrypt in VB
---

# Encrypt and Decrypt in VB

```vbnet
  Public Shared Function Encrypt(ByVal strKey As String, ByVal strData As String) As String
        If (strKey = "") Then Return strData
        Dim num As Integer = Strings.Len(strKey)
        If (num < &H10) Then
            strKey = (strKey & Strings.Left("XXXXXXXXXXXXXXXX", (&H10 - Strings.Len(strKey))))
        ElseIf (num > &H10) Then
            strKey = Strings.Left(strKey, &H10)
        End If
        Dim bytes As Byte() = Encoding.UTF8.GetBytes(Strings.Left(strKey, 8))
        Dim rgbIV As Byte() = Encoding.UTF8.GetBytes(Strings.Right(strKey, 8))
        Dim buffer As Byte() = Encoding.UTF8.GetBytes(strData)
        Dim provider As New DESCryptoServiceProvider
        Dim stream2 As New MemoryStream
        Dim stream As New CryptoStream(stream2, provider.CreateEncryptor(bytes, rgbIV), CryptoStreamMode.Write)
        stream.Write(buffer, 0, buffer.Length)
        stream.FlushFinalBlock()
        Return Convert.ToBase64String(stream2.ToArray)
    End Function

    Public Shared Function Decrypt(ByVal strKey As String, ByVal strData As String) As String
        If (strData = "") Then Return ""
        Dim str2 As String = ""
        If (strKey = "") Then Return strData
        Dim num As Integer = Strings.Len(strKey)
        If (num < &H10) Then
            strKey = (strKey & Strings.Left("XXXXXXXXXXXXXXXX", (&H10 - Strings.Len(strKey))))
        ElseIf (num > &H10) Then
            strKey = Strings.Left(strKey, &H10)
        End If
        Dim bytes As Byte() = Encoding.UTF8.GetBytes(Strings.Left(strKey, 8))
        Dim rgbIV As Byte() = Encoding.UTF8.GetBytes(Strings.Right(strKey, 8))
        Dim buffer As Byte() = New Byte((strData.Length + 1) - 1) {}
        Try
            buffer = Convert.FromBase64String(strData)
        Catch exception1 As Exception
            ProjectData.SetProjectError(exception1)
            str2 = strData
            ProjectData.ClearProjectError()
        End Try
        If (str2 = "") Then
            Try
                Dim provider As New DESCryptoServiceProvider
                Dim stream2 As New MemoryStream
                Dim stream As New CryptoStream(stream2, provider.CreateDecryptor(bytes, rgbIV), CryptoStreamMode.Write)
                stream.Write(buffer, 0, buffer.Length)
                stream.FlushFinalBlock()
                str2 = Encoding.UTF8.GetString(stream2.ToArray)
            Catch exception2 As Exception
                ProjectData.SetProjectError(exception2)
                str2 = ""
                ProjectData.ClearProjectError()
            End Try
        End If
        Return str2
    End Function

```
