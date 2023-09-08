### Clean User's Temporary Files
```powershell
# Clean the user's Temp folder
$TempPath = [System.IO.Path]::GetTempPath()

# Check if the Temp folder exists
if (Test-Path -Path $TempPath -PathType Container) {
    try {
        # Delete files in the Temp folder, excluding those currently in use.
        Get-ChildItem -Path $TempPath | ForEach-Object {
            try {
                Remove-Item -Path $_.FullName -Force -ErrorAction Stop
            } catch {
                Write-Host "Skipped: $($_.FullName) - $($_.Exception.Message)"
            }
        }

        Write-Host "Cleanup completed for $($env:USERNAME)."

    } catch {
        Write-Host "Failed to clean the Temp folder: $($_.Exception.Message)"
    }
} else {
    Write-Host "Temp folder not found for $($env:USERNAME)."
}
```
