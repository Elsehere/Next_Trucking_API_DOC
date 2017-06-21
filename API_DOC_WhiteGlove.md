# Next Trucking API for White Glove

TODO

Please noted that the prefix for all API is /whiteglove

## Lastest Orders [/latestorders]

### List All Order Snapshots for the Last 24 Hours [/latestorders?timeframe=24][GET]

TODO

+ Request 

    + Parameters
    
      + timeframe  
        Timeframe means the period for the latest orders.  
        Now this API only supports the last 24/48/96 hours for timeframe.

    + Headers

            ACCESS_KEY_ID: XXXXXXXX
            SECRET_KEY: YYYYYYYYYYYYYYYYYYYYYYYY
        
+ Response 200 (application/json)
    + id [String]  
        The unique ID of Next Trucking order.

    + canceled [Boolean]  
        True: Normal order  
        False: Canceled order

    + lastModifiedDate [Long] [UTC]  
        In Next Trucking we always updated lastModifiedDate once the order information was changed.  
        Please always check this field, and call /orders/id API to get the updated order detail information.

            [
                 {
                     "id": "T0000001",
                     "canceled": true,
                     "lastModifiedDate": 1498050097
                 },
                 {
                     "id": "T0000002",
                     "canceled": false,
                     "lastModifiedDate": 1498050097
                 },
                 {
                     "id": "T0000003",
                     "canceled": false,
                     "lastModifiedDate": 1498050097
                 }
             ]
        
+ Response 401

    401 means wrong ACCESS_KEY_ID or SECRET_KEY in request header

+ Response 422 (application/json)
        
    422 means wrong hour in request parameter

        {
            "errorCode": 90001,
            "errorMessage": "Illegal argument for hour, hour should be 24/48/96."
        }

## Order Detail [/orders]

### Get Detail Information of Order by ID [/orders/id][GET]

TODO

+ Request 

    + Parameters

        + id  
            The unique ID of Next Trucking order, such as T0000001.

    + Headers

            ACCESS_KEY_ID: XXXXXXXX
            SECRET_KEY: YYYYYYYYYYYYYYYYYYYYYYYY

+ Response 200 (application/json)
    + id [String]  
        The unique ID of Next Trucking order.
    + pickupAddressName [String]  
        TODO
    + pickupAddress [String]  
        TODO
    + pickupAddressLine [String]  
        TODO
    + pickupAddressLine2 [String]  
        TODO
    + pickupAddressCity [String]  
        TODO
    + pickupAddressState [String]  
        TODO
    + pickupAddressCountry [String]  
        TODO
    + pickupAddressZipcode [String]  
        TODO
    + deliveryAddressName [String]  
        TODO
    + deliveryAddress [String]  
        TODO
    + deliveryAddressLine [String]  
        TODO
    + deliveryAddressLine2 [String]  
        TODO
    + deliveryAddressCity [String]  
        TODO
    + deliveryAddressState [String]  
        TODO
    + deliveryAddressCountry [String]  
        TODO
    + deliveryAddressZipcode [String]  
        TODO  
    + pickupWindowStart [Long][UTC]  
        TODO  
    + pickupWindowEnd [Long][UTC]  
        TODO  
    + deliveryWindowStart [Long][UTC]  
        TODO  
    + deliveryWindowEnd [Long][UTC]  
        TODO  
    + referenceNumbers [Array][String]  
        TODO  
    + purchaseOrderNumber [String]  
        TODO  
    + sealNumber [String]  
        TODO  
    + trailerType [String]  
        TODO  
    + value [Double]  
        TODO  
    + weight [Integer]  
        TODO  
    + commodity [String]  
        TODO  
    + shipperNotes [String]  
        TODO  
    + nmfcClass [String]
        TODO
    + packageType [String]
        Valid values: "BOX"
    + totalPackages [Integer]
        TODO
    + pieceType [String]
        Valid values: "PLT"
    + totalPieces [Integer]
        TODO
    
             {
                "id": "",
                "pickupAddressName": "",
                "pickupAddress": "",
                "pickupAddressLine": "",
                "pickupAddressLine2": "",
                "pickupAddressCity": "",
                "pickupAddressState": "",
                "pickupAddressCountry": "",
                "pickupAddressZipcode": "",
                "deliveryAddressName": "",
                "deliveryAddress": "",
                "deliveryAddressLine": "",
                "deliveryAddressLine2": "",
                "deliveryAddressCity": "",
                "deliveryAddressState": "",
                "deliveryAddressCountry": "",
                "deliveryAddressZipcode": "",
                "pickupWindowStart": "",
                "pickupWindowEnd": "",
                "deliveryWindowStart": "",
                "deliveryWindowEnd": "",
                "referenceNumbers": "",
                "purchaseOrderNumber": "",
                "sealNumber": "",
                "trailerType": "",
                "value": "",
                "weight": "",
                "commodity": "",
                "shipperNotes": ""
            }
        
+ Response 401

    401 means wrong ACCESS_KEY_ID or SECRET_KEY in request header

+ Response 422 (application/json)
        
    422 means wrong id in request parameter.

        {
            "errorCode": 90002,
            "errorMessage": "Illegal argument for id, the id does not belong to you."
        }


## Status Report [/status]

### Report status of order [/status][PUT]

TODO

+ Request (application/json)

    + Headers

            ACCESS_KEY_ID: XXXXXXXX
            SECRET_KEY: YYYYYYYYYYYYYYYYYYYYYYYY

    + Body
    
        + id [String]  
            The unique ID of Next Trucking order.

        + status [String]  
            The status we accept are listed below:
            - pending
            - enroute
            - picked_up

                    {
                        "id": "T0000001",
                        "status":""
                    }

+ Response 200 
    
    200 means this status of order was accepted by Next Trucking.
        
+ Response 401

    401 means wrong ACCESS_KEY_ID or SECRET_KEY in request header

+ Response 422 (application/json) [90002]
        
    422 & 90002 means wrong id in request.

        {
            "errorCode": 90002,
            "errorMessage": "Illegal argument for id, the id does not belong to you."
        }

+ Response 422 (application/json) [90003]
        
    422 & 90003 means wrong status in request.

        {
            "errorCode": 90003,
            "errorMessage": "Illegal argument for status, the status is incorrect."
        }
