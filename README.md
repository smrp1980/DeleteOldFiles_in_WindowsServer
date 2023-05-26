# DeleteOldFiles_in_WindowsServer
# A PowerShell script that can be used to delete old files in a folder on a Windows Server:
# Here's how you can use this script:

# Open a text editor such as Notepad and paste the above script into a new file.
# Modify the $folderPath variable to specify the path of the folder where you want to delete old files.
# Modify the $ageLimit variable to specify the age limit in days. Files older than this limit will be deleted.
# Save the file with a .ps1 extension (e.g., delete_old_files.ps1).
# To execute the script:

# Open PowerShell.
# Navigate to the directory where you saved the script using the cd command.
# Run the script by entering its name: .\delete_old_files.ps1.
# The script will start deleting files older than the specified age limit and display a message for each file deleted.
# Please exercise caution when deleting files, as this script permanently removes them from the specified folder. Make sure to test the script on a non-production environment or create backups before running it on critical data.

#----------------------------------------------------#
STERT BODY:
#----------------------------------------------------#

# Set the folder path and age limit for files (in days)
$folderPath = "C:\Path\to\Your\Folder"
$ageLimit = 30

# Get the current date
$currentDate = Get-Date

# Get all files in the specified folder
$files = Get-ChildItem -Path $folderPath -File

# Iterate through each file
foreach ($file in $files) {
    # Calculate the age of the file
    $fileAge = $currentDate - $file.LastWriteTime

    # Check if the file is older than the age limit
    if ($fileAge.Days -gt $ageLimit) {
        # Delete the file
        Remove-Item -Path $file.FullName -Force
        Write-Host "Deleted file: $($file.FullName)"
    }
}
