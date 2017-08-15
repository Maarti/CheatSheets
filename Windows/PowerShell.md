# PowerShell Cheatsheet

## Discovery within PowerShell
* `Get-Command write-*` : get all commands that begin with "write-"
* `Get-Help Get-Command -detailed` : find out how to use "Get-Command"
* `Get-Date | Get-Member` : get all methods and properties of the DateTime object, just pipe the object to `Get-Member`. *(In PowerShell, every output is a .NET object.)*

## Good to know
* `$_` is the variable for the current value in the pipeline.
* **In PowerShell, every output is a .NET object.**

## Functions
Function output consists of everything that isn't captured :
```powershell
function bar {
	$procs = Get-Process svchost
	"Returning svchost process objects"
	return $procs
}
```
The above function returns :
```
PS> $result = bar
PS> $result | foreach {$_.GetType().Fullname}
	System.String
	System.Diagnostics.Process
	System.Diagnostics.Process
	System.Diagnostics.Process
	...
```
It returns the Process objects but also the string that has not been captured.
> First, the `return` keyword allows you to exit the function at any particular point. You may also "optionally" specify an argument to the return statement that will cause the argument to be output just before returning. `return $procs` does not mean that the function’s only output is the contents of the $procs variable. In fact this construct is semantically equivalent to `$procs; return`. 
> 
> -- <cite>[Effective Windows PowerShell ebook](https://rkeithhill.wordpress.com/2009/03/08/effective-windows-powershell-the-free-ebook/)</cite>

To avoid the unwanted output, just throw it away by casting it to "void" :
```powershell
function LongNumericString {
	$strBld = new-object System.Text.StringBuilder
	for ($i=0; $i -lt 20; $i++) {
		[void]$strBld.Append($i)
	}
	$strBld.ToString()
}

LongNumericString
```
Try this code with and without the `[void]` cast.

## Debugging
* Use `Get-Member` to display **properties and methods** available on objects.
* Use `Format-List *` to display all the **property values** on objects.
* Create the filter "Get-TypeName" : `filter Get-TypeName {if ($_ -eq $null) {'<null>'} else {$_.GetType().Fullname }}` and use it to see the type names of each object passed down the pipe : `Get-Date | Get-TypeName`


## Resources
* [Effective Windows PowerShell ebook](https://rkeithhill.wordpress.com/2009/03/08/effective-windows-powershell-the-free-ebook/) from Keith Hill
* [Microsoft PowerShell examples and quick ref](https://www.microsoft.com/en-us/download/details.aspx?id=42554&WT.mc_id=rss_alldownloads_all)