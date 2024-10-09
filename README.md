# Digital currency exchange

This project is an exchange project, providing users with online virtual currency transactions, market viewing, and automatic buying and selling

Database path /database/yingbt.sql

## Directory structure
api web deployment directory
├─index.php general entry file
├─readme.md readme file
├─application application directory
│ ├─admin backend module responsible for various backend functions and operations
│ ├─common public function directory
│ ├─home frontend module responsible for various user operations and functions
│ ├─mobile mobile terminal module responsible for display and processing when accessed by mobile phone
├─public resource file directory
├─upload upload resource directory
└─thinkphp framework directory
└─run.php performs data synchronization operations (virtual currency withdrawal, recharge and query, real transfer and transaction)

#  Other remarks

Newly created fields need to be commented on

# Database table structure

tw_user_coin User wallet table

tw_coin System currency table

tw_trade_json Transaction chart data (separated by time)

# Front-end API interface

### post based on /ajax/getkey Get API key

Request parameters

Parameter name | Required | Data type | Description | 
---- | ----- | ------ | ----
remarks | Yes | string | Remarks
ip | No | string | Restrict ip

Response result:

Parameter name | Required | Data type | Description | 
---- | ----- | ------ | ----
AccessKey | Yes | string | Key required for API request
SecretKey | Yes | string | Private key
user_id | Yes | int | User id
remarks | Yes | string | Remarks
ip | No | string |  Bind ip

Return example:

{
"remarks": "test",
"ip": "114.25.12.2",
"user_id": "6277",
"AccessKey": "myiyiloxpfr51l7zxxa7jdrz5xy5m2zv",
"SecretKey": "rcc4wzbnxlxxolm57lx90746mp5sf4ti"
}

--------------------------------------------------------

# User API interface

Please be sure to set X-Requested-With: XMLHttpRequest in the Header

The user's API permissions are obtained in the website's Account->API Management. Click Create to get it.

### Important: These two keys are closely related to account security. Do not disclose them to others at any time.

 Signature Method (SignatureMethod) The hash-based protocol for user-calculated signatures, HmacSHA256 is used here

Signature Example:

For example: In the API interface for canceling a delegated order, sign the following parameters, assuming that the Secret Key is: gnlzv781mgzsvkywj6tkhn1ogfeycbuu

AccessKey=wgpthr6mz7uvaf8y5tcwiququh54jbxd&id=3405&time=1538100485

Use the HmacSHA256 algorithm and SecretKey as the secret key to sign the string and perform an md5 digital signature on the signed content. The md5 value obtained is: 618ec861b1c3ff9a2fb2a9aec1ab7522

The final combined request parameters are as follows:

 AccessKey=wgpthr6mz7uvaf8y5tcwiququh54jbxd&id=3405&time=1538100485&sign=618ec861b1c3ff9a2fb2a9aec1ab7522

### GET /api/accounts Get user basic information

Request parameters

Parameter name | Required | Data type | Description | 
---- | ----- | ------ | ----
