# Checking a File's SHA256 Hash in PowerShell
## 1. Open PowerShell:
- Press Win + X, then select Windows PowerShell or Windows Terminal.
- Alternatively, search for PowerShell in the Start menu and open it.

## 2. Navigate to the Directory (if needed):
- Use the cd command to change to the directory containing the file.
    ```bash
    cd C:\Path\To\Your\File
    ```

## 3. Calculate the SHA256 Hash:
- Use the following command, replacing filename.ext with the name of your file:
- Remember to set the correct algorithm
    ```bash
    $fileHash = (Get-FileHash example.txt -Algorithm SHA256).Hash
    ```

## 4. Create a Known Good Hash Variable:
- Use the following command, adding the hash from the website.
    ```bash
    $knownGoodHash = "<place text here>"
    ```

## 5. Compare the Hashes:
- Run the following command to compare the hashes.
    ```bash
    $fileHash -eq $knownGoodHash
    ```

## 6. Clean up the Environment:  
- Run the following commands to remove the vars you created
    ```bash
    Remove-Variable fileHash, knownGoodHash
    ```
    or
    ```bash
    Get-Variable | Remove-Variable -Force
    ```