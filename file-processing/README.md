## File Processing

The implementation helps to process binary file in different integration aspects. So far, it contains following use cases:

- UC 1: Download binary file via REST API and store it into local preconfigured difrectoy
- UC 2: Download binary file via REST API and store it into SFTP server
- UC 3: Download binary file via REST API and store it into Object Storage
- UC 4: Upload binary file from local storage to SFTP server

Below is the detail instruction for each scenario

## Prerequisites

- Download Micro Integrator 4.2.0 and extract into directory named `{MI_HOME}`

## Use cases
### UC 4: Upload binary file from local storage to SFTP server
The integration will _scan a local directory_ for any PDF files, _upload those files to SFTP server_ and finally _move the upload files_ to local archived folder

__Configure Local File Storage__

Go to `{MI_HOME}/repository/deployment/server/synapse-configs/default/local-entries` and create following local-entry `LOCAL_FILE_DIR.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<localEntry key="LOCAL_FILE_DIR" xmlns="http://ws.apache.org/ns/synapse">
    <file.init>
        <name>LOCAL_FILE_DIR</name>
        <workingDir>C:</workingDir>
        <fileLockScheme>Local</fileLockScheme>
        <connectionType>LOCAL</connectionType>
    </file.init>
</localEntry>
```
> Note: Do NOT enclose above local registy entries in the `Composite Exporter` application because they need to be changed for different deployment scenarios. We tested the local entry to read the configuration from `file.properties`, it simply does not work.

__Configure SFTP__

Similarly, you need to create an local-entry `SFTP_SERVER.xml` at the same directory
```xml
<?xml version="1.0" encoding="UTF-8"?>
<localEntry key="SFTP_SERVER" xmlns="http://ws.apache.org/ns/synapse">
    <file.init>
        <name>SFTP_SERVER</name>
        <workingDir>/</workingDir>
        <fileLockScheme>Local</fileLockScheme>
        <connectionType>SFTP</connectionType>
        <host>mysftp.com</host>
        <port>2309</port>
        <username>username</username>
        <password>password</password>
        <userDirectoryIsRoot>false</userDirectoryIsRoot>
    </file.init>
</localEntry>
```
__Deploy Composite Exporter Application__

Right click on project `file-processing-local-to-sftp-composite-exporter` > `Export Composite Application Project` to export it to `{MI_HOME}/repository/deployment/server/carbonapps`. Wait for the MI deploy the necessary artifacts sucessfully.

__Trigger API__

Call API to `FileAPI` at resource `/uploadSftp` which is composed in `file-processing/file-processing-configs/src/main/resources/metadata/FileAPI_swagger.yaml`. The example and detailed description is mentioned in the API specification.
