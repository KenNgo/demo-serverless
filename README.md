# PLM RFQ Service

## Preparation: 

Installations these apps below: <br>

- [Install Visual Studio Code from https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2019](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio?view=vs-2019)
- [Install Sourcetree from https://www.sourcetreeapp.com](https://www.sourcetreeapp.com)
- [Install git from https://git-scm.com/download/win](https://git-scm.com/download/win)
- [Install yarn from https://yarnpkg.com/lang/en/docs/install](https://yarnpkg.com/lang/en/docs/install)
- [Install insomnia app or postman latest version (version support GraphQL) https://insomnia.rest/download/](https://insomnia.rest/download/)

## Code Checkout: 
Before checkout source code, we should install global serverless framework:
```sh
    npm install -g serverless
    or
    yarn global add serverless
```
Git clone project: git clone https://bitbucket.org/lifungdigitalservicegroup/plm-rfq-service/ <br>

## Setup working environment:

Navigate to root folder of project and then run commands: <br>
```sh
    yarn install
```
Then add a .env file in root folder of the project and copy the below environment variables (please check with the team for the values)<br>
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
To get access token, open insomnia tool or postman tool, and try with these info in POST body:
```sh
    POST https://dev-lfdsg.auth0.com/oauth/token
    Body (JSON)
    {
        "client_id": "oDlnjEpa6MknEZgqPwBjNmWSPDJ459zB",
        "client_secret": "xrwps8AQQxJk_uelDZR_WE464ZSLT2BbTtsXn8NIAu9LklM0yoo1iB9JP_zV3rzl",
        "audience": "https://dev.lfdsg.com/api/plm",
        "grant_type": "client_credentials"
    }
```
Then: <br>
Start AWS Lambda using below command, it will start on port 3000 :
```sh
    yarn aws:start
```
Get x-api-key in terminal: ******************* <br>
Then open insomnia tool again, and try with these info below in Header Tab:
```sh
    POST http://localhost:3000/graphql
    Authorization   Bearer ****_your_access_token_*******
    x-api-key       *****_your_x-api-key_********
    Content-Type    application/json
```
In GraphQL tab, try this in Schema and Query variables fields:
```sh
    ---- Schema
    mutation($requestForQuotationInput:RequestForQuotationInput!){
        requestForQuotation(rfqDocument:$requestForQuotationInput){
            code
            success
            message
        }
    }
    ---- Query variables
    {
	"requestForQuotationInput": {
		"recordCount": 1,
		"quoteList": [
			{
				"requestNo": "00350561",
				"styleNo": "WT71A402EN",
				"styleDescription": "WEEKEND STRAIGHT CAPRI",
				"styleStatus": "ADOPTED",
				"merchCode": "",
				"merchDescription": "",
				"season": "SP17",
				"productManagerId": "",
				"productManagerName": "MICHELLE VANDERMEER",
				"brand": "TEKGEAR",
				"division": "WOMENS",
				"customerCode": "WOMENS",
				"customerName": "WOMENS",
				"commodity": "APPAREL",
				"designerId": "",
				"designerName": "ERIN AUBREY",
				"productCoordinatorId": "",
				"productCoordinatorName": "LINDSAY BYE",
				"associateProductManagerId": "",
				"associateProductManagerName": "JENNIFER NORLAND",
				"productSpecialistId": "",
				"productSpecialistName": "MEG DELANEY",
				"classCatgOneProgram": "CROFT & BARROW",
				"classCatgTwoProgram": "DRESS SHIRTS",
				"productType": "",
				"qualityTier": 0,
				"buyProgram": "",
				"buyProgramDesc": "",
				"baseRequestNo": "00367269",
				"freightType": "STANDARD",
				"downtime": "N",
				"ecomExcl": "N",
				"testStyle": "N",
				"charity": "N",
				"hangingFtwr": "N",
				"styleDevHandoffDt": "",
				"techDesignerId": "",
				"techDesignerName": "PAMELA SAVING",
				"createTs": "06/09/2016 09:24:00",
				"createUserId": "",
				"modifyTs": "09/21/2016 08:55:47",
				"modifyUserId": "",
				"modifyUserName": "JENNIFER DOBRINSKA",
				"sizeRange": "WOMENS BOTTOMS (14)",
				"imageList": [
					{
						"mainImageFilename": "TERFQIMG_00350561.jpg"
					}
				],
				"colorList": [
					{
						"colorInfoName": "NAVY SEAL - POLY",
						"colorInfoColorway": "NASE/BLK",
						"colorInfoNrfCode": "400",
						"colorInfoType": "COLOR",
						"colorInfoArtworkId": 0,
						"colorInfoArtworkColorwayId": 0,
						"colorInfoColorId": "21877",
						"colorServiceName": "CSI",
						"colorServiceNo": "205-6840",
						"colorStatus": "COLOR",
						"devChoiceSuffix": "",
						"month": "",
						"meetingNeeds": ""
					},
					{
						"colorInfoName": "CAPITAL GREY",
						"colorInfoColorway": "CGRY M",
						"colorInfoNrfCode": "021",
						"colorInfoType": "COLOR",
						"colorInfoArtworkId": 0,
						"colorInfoArtworkColorwayId": 0,
						"colorInfoColorId": "15005",
						"colorServiceName": "CSI",
						"colorServiceNo": "211-2004",
						"colorStatus": "COLOR",
						"devChoiceSuffix": "",
						"month": "",
						"meetingNeeds": ""
					},
					{
						"colorInfoName": "NAVY ROMANCE - POLY",
						"colorInfoColorway": "NARO/BLK",
						"colorInfoNrfCode": "401",
						"colorInfoType": "COLOR",
						"colorInfoArtworkId": 0,
						"colorInfoArtworkColorwayId": 0,
						"colorInfoColorId": "9491",
						"colorServiceName": "ARCHROMA",
						"colorServiceNo": "AP1715269",
						"colorStatus": "COLOR",
						"devChoiceSuffix": "",
						"month": "",
						"meetingNeeds": ""
					},
					{
						"colorInfoName": "PHANTOM",
						"colorInfoColorway": "PHANTOM",
						"colorInfoNrfCode": "020",
						"colorInfoType": "",
						"colorInfoArtworkId": 0,
						"colorInfoArtworkColorwayId": 0,
						"colorInfoColorId": "1405",
						"colorServiceName": "PANTONE",
						"colorServiceNo": "19-4205 TCX",
						"colorStatus": "COLOR",
						"devChoiceSuffix": "",
						"month": "",
						"meetingNeeds": ""
					},
					{
						"colorInfoName": "SAGE HERB",
						"colorInfoColorway": "SAGE HERB",
						"colorInfoNrfCode": "330",
						"colorInfoType": "",
						"colorInfoArtworkId": 0,
						"colorInfoArtworkColorwayId": 0,
						"colorInfoColorId": "12664",
						"colorServiceName": "CSI",
						"colorServiceNo": "211-768",
						"colorStatus": "COLOR",
						"devChoiceSuffix": "",
						"month": "",
						"meetingNeeds": ""
					},
					{
						"colorInfoName": "ASPHALT",
						"colorInfoColorway": "ASPHLT",
						"colorInfoNrfCode": "010",
						"colorInfoType": "COLOR",
						"colorInfoArtworkId": 0,
						"colorInfoArtworkColorwayId": 0,
						"colorInfoColorId": "8821",
						"colorServiceName": "PANTONE",
						"colorServiceNo": "19-0201 TCX",
						"colorStatus": "COLOR",
						"devChoiceSuffix": "",
						"month": "",
						"meetingNeeds": ""
					}
				],
				"otbList": [
					{
						"otbMonth": "MAR",
						"otbWeek": "2",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 1752,
						"otbPackCode": ""
					},
					{
						"otbMonth": "MAR",
						"otbWeek": "3",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 6000,
						"otbPackCode": ""
					},
					{
						"otbMonth": "MAR",
						"otbWeek": "4",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 100,
						"otbPackCode": ""
					},
					{
						"otbMonth": "MAR",
						"otbWeek": "5",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 18530,
						"otbPackCode": ""
					},
					{
						"otbMonth": "APR",
						"otbWeek": "1",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 4000,
						"otbPackCode": ""
					},
					{
						"otbMonth": "APR",
						"otbWeek": "2",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 6910,
						"otbPackCode": ""
					},
					{
						"otbMonth": "APR",
						"otbWeek": "3",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 2332,
						"otbPackCode": ""
					},
					{
						"otbMonth": "APR",
						"otbWeek": "4",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 1636,
						"otbPackCode": ""
					},
					{
						"otbMonth": "MAY",
						"otbWeek": "1",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 1168,
						"otbPackCode": ""
					},
					{
						"otbMonth": "MAY",
						"otbWeek": "2",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 11452,
						"otbPackCode": ""
					},
					{
						"otbMonth": "MAY",
						"otbWeek": "3",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 1000,
						"otbPackCode": ""
					},
					{
						"otbMonth": "MAY",
						"otbWeek": "4",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUN",
						"otbWeek": "1",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUN",
						"otbWeek": "2",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 20904,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUN",
						"otbWeek": "3",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 1270,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUN",
						"otbWeek": "4",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUN",
						"otbWeek": "5",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUL",
						"otbWeek": "1",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 4500,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUL",
						"otbWeek": "2",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUL",
						"otbWeek": "3",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUL",
						"otbWeek": "4",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "1",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "2",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 800,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "3",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "4",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "JUL",
						"otbWeek": "4",
						"capacitySeason": "SP17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "1",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "2",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "3",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					},
					{
						"otbMonth": "AUG",
						"otbWeek": "4",
						"capacitySeason": "FA17",
						"startXFactory": "",
						"lastXFactory": "",
						"otbStatus": "O",
						"otbQuantity": 0,
						"otbPackCode": ""
					}
				],
				"quoteBomcList": [
					{
						"qbomcBomName": "KOHLS DESIGN BOM",
						"qbomcBomStatus": "ACTIVE",
						"qbomcOfferNo": ""
					},
					{
						"qbomcBomName": "KOHLS DESIGN BOM",
						"qbomcBomStatus": "ACTIVE",
						"qbomcOfferNo": "1289409"
					},
					{
						"qbomcBomName": "KOHLS DESIGN BOM",
						"qbomcBomStatus": "ACTIVE",
						"qbomcOfferNo": "1284275"
					}
				],
				"offerList": [
					{
						"offerNo": "1289409",
						"offerStatus": "CFM",
						"agentId": "76206",
						"agentName": "LI & FUNG TAIWAN",
						"vendorId": "59685",
						"vendorName": "GREAT GIANT FIBRE GARMENT CO. LTD",
						"idInd": "I",
						"factoryId": "81930",
						"factoryName": "CAO HOA CO., LTD.",
						"qaInsp": "",
						"firstSale": "Y",
						"itemFirstCost": 7.86,
						"estimatedLandedCost": 11.111,
						"imuPercent": 74.748,
						"cop": "VN",
						"fobPort": "SGN",
						"poePort": "LA",
						"transitLeadDays": 37,
						"freightCalcDate": "01/29/2017",
						"cartonCodeFtwr": "",
						"unitsInner": 0,
						"unitsOuter": 0,
						"maxCtnSzDispDim": "",
						"unitsPerCbm": 500,
						"unitsMeas": 0.002,
						"um": "CBM",
						"dutyRate": 0.282,
						"dutyFree": "N",
						"sweaterWt": 0,
						"sweaterWtUm": "",
						"materialForecastUnits": "8022",
						"knitToShape": "",
						"stitchCount": "Horz=   Vert=",
						"vendorItemDescription": "WOMENS 88% POLYESTER 12% SPANDEX KNITTED PANTS (06685)",
						"deliveryTerms": "FOB",
						"opaPartnerFactory": "",
						"opaPartnerFactoryOrgn": "",
						"vendorStyleId": "SC64B01-PC",
						"emailTo": "CBPLXTWNWOMENS@LFSOURCING.COM",
						"emailDate": "09/21/2016",
						"initialCfmDate": "10/05/2016",
						"lfIndicator": "Y",
						"presentationNotes": "Size Strip Details: SS V-Neck",
						"vendorNotes": "Supplier - Product Manager Correspondence (NAME, DATE, NOTE)\n---------------------------------------\nWT71A402ES: FC$6.67/ ELC$9.46\nWT71A402EN: FC$7.86/ ELC$11.11",
						"vendorPreclassificationNotes": "AGENT/VENDOR CLASSIFICATION NOTES\n   (For Multi-Piece Style: Identify Piece Percentages)\n-------------------------------------------------\n",
						"deptNo": "442",
						"deptName": "442 - PETITE BOTTOMS",
						"sourcingType": "KNIT",
						"retailPrice": "44",
						"boxIdFtwr": 0,
						"classificationStatus": "CLASSIFD",
						"brokerDescription": "WOMENS POLYESTER/SPANDEX 88/12 KNIT PANTS",
						"preclassDate": "09/21/2016",
						"classificationDate": "01/04/2017",
						"buyingSizeRange": "",
						"supplierRefNo": "276145.48",
						"devChoiceStyleNo": "",
						"hangFold": "",
						"integratedHangtag": "89132.442",
						"dutyFreeProgram": "",
						"finishedFabricWeight": "",
						"wgtUm": "",
						"hangerCost": 0.13,
						"offerImage": [
							{
								"offerImageFilename": "TEOFRIMGOne358274.JPG"
							}
						],
						"offerBomcList": [
							{
								"offerBomcDetailList": [
									{
										"bomcSection": "MATERIALS",
										"bomcComponentId": 6139,
										"bomcArticleCode": "",
										"bomcComponentName": "K 88/12 POLYESTER/SPANDEX JERSEY 300 GM2",
										"bomcNotes": "PD",
										"bomcType": "KNIT",
										"bomcSubType": "JERSEY",
										"bomcPosition": "",
										"bomcSuppMillId": "M00748",
										"bomcSuppMillName": "JIANGSU XINKAISHENG",
										"bomcSupplierCop": "CN",
										"bomcYieldOrQty": 1.31
									},
									{
										"bomcSection": "PACKAGING",
										"bomcComponentId": 31167,
										"bomcArticleCode": "KH-6012-CG",
										"bomcComponentName": "KH-6012-CG - 12IN. BOTTOM - PINCH GRIP - BLACK ADULT HANGER WITH SIZER",
										"bomcNotes": "",
										"bomcType": "PACKAGING",
										"bomcSubType": "HANGER",
										"bomcPosition": "",
										"bomcSuppMillId": "199177",
										"bomcSuppMillName": "MAINETTI USA",
										"bomcSupplierCop": "VN",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 35297,
										"bomcArticleCode": "20702-TK",
										"bomcComponentName": "20702-TK - DRI TEK INTEGRATED",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 36316,
										"bomcArticleCode": "KOH-UPC",
										"bomcComponentName": "KOH-UPC - GENERIC UPC LABEL",
										"bomcNotes": "",
										"bomcType": "LABEL",
										"bomcSubType": "TRIM LABEL",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 37013,
										"bomcArticleCode": "40580002TG",
										"bomcComponentName": "40580002TG - HEATSEAL",
										"bomcNotes": "",
										"bomcType": "LABEL",
										"bomcSubType": "MAIN LABEL",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 33944,
										"bomcArticleCode": "31888010TG",
										"bomcComponentName": "31888010TG - CAPRI JOKER",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 33944,
										"bomcArticleCode": "31888010TG",
										"bomcComponentName": "31888010TG - CAPRI JOKER",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 39892,
										"bomcArticleCode": "MTPSBHT-A9",
										"bomcComponentName": "MTPSBHT-A9 - MENS TOPS INTEGRATED TAG",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "",
										"bomcSuppMillName": "",
										"bomcSupplierCop": "",
										"bomcYieldOrQty": 0
									}
								]
							}
						],
						"multiHtsList": [
							{
								"multiKohlsHtsNo": "6104632006",
								"multiVendorHtsNo": "",
								"multiHtsDutyRate": 0.282,
								"multiHtsDescription": ""
							}
						]
					},
					{
						"offerNo": "1289409",
						"offerStatus": "CFM",
						"agentId": "76206",
						"agentName": "LI & FUNG TAIWAN",
						"vendorId": "59685",
						"vendorName": "GREAT GIANT FIBRE GARMENT CO. LTD",
						"idInd": "I",
						"factoryId": "81930",
						"factoryName": "CAO HOA CO., LTD.",
						"qaInsp": "",
						"firstSale": "Y",
						"itemFirstCost": 7.86,
						"estimatedLandedCost": 11.111,
						"imuPercent": 74.748,
						"cop": "VN",
						"fobPort": "SGN",
						"poePort": "LA",
						"transitLeadDays": 37,
						"freightCalcDate": "01/29/2017",
						"cartonCodeFtwr": "",
						"unitsInner": 0,
						"unitsOuter": 0,
						"maxCtnSzDispDim": "",
						"unitsPerCbm": 500,
						"unitsMeas": 0.002,
						"um": "CBM",
						"dutyRate": 0.282,
						"dutyFree": "N",
						"sweaterWt": 0,
						"sweaterWtUm": "",
						"materialForecastUnits": "8022",
						"knitToShape": "",
						"stitchCount": "Horz=   Vert=",
						"vendorItemDescription": "WOMENS 88% POLYESTER 12% SPANDEX KNITTED PANTS (06685)",
						"deliveryTerms": "FOB",
						"opaPartnerFactory": "",
						"opaPartnerFactoryOrgn": "",
						"vendorStyleId": "SC64B01-PC",
						"emailTo": "CBPLXTWNWOMENS@LFSOURCING.COM",
						"emailDate": "09/21/2016",
						"initialCfmDate": "10/05/2016",
						"lfIndicator": "Y",
						"presentationNotes": "Size Strip Details: SS V-Neck",
						"vendorNotes": "Supplier - Product Manager Correspondence (NAME, DATE, NOTE)\n---------------------------------------\nWT71A402ES: FC$6.67/ ELC$9.46\nWT71A402EN: FC$7.86/ ELC$11.11",
						"vendorPreclassificationNotes": "AGENT/VENDOR CLASSIFICATION NOTES\n   (For Multi-Piece Style: Identify Piece Percentages)\n-------------------------------------------------\n",
						"deptNo": "442",
						"deptName": "442 - PETITE BOTTOMS",
						"sourcingType": "KNIT",
						"retailPrice": "44",
						"boxIdFtwr": 0,
						"classificationStatus": "CLASSIFD",
						"brokerDescription": "WOMENS POLYESTER/SPANDEX 88/12 KNIT PANTS",
						"preclassDate": "09/21/2016",
						"classificationDate": "01/04/2017",
						"buyingSizeRange": "",
						"supplierRefNo": "276145.48",
						"devChoiceStyleNo": "",
						"hangFold": "",
						"integratedHangtag": "89132.442",
						"dutyFreeProgram": "",
						"finishedFabricWeight": "",
						"wgtUm": "",
						"hangerCost": 0.13,
						"offerImage": [
							{
								"offerImageFilename": "TEOFRIMGOne358274.JPG"
							}
						],
						"offerBomcList": [
							{
								"offerBomcDetailList": [
									{
										"bomcSection": "MATERIALS",
										"bomcComponentId": 6139,
										"bomcArticleCode": "",
										"bomcComponentName": "K 88/12 POLYESTER/SPANDEX JERSEY 300 GM2",
										"bomcNotes": "PD",
										"bomcType": "KNIT",
										"bomcSubType": "JERSEY",
										"bomcPosition": "",
										"bomcSuppMillId": "M00748",
										"bomcSuppMillName": "JIANGSU XINKAISHENG",
										"bomcSupplierCop": "CN",
										"bomcYieldOrQty": 1.31
									},
									{
										"bomcSection": "PACKAGING",
										"bomcComponentId": 31167,
										"bomcArticleCode": "KH-6012-CG",
										"bomcComponentName": "KH-6012-CG - 12IN. BOTTOM - PINCH GRIP - BLACK ADULT HANGER WITH SIZER",
										"bomcNotes": "",
										"bomcType": "PACKAGING",
										"bomcSubType": "HANGER",
										"bomcPosition": "",
										"bomcSuppMillId": "199177",
										"bomcSuppMillName": "MAINETTI USA",
										"bomcSupplierCop": "VN",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 35297,
										"bomcArticleCode": "20702-TK",
										"bomcComponentName": "20702-TK - DRI TEK INTEGRATED",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 36316,
										"bomcArticleCode": "KOH-UPC",
										"bomcComponentName": "KOH-UPC - GENERIC UPC LABEL",
										"bomcNotes": "",
										"bomcType": "LABEL",
										"bomcSubType": "TRIM LABEL",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 37013,
										"bomcArticleCode": "40580002TG",
										"bomcComponentName": "40580002TG - HEATSEAL",
										"bomcNotes": "",
										"bomcType": "LABEL",
										"bomcSubType": "MAIN LABEL",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 33944,
										"bomcArticleCode": "31888010TG",
										"bomcComponentName": "31888010TG - CAPRI JOKER",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 33944,
										"bomcArticleCode": "31888010TG",
										"bomcComponentName": "31888010TG - CAPRI JOKER",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "9425",
										"bomcSuppMillName": "AVERY DENNISON",
										"bomcSupplierCop": "HK",
										"bomcYieldOrQty": 1
									},
									{
										"bomcSection": "LABEL",
										"bomcComponentId": 39892,
										"bomcArticleCode": "MTPSBHT-A9",
										"bomcComponentName": "MTPSBHT-A9 - MENS TOPS INTEGRATED TAG",
										"bomcNotes": "",
										"bomcType": "HANGTAG",
										"bomcSubType": "INTEGRATED",
										"bomcPosition": "",
										"bomcSuppMillId": "",
										"bomcSuppMillName": "",
										"bomcSupplierCop": "",
										"bomcYieldOrQty": 0
									}
								]
							}
						],
						"multiHtsList": [
							{
								"multiKohlsHtsNo": "6104632006",
								"multiVendorHtsNo": "",
								"multiHtsDutyRate": 0.282,
								"multiHtsDescription": ""
							}
						]
					}
				]
			}
		]
	}
}
```
or try with your oneHealthCheck
