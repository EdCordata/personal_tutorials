# VB.Net - Run Code in Thread

```vb.net
Public Class Example

    Dim perform_action_thread As New Threading.Thread(AddressOf PerformAction)

    Public Sub StartAction
        perform_action_thread.Start()
    End Sub

    Public Sub EndAction
        perform_action_thread.Abort()
    End Sub
    
    Private Sub PerformAction()
        ' Your code
    End Sub

End Class
```
