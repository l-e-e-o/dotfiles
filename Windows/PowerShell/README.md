# PowerShell

Edit the profile configuration via

```ps1
notepad $profile
```

and insert the following config

```ps1
Set-PSReadLineKeyHandler -Chord ctrl+w -Function BackwardDeleteWord
Set-PSReadLineKeyHandler -Chord ctrl+d -Function DeleteCharOrExit
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
Set-PSReadLineKeyHandler -Key Tab -Function MenuComplete
```
