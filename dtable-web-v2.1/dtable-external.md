# Base External Link

## Download A Base Through its External Link

Use this request to download a base through its external link.


**URL Structure**

> **\[GET]** dtable/external-links/<token>/download-zip/


**Request Authentication**

None.



**Sample Request**

Download the base through the external link with the token `8720e55e17a44aa89990`:

> ```
> curl GET \
> https://cloud.seatable.io/dtable/external-links/8720e55e17a44aa89990/download-zip/
> ```


**Input Parameters**

**token** _\[string, required]_
> As an external link is generated, its token is used as the suffix to its link. For example: https\://cloud.seatable.io/dtable/external-links/`<token>`/



**Return Values**

.dtable file.


**Sample Response (200)**

A .dtable zip file is downloaded.


**Possible Errors**

404 Not Found: The external link token is not valid:
> ```
> Sorry, but the requested page could not be found.
> ```