# PowerShell

Split paths into different components: `Split-Path`, see [*Do multiple (git-related) things in multiple subfolders*](#do-multiple-git-related-things-in-multiple-subfolders), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/split-path?view=powershell-7.1

## Do multiple (git-related) things in multiple subfolders:

```PowerShell
param([string]$checkoutBranch = "master")

function Get-AllRepos ([string]$checkoutBranch = "master")
{
    Get-ChildItem -Recurse -Depth 2 -Force |
        Where-Object { $_.Mode -match "h" -and $_.FullName -like "*\.git" } |
        ForEach-Object {
            $dir = Get-Item (Join-Path $_.FullName "../")
            ##pushd $dir
            Push-Location $dir

            if ($checkoutBranch) {
                $branch= &git rev-parse --abbrev-ref HEAD

                if ($branch -ne $checkoutBranch) {
                    "Checkout out $($checkoutBranch) branch for $($dir.Name)"
                    git checkout $checkoutBranch
                }
            }

            "Pulling $($dir.Name)"
			$reponame = Split-Path $dir -leaf
            Write-Host $(git remote add REMOTENAME PATHTOREMOTE/$reponame) -ForegroundColor Green
			#Start-Sleep -Seconds 5
			Write-Host $(git fetch -a REMOTENAME) -ForegroundColor Green
			#Start-Sleep -Seconds 5
			Write-Host $(git branch BRANCHNAME REMOTENAME/BRANCHNAME) -ForegroundColor Green
			#Start-Sleep -Seconds 5
			Write-Host $(git remote remove REMOTENAME) -ForegroundColor Green
            #Start-Sleep -Seconds 5
			##popd
            Pop-Location
        }
 }

 Get-AllRepos $checkoutBranch
```

- Partial source: http://antonkallenberg.com/2017/12/02/execute-a-git-command-in-multiple-folders-using-powershell/
- https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/start-sleep?view=powershell-7.1
