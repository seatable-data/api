# Temporary API token

## Get a temporary base API token

**GET** api/v2.1/workspace/:workspace_id/dtable/:name/temp-api-token/

**Sample Request**

```
curl --request GET 'https://cloud.seatable.io/api/v2.1/workspace/107/dtable/for-add/temp-api-token/' --header 'Authorization: Token 64b9ee55dc4ab902ff36763ef5c604a76d52875e'

```

**Sample Response**

```
{
    "api_token": "ed3dc97a6c4fcadc6ba9561b0839ed9b5c25b644"
}

```

**Note: **Get a download link by API token, please view [Get file download link by API token](https://docs.seatable.io/published/seatable-api/dtable-web-v2.1/dtable-api-token.md#user-content-Get%20File%20Download%20Link%20by%20API%20Token)
