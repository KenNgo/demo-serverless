
# PLM RFQ Service

## Preparation: 

Installations these apps below: <br>

- [Install Visual Studio Code from https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2019](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2019)
- [Install Sourcetree from https://www.sourcetreeapp.com](https://www.sourcetreeapp.com)
- [Install git from https://git-scm.com/download/win](https://git-scm.com/download/win)
- [Install yarn from https://yarnpkg.com/lang/en/docs/install](https://yarnpkg.com/lang/en/docs/install)

## Code Checkout: 
Before checkout source code, we should install global serverless framework:
```sh
    npm install -g serverless
    or
    yarn global add serverless
```
Git clone from: https://bitbucket.org/lifungdigitalservicegroup/plm-rfq-service/ <br>
Navigate to root folder of project and then run commands: <br>
```sh
    yarn install
```
Add a .env file in root folder of the project and copy the below environment variables (please check with the team for the values)<br>
```sh
    WORKATO_ENDPOINT=******
    WORKATO_API_TOKEN=******
    CLIENT_AUDIENCE=******
    TOKEN_ISSUER=******
    JWKS_URI=******
    TF_VAR_aws_account_number=******
```
Example: 
```sh
    WORKATO_ENDPOINT=https://apim.workato.com/plm-dev-v0-0-1/plm/v1/quotedetailtest
    WORKATO_API_TOKEN=e58c56421b97e25fdd88503c487d116828c86bcb119e3655f67cc689d4445134
    AWS_XRAY_CONTEXT_MISSING=LOG_ERROR
    CLIENT_AUDIENCE=https://dev.lfdsg.com/api/plm
    TOKEN_ISSUER=https://dev-lfdsg.auth0.com/
    JWKS_URI=https://dev-lfdsg.auth0.com/.well-known/jwks.json
    TF_VAR_service_env=Dev
    TF_VAR_aws_account_number=298498000182
```
Start AWS Lambda using below command, it will startup on port 3000 :
```sh
    yarn aws:start
```
