# Storage Gateway

Create Storage Gateway

**In AWS**

Create File Share and Point to s3 bucket

**Windows**

1. From windows VMpowershell:

`Get-WindowsFeature-name NFS*`

`Install-WindowsFeature-name NFS-Client`

**create mount:**

`cmd`

`mount -onolock11.254.2.245:/gpc-test-bucket Y:`

`remove mount:`

`umountY:`

Linux – not tested yet

