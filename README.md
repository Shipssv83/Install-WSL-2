# Install-WSL-2
PowerShell скрипт, который автоматизирует процесс включения функций для WSL, установки WSL 2 и дистрибутива Linux в Windows:
```powershell
    # PowerShell скрипт для настройки и установки WSL и дистрибутива Linux на Windows

# Включение компонентов WSL и платформы виртуальной машины
Write-Output "Включение компонентов Windows для WSL и виртуальной машины..."
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux -All -NoRestart
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -All -NoRestart

# Перезагрузка компьютера, если требуется
if ($LASTEXITCODE -eq 3010)
{
    Write-Output "Требуется перезагрузка для завершения установки компонентов."
    Read-Host "Нажмите Enter для перезагрузки..."
    Restart-Computer
}

# Скачивание и установка пакета обновления ядра Linux для WSL 2
$kernelUpdateUrl = "https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi"
$kernelUpdatePath = "$env:USERPROFILE\Downloads\wsl_update_x64.msi"

Write-Output "Скачивание пакета обновления ядра Linux для WSL 2..."
Invoke-WebRequest -Uri $kernelUpdateUrl -OutFile $kernelUpdatePath

Write-Output "Установка пакета обновления ядра Linux..."
Start-Process msiexec.exe -ArgumentList "/i", $kernelUpdatePath, "/quiet", "/norestart" -Wait

# Установка WSL 2 как версии по умолчанию
wsl --set-default-version 2

# Установка дистрибутива Linux (Ubuntu) из Microsoft Store
# Убедитесь, что у вас настроен Microsoft Store для скриптов или установите дистрибутив вручную
Write-Output "Установка дистрибутива Ubuntu..."
winget install -e --id Canonical.Ubuntu

Write-Output "Настройка завершена. Теперь вы можете использовать Ubuntu на вашем компьютере с Windows."
```
