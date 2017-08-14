# PowerShell Cheatsheet

## Discovery within PowerShell
* `Get-Command write-*` : get all commands that begin with "write-"
* `Get-Help Get-Command -detailed` : find out how to use "Get-Command"
* `Get-Date | Get-Member` : get all methods and properties of the DateTime object, just pipe the object to `Get-Member`. In PowerShell, every output is a .NET object.

## Good to know
* `$_` is the variable for the current value in the pipeline

## Sources
* [Effective Windows PowerShell ebook](https://rkeithhill.wordpress.com/2009/03/08/effective-windows-powershell-the-free-ebook/) from Keith Hill