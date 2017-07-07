# Next Trucking API for White Glove

Next Trucking will send you ACCESS_KEY_ID and SECRET_KEY once you need to intergate with Next Trucking API.  
- ACCESS_KEY_ID is a 8 characters random string.
- SECRET_KEY is a 16 characters random sting.

DO NOT share this pair with others.

Please noted that the prefix for all API is /api/whiteglove

## Lastest Orders [/latestorders]

### List All Order Snapshots for the Last 24 Hours [/latestorders?timeframe=24][GET]

All the order of whiteglove could be accessed via this interface.
- If you got an order with cancelled:False, this means a new/updated order, you should process this save or update logic in your code.
  - If this order already existed in your system, please update this order in your system.
  - If this order does not exist in your system, please create an new order.

- If you got an order with cancelled:True, this means a cancelled order.
  - If this cancelled order already existed in your system, please cancel it.
  - If this cancelled order does not exist in your system, please ignore it.

+ Request 

    + Parameters
    
      + timeframe  
        Timeframe means the period for the latest orders.  
        Now this API only supports the last 24/48/96 hours for timeframe.

    + Headers

            ACCESS_KEY_ID: XXXXXXXX
            SECRET_KEY: YYYYYYYYYYYYYYYY
        
+ Response 200 (application/json)
    + id [String]  
        The unique ID of Next Trucking order.
        
    + cancelled [Boolean]  
        True: Normal order  
        False: Cancelled order  
        
    + lastModifiedDate [Long] [UTC]  
        In Next Trucking we always updated lastModifiedDate once the order information was changed.  
        Please always check this field, and call /orders/id API to get the updated order detail information.

            [
                {
                    "id": "T0000001",
                    "cancelled": true,
                    "lastModifiedDate": 1498050097
                }, 
                {
                    "id": "T0000002",
                    "cancelled": false,
                    "lastModifiedDate": 1498050097
                }, 
                {
                    "id": "T0000003",
                    "cancelled": false,
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

The detail information of order could be accessed via this interface.

+ Request 

    + Parameters

        + id  
            The unique ID of Next Trucking order, such as T0000001.

    + Headers

            ACCESS_KEY_ID: XXXXXXXX
            SECRET_KEY: YYYYYYYYYYYYYYYY

+ Response 200 (application/json)
    + id [String]  
        The unique ID of Next Trucking order.
    + pickupAddressName [String]  
        The name of pickup location address.
    + pickupAddressLine [String]  
        The first line of pickup location address, such as street and number.
    + pickupAddressLine2 [String]  
        The second line of pickup location address, such as apartment, suite, unit, building, floor, etc.
    + pickupAddressCity [String]  
        The city of pickup location address.
    + pickupAddressState [String]  
        The state of pickup location address, please use abbreviation such as CA for California, AZ for Arizona etc.
    + pickupAddressCountry [String]  
        The country of pickup location address, such as United State, Canada.
    + pickupAddressZipcode [String]  
        The zipcode of pickup location address.
    + deliveryAddressName [String]  
        The name of pickup location address.
    + deliveryAddressLine [String]  
        The first line of pickup location address, such as street and number.
    + deliveryAddressLine2 [String]  
        The second line of pickup location address, such as apartment, suite, unit, building, floor, etc.
    + deliveryAddressCity [String]  
        The city of pickup location address.
    + deliveryAddressState [String]  
        The state of pickup location address, please use abbreviation such as CA for California, AZ for Arizona etc.
    + deliveryAddressCountry [String]  
        The country of pickup location address, such as United State, Canada.
    + deliveryAddressZipcode [String]  
        The zipcode of pickup location address.  
    + pickupWindowStart [Long][UTC]  
        The start time of pickup window.  
    + pickupWindowEnd [Long][UTC]  
        The end time of pickup window.  
    + deliveryWindowStart [Long][UTC]  
        The start time of delivery window.  
    + deliveryWindowEnd [Long][UTC]  
        The end time of delivery window.  
    + referenceNumbers [Array][String]  
        The reference number of order, the maximum of length is 3.  
    + purchaseOrderNumber [String]  
        The purchase order number of order.  
    + sealNumber [String]  
        The seal number of order.  
    + trailerType [String]  
        The trailer type of order, the value of this field should be one of DryVan/Reefer/Flatbed.
    + value [Double]  
        The value of this order, and the unit is US dollar.  
    + weight [Integer]  
        The weight of this order, and the unit is lb.  
    + commodity [String]  
        The commodity of this order.
    + shipperNotes [String]  
        The notes of shipper for this order.  
    + nmfcClass [String]  
        TODO
    + packageType [String]  
        Valid value: BOX
    + pieceType [String]  
        Valid values: "PLT"
    + totalPackages [Integer]  
        The number of packages for BOX.
    + totalPieces [Integer]  
        The number of pieces for PLT.
    + costSummary [Double]  
        The cost summary of this order.
       
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
                "nmfcClass": "",
                "packageType": "",
                "pieceType": "",
                "totalPackages": "",
                "totalPieces": "",
                "costSummary": ""
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

Update the status of order via this interface.

+ Request (application/json)

    + Headers

            ACCESS_KEY_ID: XXXXXXXX
            SECRET_KEY: YYYYYYYYYYYYYYYY

    + Body
    
        + id [String]  
            The unique ID of Next Trucking order.

        + status [String]  
            The status we accept are listed below:
            - Open
            - Set Off
            - Scheduled
            - Delivered
            - Cancelled

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
