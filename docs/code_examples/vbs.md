# VBScript


## General


###### Exit Script:
```vbs
WScript.Quit
```


###### Alert MsgBox:
```vbs
Wscript.Echo "hello world"
```


###### Evaluate Admin Permissions:
```vbs
Set Application = CreateObject("Shell.Application")

If WScript.Arguments.Length = 0 Then
  Application.ShellExecute "wscript.exe", """" & WScript.ScriptFullName & """ RunAsAdministrator", , "runas", 1
  WScript.Quit
End if
```


###### Show Yes/No Popup:
```vbs
Set Shell = CreateObject("Wscript.Shell")

timeout = 15 ' seconds. 0 = no timeout
intReturn = Shell.Popup("Click Yes or No!", timeout, "My Title", vbYesNo + vbQuestion)

If (intReturn = vbYes) Then
  Wscript.Echo "Yes was clicked"
End If
If (intReturn = vbNo) Then
  Wscript.Echo "No was clicked"
End If

If (intReturn = -1) Then
  Wscript.Echo "Popup timed out"
End If
```


###### Create Named Function:
```vbs
Function FuncName(sText)
  Wscript.Echo sText
End Function

FuncName("abc")
```


## Path


###### Generate Valid Path:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")

ROOT = FileSystemObject.GetParentFolderName(Wscript.ScriptFullName)

FileSystemObject.BuildPath("C:/", "/test.txt") ' => C:/test.txt
FileSystemObject.BuildPath("C:/", "test.txt") ' => C:/test.txt
```


###### Get Current Path:
```vbs
set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
```


###### Get Windows Folders:
```vbs
Set Shell = CreateObject("WScript.Shell")
windir = Shell.ExpandEnvironmentStrings("%windir%")
```


###### Get User Folders:
```vbs
Set Shell = CreateObject("WScript.Shell")
profiledir = Shell.ExpandEnvironmentStrings("%userprofile%")
```


## Files


###### Create Text File:
```vbs
set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")

Set file = FileSystemObject.CreateTextFile(ROOT + "/test.txt", True)
file.WriteLine("This is a test.")
file.Close
```


###### Read Text File:
```vbs
set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
STR  = FileSystemObject.OpenTextFile(ROOT + "/test.txt").ReadAll
```


###### Read Text File Line-By-Line:
```vbs
set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")

Set FILE = FileSystemObject.OpenTextFile(ROOT + "/test/test.txt")

Do Until FILE.AtEndOfStream
  WScript.Echo FILE.ReadLine
Loop

FILE.Close
```


###### Move File:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
FileSystemObject.MoveFile ROOT + "/test.txt", ROOT + "/test_2.txt"
```


###### Copy File:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
FileSystemObject.CopyFile ROOT + "/test.txt", ROOT + "/test_2.txt"
```


###### Delete File:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
FileSystemObject.DeleteFile ROOT + "/test.txt"
```


###### Check If File Exists:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")

If FileSystemObject.FileExists("C:/test.txt") Then
  WScript.Echo("yes")
Else
  WScript.Echo("no")
End If
```


###### Check If Folder Exists:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")

If FileSystemObject.FolderExists("C:/") Then
  WScript.Echo("yes")
Else
  WScript.Echo("no")
End If
```


###### Get Files In Folder:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")

For Each file in FileSystemObject.GetFolder(ROOT).files
  file_Name              = file.Name
  file_DateCreated       = file.DateCreated
  file_DateLastAccessed  = file.DateLastAccessed
  file_DateLastModified  = file.DateLastModified
  file_ParentFolder      = file.ParentFolder
  file_Path              = file.Path
  file_Size              = file.Size
  file_Type              = file.Type
  file_Extension         = FileSystemObject.GetExtensionName(file.Name)
Next
```


## Folder


###### Create Folder:
```
set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
FileSystemObject.CreateFolder(ROOT + "/test")
```


###### Move Folder:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
FileSystemObject.MoveFolder ROOT + "/test", ROOT + "/test_2"
```


###### Copy Folder:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
FileSystemObject.CopyFolder ROOT + "/test", ROOT + "/test_2"
```


###### Delete Folder:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")
FileSystemObject.DeleteFolder ROOT + "/test"
```


###### Check If Folder Exists:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")

If FileSystemObject.FolderExists("C:/test") Then
	WScript.Echo("yes")
Else
	WScript.Echo("no")
