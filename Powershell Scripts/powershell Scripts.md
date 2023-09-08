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
