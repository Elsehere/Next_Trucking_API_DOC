# Next Trucking FTP Server Usage for White Glove

Next Trucking will send you account and password of FTP once you need to upload files to Next Trucking.  
DO NOT share your account and password with others.

The path /whiteglove is your home path of Next Trucking FTP Server.  
There are two folders under home path, Inbound and Outbound.  
Upload all your files to Inbound, so the path is /whiteglove/Inbound.  
Ignore Outbound folder for now.

Two types of files should be upload to /whiteglove/Inbound.
- POD 
- IMAGE

Filename should be consisted of 4 parts, [Order_ID]_[File_Type]_[Created_UTC_Date].[File_Extension]
- Order_ID 
  - Order Id was return by API of Next Trucking
- File_Type  
  - POD or IMAGE
- Created_UTC_Date  
  - UTC created date of file in your system.
- File_Extension  
  - Next Trucking only accepts JPG/PNG/PDF files.

Example:
- POD
  - T0000001_POD_20170701000001.pdf
  - T0000001_POD_20170701235959.jpg
  - T0001000_POD_20170703235959.png
- IMAGE
  - T0000001_IMAGE_20170701000001.pdf
  - T0000001_IMAGE_20170701235959.jpg
  - T0001000_IMAGE_20170703235959.png
  
Once Next Trucking consumed file on FTP Server, the file will be deleted by Next Trucking.  
For one load, 5 is the maximum for each type of file.
