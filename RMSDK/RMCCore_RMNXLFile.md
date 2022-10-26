[HOME](Home)
# RMCCore SDK Local File interface #
RMNXLFile class is designed to protect/share local file with specified user membership.
It also include the functions based on following Restful API from RMS  
[Sharing local file](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMS/RESTful%20API/Sharing%20REST%20API#markdown-header-sharing-local-files)  

## RMNXLFile Interface class definition ##
```
#!c++

    class RMNXLFile: public FileBase, RestfulBase
    {
    public:
        RMNXLFile(const std::string& path);
        RMNXLFile(JsonObject * value);
        ~RMNXLFile();

    public:
        bool Open(const RMToken & token);
        void Close();
        
        bool IsUploaded(void);
        uint64_t    size(void);
        
        uint32_t read(uint64_t offset, uint8_t* buf, uint32_t bytesToRead);
 
        bool SetRecipientsList(const std::vector<std::string>& recipients);
        const RMRecipients & GetFileRecipients(void);
        
        std::string GetSourceFilePath(void);
        std::string GetSourceFileName(void) const;
        std::string GetSourceFileExt(void) const;
        
        uint64_t GetNXLRights(void) const;
    public:
        std::string        GetOwnerID();
        std::string        GetAgreement();
        std::string        GetDuid();
        uint32_t        GetMaintainLevel();
        std::string        GetName();
        std::string        GetPathID();
        
    public: //file metadata related API
        RetValue ImportMetadataQueryFromRMSResponse(std::string jsonstr);
        
        uint64_t        GetLastRMSSyncTime();
        uint64_t        GetLastModify();
        std::string        GetFileLink();
        bool            IsShared();
        bool            IsDeleted();
        bool            IsRevoked();
    public:
        RetValue ImportFromRMSResponse(JsonObject * root);
    };
}
```
## [RestfulBase class definition](RestfulBase_Interface) ##
## [FileBase class definition](FileBase_Interface) ##

## NXLFile Interface Functions ##
```
#!c++
	RMNXLFile(const std::string& path);/// constructor 
	/**
	* @param
        *    path  full file path of the NXL file
	*/
```
```
#!c++
	RMNXLFile(JsonObject * value);/// constructor 
	/**
	* @param
        *    value  Json object which is exported by RMNXLFile class
        *    when file token is also imported, the file will be opened during constructor
	*/
```
```
#!c++
	bool Open(const RMToken & token);//open nxl file with specified token 
	/**
	* @param
        *    token  token to decrypt the nxl file
	* @return 
	*    true if open succeed. otherwise call GetLastError() to get the error code
	*/
```

```
#!C++
	void Close();///close file
	/**
	* @return 
	*    none
	*/
```

```
#!c++
	bool IsUploaded(void);///Get file uploading status
	/**
	* @return
        *    true if the nxl file is uploaded to RMS
	*/
```

```
#!c++
	uint64_t  size(void);///get original file size
	/**
	* @return
	*   size of original file. 0 if file is not decrypted.
	*/
```

```
#!c++
	uint32_t read(uint64_t offset, uint8_t* buf, uint32_t bytesToRead);
        /// read file from specified offset. 
	/**
	* @param
    *    offset  the offset read file begin with. offset need based on nxl file block size
    *    buf     pointer to the return buffer
    *    bytesToRead  the bytes to read from nxl file
	* @return
	*    read bytes
	*/
```
```
#!c++
RetValue ImportFromRMSResponse(std::string jsonstr)/// Import upload shared nxl file information
/**
* @param
*    String of json string receive from RMS.
*/
Note: After upload the nxl file. this function need be called to import RMS response.
```

###NXL File properties as local file###
```
#!c++
    bool SetRecipientsList(const std::vector<std::string>& recipients);///Set RecipientsList for NXL file.
    /**
    * @param
    *    recipients  the recipients list for shared nxl file.
    * @return
    *    return true if set recipients list success
    */
    Note: this function must be call before call uploading nxl file to RMS. Otherwise the HTTP Helper will missing recipients information
```
```
#!c++
    const RMRecipients & GetFileRecipients(void);///Get RecipientsList for NXL file.
    /**
    * @param
    *    none
    * @return
    *    recent recipients list for nxl file
    */
    Note: the recipients list may updated after ImportMetadataQueryFromRMSResponse().
```

```
#!c++
    std::string GetSourceFilePath(void);///get original file path
    /**
    * @return
    *   file path string of original file.
    */
```
```
#!c++
    std::string GetSourceFileName(void) const;///get original file name
    /**
    * @return
    *   file name string of original file.
    */
```

```
#!c++
    std::string GetSourceFileExt(void) const;///get original file extension
    /**
    * @return
    *   file extension string of original file.
    */
```

```
    #!c++
    uint64_t GetNXLRights(void) const;///get rights for the NXL file
    /**
    * @return
    *   file rights for NXL file
    */
```
```
#!c++
const std::string   GetOwnerID();///Get OwnerID property of NXL file
/**
* @return
*    the Owner ID property of nxl file
*/

```

```
#!c++
    std::string        GetDuid();///Get DUID property of NXL file
    /**
    * @return
    *    the DUID property of nxl file
    */

```
```
#!c++
    std::string        GetAgreement();///Get Agreement of NXL file
    /**
    * @return
    *    the Agreement property of nxl file
    */

```

```
#!c++
    uint32_t        GetMaintainLevel();//Get Maintain Leve peroperty of NXL file
    /**
    * @return
    *    the token maintain level used for nxl file
    */

```


###NXL File properties from RMS###
```
#!c++
	const std::string   GetName();///Get NXL file name on RMS
	/**
	* @return
        *    the nxl file name on RMS if available. otherwise return empty string
	*/
```


```
#!c++
	const std::string   GetPathID();///Get NXL file path ID on RMS
	/**
	* @return
	*    the nxl file path ID on RMS if available. otherwise return empty string
	*/

```
```
#!c++
	const std::string   GetDisplayPath();///Get NXL file display path on RMS 
	/**
	* @return
	*    the nxl file path for displaying purpose at client if available. otherwise return empty string
	*/

```


###NXL File metadata properties from RMS###

```
#!c++
    uint64_t        GetLastRMSSyncTime();///Get time when synchronize NXL file Metadata information from RMS
    /**
    * @return
    *    the time when user call ImportMetadataQueryFromRMSResponse to import metadata information return from RMS
    */

```

```
#!c++
    unint64_t            GetLastModify();///Get NXL file last modify info on RMS
    /**
    * @return
    *    the nxl file last modify time on RMS if available. otherwise return 0
    */

```

```
#!c++
    std::string        GetFileLink();///Get file link which can access the nxl file online.
    /**
    * @return
    *    url to access this nxl file.
    */

```

```
#!c++
    bool            IsShared();///Get nxl file property on RMS
    /**
    * @return
    *    if the file is shared with others.
    */

```

```
#!c++
    bool            IsDeleted();///Get nxl file property on RMS
    /**
    * @return
    *    if the file is deleted on MyVault.
    */

```
```
#!c++
    bool            IsRevoked();///Get nxl file property on RMS
    /**
    * @return
    *    if the file is revoked by owner.
    */

```

```
#!c++
    RetValue ImportMetadataQueryFromRMSResponse(std::string jsonstr);/// Import query nxl file metadata information return from RMS
    /**
    * @param
    *    String of json string receive from RMS.
    */
    Note: This function can be called multiple times for every metadata query. the related nxl file property will be updated after.
```