End If
```


###### List Folder Sub-Folders:
```vbs
Set FileSystemObject = CreateObject("Scripting.FileSystemObject")
ROOT = FileSystemObject.GetAbsolutePathName(".")

For Each folder in FileSystemObject.GetFolder(ROOT).SubFolders
  folder_Name              = folder.Name
  folder_DateCreated       = folder.DateCreated
  folder_DateLastAccessed  = folder.DateLastAccessed
  folder_DateLastModified  = folder.DateLastModified
  folder_Size              = folder.Size
Next
```


## System


###### Import Reg File:
```vbs
Set Shell = CreateObject("WScript.Shell")
Shell.Run("REG.EXE IMPORT " + Chr(34) + "C:/test.reg" + Chr(34))
```


###### Remove a reg key
```vbs
Set Shell = CreateObject("WScript.Shell")
Shell.Run("reg delete " + Chr(34) + "HKEY_CURRENT_USER\path\to\key" + Chr(34) + " /f")
```


###### Execute command:
```vbs
Set Shell = WScript.CreateObject ("WScript.Shell")
Shell.run ""
```


###### Create Shortcut To File:
```vbs
Set Shell = WScript.CreateObject("WScript.Shell")

link_location = Shell.ExpandEnvironmentStrings("%userprofile%") + "\Desktop\notepad.lnk"
link_target   = Shell.ExpandEnvironmentStrings("%windir%") + "\System32\notepad.exe"
link_icon     = Shell.ExpandEnvironmentStrings("%windir%") + "\system32\notepad.exe, 0"

Set lnk = Shell.CreateShortcut(link_location)
lnk.IconLocation     = link_icon
lnk.TargetPath       = link_target
lnk.Save
Set lnk = Nothing 'Clean up
```


###### Create Shortcut To Folder:
```vbs
Set Shell = WScript.CreateObject("WScript.Shell")

link_location = Shell.ExpandEnvironmentStrings("%userprofile%") + "\Desktop\system32.lnk"
link_target   = Shell.ExpandEnvironmentStrings("%windir%") + "\System32"
link_icon     = Shell.ExpandEnvironmentStrings("%windir%") + "\explorer.exe, 0"

Set lnk = Shell.CreateShortcut(link_location)
lnk.IconLocation     = link_icon
lnk.TargetPath       = link_target
lnk.Save
Set lnk = Nothing 'Clean up
```


###### Creates a Directory Junction
That means shortcut acts like folder. Meaning - no folder with links name can be created in the same directory.
```vbs
Set Shell = CreateObject("WScript.Shell")

link_location = Shell.ExpandEnvironmentStrings("%userprofile%") + "\Desktop"
link_target   = Shell.ExpandEnvironmentStrings("%windir%") + "\System32"

Shell.run "cmd.exe /C mklink /J """ + link_location + """ """ + link_target + """ ", 0, False
```


###### Remove a Directory Junction
Removes junction without removing source folder
```vbs
link_location = Shell.ExpandEnvironmentStrings("%userprofile%") + "\Desktop\System32"
Shell.run "cmd.exe /C rmdir """ + link_location + """ ", 0, False
```


###### Rescue from error
```vbs
On Error Resume Next ' rescue from errors from this point on
' code with error
On Error Goto 0 ' stop rescueing errors
```


## String Manipulation


###### Replace In String:
```vbs
Replace("123", "1", "a") ' =>  "a23"
```


###### Get String Length:
```vbs
Len("abc") ' => 3
```


###### Convert String To Uppercase:
```vbs
Ucase("abc") ' => "ABC"
```


###### Convert String To Downcase:
```vbs
Lcase("ABC") ' => "abc"
```


###### Slice String:
```vbs
Left("abc", 1)  ' => "a"
Right("abc", 1) ' => "c"
```

###### Check if variable is null
```vbs
IsNull(variable)
```
###### Command Line Arguments
```vbs
Set CommandLineArguments  = WScript.Arguments
CommandLineArgumentsCount = CommandLineArguments.Count

If CommandLineArgumentsCount = 0 Then
  MsgBox "No Arguments"
Else
  For Each arg in CommandLineArguments 
    MsgBox arg 
  Next
End If
```

###### Array Length
```vbs
days=Array("Sun","Mon","Tue","Wed","Thu","Fri","Sat")
days_count = (UBound(days) + 1)

MsgBox days_count
```

## Resources
* https://ss64.com/vb/
* https://www.tutorialspoint.com/vbscript
* https://docs.microsoft.com/en-us/office/vba/language/reference/objects-visual-basic-for-applications
