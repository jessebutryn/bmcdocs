# CertManage

Facilitates certificate management for the managed system on NVIDIA GB200 systems. Allows users to perform a variety of actions such as retrieving a list of certificates, generating Certificate Signing Requests (CSR), uploading certificates, and deleting specific certificates.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CertManage --action <action>
```

### In-Band
```
saa -c CertManage --action <action>
```

## Actions

- **GetCertList**: Retrieves a list of all certificates available on the system, categorized by usage (HTTPS, LDAP, Truststore).
- **GenerateCSR**: Generates a Certificate Signing Request (CSR) token and writes it to a `.csr` file, using certificate details supplied in a config file.
- **UploadCert**: Uploads a certificate (in PEM format) to the system for a specific certificate type.
- **DeleteCert**: Deletes a specific certificate from the system by type and certificate ID.

## Options

- `--action <action>`: Sets the action to perform. One of `GetCertList`, `GenerateCSR`, `UploadCert`, or `DeleteCert`.
- `--cfg_file <filename>`: Configuration file (JSON) containing the certificate details used to generate a CSR (`GenerateCSR` action).
- `--file <filename>`: Output file for the generated CSR token (`GenerateCSR` action), or the certificate file to upload (`UploadCert` action).
- `--type <type>`: Certificate type, e.g. `LDAP` (`UploadCert` and `DeleteCert` actions).
- `--certid <id>`: ID of the certificate to delete (`DeleteCert` action).

## Examples

### Retrieve Certificate List

```bash
# OOB
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CertManage --action GetCertlist

# In-Band
[SAA_HOME]# ./saa -c CertManage --action GetCertlist
```

### Generate CSR Token

The content of the `config.json` file should be as below for generating a CSR token:

```json
{
 "City": "San Francisco",
 "CertificateCollection": {
 "@odata.id": "/redfish/v1/Managers/BMC_0/NetworkProtocol/HTTPS/Certificates/1"
 },
 "CommonName": "SMCI",
 "Country": "US",
 "Organization": "SuperMicro",
 "OrganizationalUnit": "Server",
 "State": "SanJose",
 "KeyPairAlgorithm": "EC"
}
```

```bash
# OOB
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CertManage --action GenerateCSR --cfg_file config.json --file out.csr

# In-Band
[SAA_HOME]# ./saa -c CertManage --action GenerateCSR --cfg_file config.json --file out.csr
```

The config file supplies certificate details such as City, Common Name, Organization, and Key Pair Algorithm.

### Upload Certificate

The system accepts certificates in PEM format for uploading or replacing. You can use OpenSSL to generate the PEM file from the CSR created via `GenerateCSR`:

```bash
# Generate a private key (2048-bit)
openssl genrsa -out private.key 2048

# Generate the certificate using the CSR
openssl x509 -req -days 365 -in request.csr -signkey private.key -out certificate.crt

# Combine the private key and certificate into a PEM file
cat private.key certificate.crt > certificate.pem
```

```bash
# OOB
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CertManage --action UploadCert --type LDAP --file certificate.pem

# In-Band
[SAA_HOME]# ./saa -c CertManage --action UploadCert --type LDAP --file certificate.pem
```

### Delete Certificate

```bash
# OOB
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CertManage --action DeleteCert --type LDAP --certid 14

# In-Band
[SAA_HOME]# ./saa -c CertManage --action DeleteCert --type LDAP --certid 14
```

## Output

### Retrieve Certificate List
```
Certificate List:
[
 "/redfish/v1/Managers/BMC_0/Truststore/Certificates/7",
 "/redfish/v1/AccountService/LDAP/Certificates/15",
 "/redfish/v1/Managers/BMC_0/NetworkProtocol/HTTPS/Certificates/1"
]
```

### Generate CSR Token
```
Successfully generated the CSR token and wrote it to the out.csr Certificate to System.
```

### Upload Certificate
```
Successfully uploaded the LDAP Certificate to System.
```

### Delete Certificate
```
Successfully deleted the certificate of type LDAP with ID 14 from the system.
```

## Notes

- `GetCertList` output contains the URLs of certificates categorized by usage: HTTPS Certificates (secure web communication), LDAP Certificates (LDAP authentication), and Truststore Certificates (validating external entities).
- `GenerateCSR` requires a `config.json` file describing the certificate details (City, Common Name, Organization, Organizational Unit, Country, State, Key Pair Algorithm, and the target certificate collection).
- `UploadCert` and `DeleteCert` both require the `--type` option (e.g. `LDAP`) to identify the certificate category being managed.
