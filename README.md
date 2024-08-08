# Containerized-R-Template

This is a sample project that shows how to setup an R environment within a container.

## Proxy Servers

### Intermediate Certificates

If your proxy server uses an intermediate certificate, it is necessary to copy the certificate file into the container and make it available via an environment variable. 

This is a four step process:

1. Export intermediate certificate from host system
2. Copy the certificate to the container in the Dockerfile and update certificate chain
3. Add environment variable(s)
4. Rebuild the container

#### Exporting Intermediate Certificate

Obtain the certificate file form the host system. This must be a .crt file. Windows will export a .cer by default. 

1. Export certificate from Certificate Manager as a Base64 Encoded .cer file
2. Rename the file from .cer to .crt
3. Verify contents of certificate file, should have the ----Begin/End Certificate--- markers
4. Copy the certificate file to the .devcontainer file, or other known directory. In this example the files are located in .devcontainer/certs

#### Updating Dockerfile

The Docker file should be updated to perform three actions:

1. Copy the certificate file to the appropriate container folder (this is Linux)
2. Set an environment variable for the container
3. Update the container certificate chain. 

Add the following to your Dockerfile:

```[docker]
COPY certs/. /usr/local/share/ca-certificates/
ENV NODE_EXTRA_CA_CERTS=/usr/local/share/ca-certificates/YOURCERTIFICATE.crt
RUN update-ca-certificates
```

#### Updating devcontainer.json

While the environment variable above is added for use in the container, vscode needs the enviornment set in order to install extensions.

Add the following to devcontainer.json:

```[json]
"remoteEnv": {
		"NODE_EXTRA_CA_CERTS": "/usr/local/share/ca-certificates/YOURCERTIFICATE.crt"
  }
```