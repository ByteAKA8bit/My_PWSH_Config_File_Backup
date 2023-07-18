# My_PWSH_Config_File_Backup

```powershell
# cls

#------------------------------- Import Modules BEGIN -------------------------------
# 引入 posh-git
Import-Module posh-git

# 引入 ps-read-line
Import-Module PSReadLine

#------------------------------- Import Modules END   -------------------------------

#-------------------------------  Set Hot-keys BEGIN  -------------------------------
# 设置预测文本来源为历史记录
Set-PSReadLineOption -PredictionSource History

# 每次回溯输入历史，光标定位于输入内容末尾
Set-PSReadLineOption -HistorySearchCursorMovesToEnd

# 设置 Tab 为菜单补全和 Intellisense
Set-PSReadLineKeyHandler -Key "Tab" -Function MenuComplete

# 设置 Ctrl+d 为退出 PowerShell
Set-PSReadlineKeyHandler -Key "Ctrl+d" -Function ViExit

# 设置 Ctrl+z 为撤销
Set-PSReadLineKeyHandler -Key "Ctrl+z" -Function Undo

# 设置向上键为后向搜索历史记录
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward

# 设置向下键为前向搜索历史纪录
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
#-------------------------------  Set Hot-keys END    -------------------------------

# 自定义提示符
#function prompt {
#    $p = Split-Path -leaf -path (Get-Location)
#    "<$p>: "
#}

# 设定代理
function set_proxy_variable{
    Set-Item Env:http_proxy "http://127.0.0.1:7890"
    Set-Item Env:https_proxy "http://127.0.0.1:7890"
}

function unset_proxy_variable{
    Remove-Item Env:http_proxy
    Remove-Item Env:https_proxy
}

function echo_proxy_variable{
    echo $Env:http_proxy
    echo $Env:https_proxy
}

function phone{
    adb connect @args
    Start-Job -Name ScreenCopy -ScriptBlock {scrcpy --prefer-text --turn-screen-off --stay-awake}
}


# 别名代理
New-Alias -Name spp -Value set_proxy_variable
New-Alias -Name upp -Value unset_proxy_variable
New-Alias -Name epp -Value echo_proxy_variable
New-Alias -Name startJ -Value Start-Job
New-Alias -Name getJ -Value Get-Job
New-Alias -Name stopJ -Value Stop-Job
New-Alias -Name removeJ -Value Remove-Job

spp

# use theme
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/bubblesextra.omp.json" | Invoke-Expression | Invoke-Expression

# with out themes
# oh-my-posh init pwsh | Invoke-Expression | Invoke-Expression

```
