# Errors

<aside class="notice">
    This is just a quick list of HTTP error codes that the API may return.
</aside>

The Kittn API uses the following error codes:

| Error Code | Meaning                                                                                   |
| ---------- | ----------------------------------------------------------------------------------------- |
| 400        | Bad Request -- Your request is invalid.                                                   |
| 401        | Unauthorized -- Your Authorization header is invalid or not present.                      |
| 403        | Forbidden -- Must require specific access.                                                |
| 404        | Not Found -- The requested resource was not found                                         |
| 418        | I'm a teapot.                                                                             |
| 500        | Internal Server Error -- We had a problem with our server. Contact Mark Artishuk          |
| 503        | Service Unavailable -- We're temporarily offline for maintenance. Please try again later. |
