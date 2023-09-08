### Clean User's Temporary Files
```powershell
# Clean the user's Temp folder
$TempPath = [System.IO.Path]::GetTempPath()

# Check if the Temp folder exists
if (Test-Path -Path $TempPath -PathType Container) {
    try {
        # Get a list of files to be deleted (excluding those currently in use)
        $FilesToDelete = Get-ChildItem -Path $TempPath -File | Where-Object { !$_.IsReadOnly }

        # Delete files in the Temp folder
        foreach ($File in $FilesToDelete) {
            try {
                Remove-Item -Path $File.FullName -Force -ErrorAction Stop
            } catch {
                # If an error occurs (e.g., file in use), silently skip the file
                continue
            }
        }

        # Optionally, you can display a message indicating cleanup completion
        # Write-Host "Cleanup completed for $($env:USERNAME)."

    } catch {
        # Silently handle any unexpected errors
    }
}
```

### Performance Optimization and Cleanup Script
```powershell
# Disable Windows Search service
Set-Service -Name "wsearch" -StartupType Disabled

# Disable Superfetch service
Set-Service -Name "sysmain" -StartupType Disabled

# Clear Windows Temp folder
Remove-Item -Path "$env:TEMP\*" -Force -Recurse

# Clear Internet Explorer cache
RunDll32.exe InetCpl.cpl,ClearMyTracksByProcess 255

# Specify the correct registry path for user-specific startup programs
$RegistryPath = "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run"

# Get a list of startup items
$StartupItems = Get-ItemProperty -Path $RegistryPath

# Define a list of startup items to keep (Windows Defender and OneDrive)
$ItemsToKeep = @("WindowsDefender", "OneDrive")

# Remove unnecessary startup items
foreach ($Item in $StartupItems.PSObject.Properties) {
    $Name = $Item.Name
    if ($ItemsToKeep -notcontains $Name) {
        Remove-ItemProperty -Path $RegistryPath -Name $Name -ErrorAction SilentlyContinue
    }
}

# Optimize Windows for best performance
Set-ItemProperty -Path "HKCU:\Control Panel\Desktop" -Name UserPreferencesMask -Value 90

# Restart the computer to apply changes (optional)
# Restart-Computer -Force
```
# Description:
This PowerShell script is designed to enhance the performance of your Windows computer by disabling resource-intensive services, clearing temporary files, and optimizing startup programs. It provides the following functionalities:

    Disables the Windows Search service to reduce background indexing.
    Disables the Superfetch service to free up system resources.
    Clears the Windows Temp folder to reclaim disk space.
    Clears the Internet Explorer cache for improved browsing performance.
    Removes unnecessary startup items from the user's registry, keeping essential programs like Windows Defender and OneDrive.
    Optimizes Windows visual effects settings for smoother performance (optional).
    Offers an option to restart the computer to apply changes (optional).
