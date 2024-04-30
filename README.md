# bin
Binary applications used for internal distribution. Most will require being within the internal network to actually work.

## caniuse
Checks if an IP address is in use. Since it pings an internal server that is hard wired to the network it allows you to detect an ip address is in use even if it doesnt have a gateway assigned.

**Installation:** 

Copy the following script and paste into an administrator powershell then press `enter`.
```shell
# Define the URL and destination path
$url = "https://github.com/Avanzar-PC/bin/raw/main/caniuse.exe"
$destination = "C:\Program Files\caniuse\caniuse.exe"

# Create the directory if it does not exist
$destinationDirectory = Split-Path -Path $destination -Parent
if (-not (Test-Path -Path $destinationDirectory)) {
    New-Item -ItemType Directory -Path $destinationDirectory -Force
}

# Download the file
Invoke-WebRequest -Uri $url -OutFile $destination

# Add the destination directory to the system PATH if it is not already included
$path = [System.Environment]::GetEnvironmentVariable("PATH", "Machine")
if (-not $path.Split(';').Contains($destinationDirectory)) {
    $newPath = $path + ";" + $destinationDirectory
    [System.Environment]::SetEnvironmentVariable("PATH", $newPath, "Machine")
}

# Output success message
Write-Output "caniuse.exe downloaded and path updated successfully."
```

**Usage:**
You should now be able to use the executable you can test it by running:
```shell
caniuse -V
```
