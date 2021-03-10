VB.Net - Execute and Log Shell Command Output

```vb.net
Public Class Example

    Private example_process As Process
    
    Public Sub Start
        Dim exe_path As String = ""
        
        example_process = New Process()
        example_process.StartInfo.RedirectStandardOutput = True
        example_process.StartInfo.RedirectStandardError  = True
        example_process.StartInfo.UseShellExecute        = False
        example_process.StartInfo.CreateNoWindow         = True
        example_process.StartInfo.Arguments              = ""
        example_process.StartInfo.FileName               = exe_path
        
        AddHandler example_process.OutputDataReceived, AddressOf LogProcessOutput
        
        example_process.Start()
        example_process.BeginOutputReadLine()
        example_process.BeginErrorReadLine()
        example_process.WaitForExit()
        example_process.Dispose()
    End Sub
    
    Public Sub End
        example_process.Dispose()
    End Sub
    
    Private Sub LogProcessOutput(sendingProcess As Object, outLine As DataReceivedEventArgs)
        If Not String.IsNullOrEmpty(outLine.Data) Then
            ' ExampleForm.TextBox1.Text = TextBox1.Text + outLine.Data + vbNewLine
        End If
    End Sub
    
End Class
```
