# CSV_Dicer
Converts Large CSV files to smaller more manageable excel/csv files



Function Get-FileName($initialDirectory)
{   

     [System.Reflection.Assembly]::LoadWithPartialName("System.windows.forms") | Out-Null
     $OpenFileDialog = New-Object System.Windows.Forms.OpenFileDialog
     $OpenFileDialog.initialDirectory = $initialDirectory
     $OpenFileDialog.filter = "All files (*.*)| *.*"
     $OpenFileDialog.ShowDialog() | Out-Null
     $OpenFileDialog.filename
     $OpenFileDialog.ShowHelp = $true

} #end function Get-FileName

$file = Get-FileName -initialDirectory "c:fso"

Function Get-Folder($initialDirectory)

{
    [System.Reflection.Assembly]::Assembly.Load("System.windows.forms")

    $foldername = New-Object System.Windows.Forms.FolderBrowserDialog
    $foldername.rootfolder = "Desktop"

    if($foldername.ShowDialog() -eq "OK")
    {
        $folder += $foldername.SelectedPath
    }
    return $folder
}

 
$i=0;


$a = Get-Folder
$b = '\splitfile_'
$c = '.csv'
$d ="$a$b"

# [System.Windows.MessageBox]::Show("$d") #Uncomment to check if directory path is in fact equal to the directory you chose in the folder dialog

Get-Content $file -ReadCount 75000 | %{$i++; $_ | Out-File "$d$i$c"};
