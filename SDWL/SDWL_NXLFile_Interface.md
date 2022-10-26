[HOME](Home)

# SDWL NXL File Interface for NXL File Information#
To obtain tenant interface handler, Call [User Interface](SDWL_User_Interface) function
```C++
SDWLResult OpenFile(std::wstring nxlfilepath, ISDRmNXLFile ** file);
```

## NXL File Class ##

ISDRmNXLFile: can get nxl file information. such as file size, rights, tags, expiration, water mark and tenant name.

```
#!c++
class ISDRmNXLFile
{
public:
const std::wstring GetFileName(void);
uint64_t GetFileSize(void);
bool IsValidNXL(void);
const std::vector<SDRmFileRight> GetRights(void);
bool CheckRights(SDRmFileRight right);
bool IsOpen(void);
bool IsUploadToRMS(void);
bool IsRecipientsSynced(void);
std::string GetTenantName(void) const;
std::string GetAdhocWaterMarkString(void) const;
const SDR_WATERMARK_INFO GetWaterMark(void);
const std::string GetTags(void);
const SDR_Expiration GetExpiration(void);
bool CheckExpired();
};


```
## NXL File Interface ##

```
#!c++
const std::wstring GetFileName(void);
/// Get NXL filename
/**
* @return
*    Result: filename string
*/
```

```
#!c++
const uint64_t GetFileSize(void);
/// Get NXL file size
/**
* @return
*    Result: file size.
*/
```

```
#!c++
bool IsValidNXL(void);
/// If the current file is a valid NXL file
/**
* @return true if file is valid NXL file. if the file is not valid NXL, the return value of following function cannot be trusted.
*/
```

```
#!c++
const std::vector<SDRmFileRight> GetRights(void);
/// Get NXL file rights
/**
* @return array of rights asssigned to current file.
*/
```

```
#!c++
bool CheckRights(SDRmFileRight right);
/// check if current file has specific right
/**
* @return true if file has right. when calling this function, a activity log will send to server for the request.
*/
```

```
#!c++
bool IsOpen(void);
/// Is file open
/**
* @param
*    none
* @return
*           true if file is open
*/
```

```
#!c++
bool IsUploadToRMS(void);
/// check if current file has been uploaded to RMS
/**
* @return true if file is uploaded. false if the file is not uploaded.
*/
```

```
#!c++
bool IsRecipientsSynced(void);
/// check if shared users (recipients) of current file have been synced/uploaded to RMS
/**
* @return true if recipients are uploaded. false if recipients are not uploaded.
*/
```

```
#!c++
std::string GetTenantName() const;
/// Get tenant from the protected file
/**
* @param
*    none
* @return
*           tenant data.
*/
```

```
#!c++
std::string GetAdhocWaterMarkString()  const= 0;
/// Get string representing watermark in Ad-hoc policy
/**
* @param
*    none
* @return
*           watermark string
*/
```

```
#!c++
const SDR_WATERMARK_INFO GetWaterMark(void);
/// Get water mark info
/**
* @param
*    none
* @return
*           SDR_WATERMARK_INFO structure
*/
```

```
#!c++
const std::string GetTags(void);
/// Get nxl file tags
/**
* @param
*    none
* @return
*           tags string
*/
```

```
#!c++
const SDR_Expiration GetExpiration(void);
/// Get nxl file expiration
/**
* @param
*    none
* @return
*           SDR_Expiration
*/
```

```
#!c++
bool CheckExpired();
/// Check if nxl file is expirated
/**
* @param
*    none
* @return
*           result bool
*/
```