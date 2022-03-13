
Spec: https://www.jsonrpc.org/specification


### Request format

(in js for readability, but MUST be 100% standard JSON, no comments)

_To be sent to the service_
```js
{
    // REQUIRED and must be exactly "2.0"
    jsonrpc: "2.0", 

    // REQUIRED (make sure to follow a good normative scheme)
    method: "someMethodName", 

    // Optional, should be present and fully specified 99.9% of the time
    params: {...}, 

    // REQUIRED (can be set to null). Can be number, but string/uuid us a good normative approach
    id: "some_client_id_per_request", 
}
```

> Note - The `id` is just a client identifier, and the server should not do anything with it but return it with the corresponding response. This is to allow the client to keep track of the responses in the event they are batch.


### Response format

(in js for readability, but will be returned in standard JSON)

_Returned by the service_
```js
{
    // REQUIRED and must be exactly "2.0"
    jsonrpc: "2.0", 

    // REQUIRED if success. MUST NOT exists if error. 
    // Can be array but the normative approach will be to have it object only.
    result: {...}, 

    error: {
        // REQUIRED Must be an integer (required)
        code: number, 

        // (Optional) String for SHORT description 
        // (can be enum style, like ACCESS_FAILED_NO_PRIVILEGE)
        message: string,

        // (optional) Service/Method dependent extra information
        data: {}
    }

    // REQUIRED (will match the corresponding json-rpc request)
    id: "some_client_id_per_request", 
}
```

