[HOME](Home)
# RMCCore SDK NXL File interface #
NXL File class is based on following design document
[NXL File Format V2.0](https://bitbucket.org/nxtlbs-devops/rightsmanagement-wiki/wiki/RMD/nxl.format.v2.md)

## NXL File Interface class definition ##
```
#!c++
namespace RMSDK {
namespace NXLFMT {    
class File
{
public:
    File();
    ~File();
    
    // Not copyable/movable
    File(const File& f) = delete;
    File(File&& f) = delete;

    bool good();
    bool opened();
    FileError getError();

    static bool validate(const std::string& file);
    bool create(const std::string& file,
                const Token& token,
                std::string& ownerId,
                const std::vector<uint8_t>& agreement0,
                const std::vector<uint8_t>& agreement1,
                const std::string& info,
                const std::string& policy,
                const std::string& tags,
                const std::vector<uint8_t>& recoveryKey);
    
    bool open(const std::string& path, bool readOnly);
    void close();

    bool setTokenKey(const std::vector<uint8_t>& key);
    bool unpack(const std::string& plainFile, bool replaceExisting);
    bool changeToken(const Token& newToken);

    TokenId getTokenId() const;
    std::string getOwnerId() const;
    uint32_t getFileFlags() const;
    uint32_t getFileAlignment() const;
    uint32_t getAlgorithm() const;
    uint32_t getBlockSize() const;
    uint32_t getContentOffset() const;

    uint32_t getKeyMode() const;
    uint32_t getKeyFlags() const;
    std::vector<uint8_t> getIvSeed() const;
    std::vector<uint8_t> getAgreement0() const;
    std::vector<uint8_t> getAgreement1() const;

    uint64_t getContentLength() const;
    
    uint32_t read(uint64_t offset, uint8_t* buf, uint32_t bytesToRead);
    uint32_t write(uint64_t offset, const uint8_t* buf, uint32_t bytesToWrite);
    
    FileError readInfoSection(std::string& s);
    FileError readPolicySection(std::string& s);
    FileError readTagSection(std::string& s);
    
    FileError writeInfoSection(const std::string& s);
    FileError writePolicySection(const std::string& s);
    FileError writeTagSection(const std::string& s);
};   
}
}

```
## File Error definition ##

```
#!C++
typedef enum {
    FeSuccess = 0,
    FeEmpty,
    FeIoError,
    FeCryptoError,
    FeIoEof,
    FeInvalidSize,
    FeInvalidHeaderSize,
    FeInvalidMagic,
    FeInvalidVersion,
    FeVersionTooOld,
    FeInvalidToken,
    FeInvalidAgreement,
    FeInvalidDuid,
    FeInvalidAlignment,
    FeInvalidAlgorithm,
    FeInvalidBlockSize,
    FeInvalidOwnerId,
    FeInvalidCryptIv,
    FeInvalidCipherCek,
    FeChecksumMismatch,
    FeNoAgreement,
    FeNoSectionNotFound,
    FeNoSectionFileInfo,
    FeNoSectionFilePolicy,
    FeNoSectionFileTag,
    FeNoKek,
    FeNoCek,
    FeDataOverflow,
    FeMax
} FileError;
```

## File Interface Functions ##
```
#!c++
	bool good(); /// Get File class status
	/**
	* @return
	*    return false if error happens. Call function getError() for detail
	*/
```

```
#!c++
	bool opened();/// Get if class is associated with a file
	/**
	* @return
	*    true if create or open function is called and return success.
	*/
```

```
#!c++

	static bool validate(const std::string& file);/// Validate if a file is NXL format 
	/**
	* @return
	*    true if the file has correct NXL format.
	*/
```

```
#!C++

	bool create(const std::string& file, const Token& token, std::string& ownerId, const std::vector<uint8_t>& agreement0, const std::vector<uint8_t>& agreement1, const std::string& info, const std::string& policy, const std::string& tags, const std::vector<uint8_t>& recoveryKey);
        /// Get a NXL file with specified parameters
	/**
	* @param 
	*    file: full path of new NXL file name
	*    token: file token to encrypt the file
	*    ownerId: string of OwnerID of the file
	*    agreement0: first agreement used for the file
	*    agreement1: second agreement used for the file
	*    info: string of file info section for the file
	*    policy: string of policy info section for the file
	*    tags: string of tags for the file
	*    recoveryKey: Key for recovery
	* @return
	*    true if file and NXL header is created
	*/
```

```
#!c++
	bool open(const std::string& path, bool readOnly);///open a NXL file for read
	/**
	* @param
        *    path  NXL file pull path
	* @return
	*    true if file and NXL header is created
	*/
```

```
#!c++
	void close();/// close file
	/**
	* @param
	*    NONE
	*/
```

```
#!c++
	bool setTokenKey(const std::vector<uint8_t>& key);///Set open file with NXL token
	/**
	* @param
        *    key   token to encrypt the file
	* @return
	*    true if succeed
	*/
```
    
```
#!c++
	bool unpack(const std::string& plainFile, bool replaceExisting);
	/**
	* @param
        *    
	* @return
	*    
	*/
```

```
#!c++
	bool changeToken(const Token& newToken);//replace file with new token
	/**
	* @param
        *    newToken  the new token
	* @return
	*    true if replace file token succeed.
	*/
```  
    
```
#!c++
	TokenId getTokenId();//Get NXL File Token ID
	/** 
	* @return
	*    file Token ID.
	*/
```    
```
#!c++
	std::string getOwnerId();//Get NXL File Owner ID
	/**   
	* @return
	*    string of file Owner ID. call GetError() to get error code if empty
	*/
```    
```
#!c++
	uint32_t getFileFlags();//Get NXL file flags
	/**
	* @return
	*    file flags
	*/
```     
```
#!c++
	uint32_t getFileAlignment();//Get NXL file Alignment
	/**   
	* @return
	*    file alignment
	*/
```    
```
#!c++
	uint32_t getAlgorithm() ;//Get NXL file Algorithm
	/**   
	* @return
	*    file algorithm for encryption
	*/
```        
```
#!c++
	uint32_t getBlockSize();//Get NXL file data block size
	/**   
	* @return
	*    file data block size
	*/
```   
```
#!c++
	uint32_t getContentOffset();//Get NXL file data offset of original file content
	/**   
	* @return
	*    the original file content offset 
	*/
```  
```
#!c++
	 uint32_t getKeyMode();//Get NXL file key mode
	/**   
	* @return
	*    Key Mode
	*/
```  
```
#!c++
	uint32_t getKeyFlags() ;//Get NXL file key flags
	/**   
	* @return
	*    Key Flags
	*/
```  
```
#!c++
	 std::vector<uint8_t> getIvSeed()  ;//Get NXL file IV seed
	/**   
	* @return
	*    Iv seed
	*/
```  
```
#!c++
	std::vector<uint8_t> getAgreement0();//Get NXL file first agreement
	/**   
	* @return
	*    first agreement of file
	*/
```  
```
#!c++
	std::vector<uint8_t> getAgreement1();//Get NXL file second agreement
	/**   
	* @return
	*    second agreement of file
	*/
```   

```
#!c++
	uint64_t getContentLength();//Get NXL file original content length
	/**   
	* @return
	*    the length of original file content
	*/
```   

```
#!c++
	uint32_t read(uint64_t offset, uint8_t* buf, uint32_t bytesToRead);//Read NXL file
	/**
	* @param
        *    offset offset of original file content
        *    buf    buffer for read
        *    bytesToRead bytes of buffer size
	* @return
	*    content copied to buffer
	*/
```

```
#!c++
	uint32_t write(uint64_t offset, const uint8_t* buf, uint32_t bytesToWrite);//Write NXL file
	/**
	* @param
        *    offset offset of original file content
        *    buf    buffer to write
        *    bytesToWrite bytes of buffer size
	* @return
	*    content written to the file
	*/
```
```
#!c++
	FileError readInfoSection(std::string& s);//Read File Info Section
	/**
	* @param
        *    s string buffer for File Info Section
	* @return
	*    FeSuccess if succeed
	*/
```
```
#!c++
	FileError readPolicySection(std::string& s); //Read File Policy Section
	/**
	* @param
        *    s string buffer for File Policy Section
	* @return
	*    FeSuccess if succeed
	*/
```
```
#!c++
	FileError readTagSection(std::string& s); //Read File Tags
	/**
	* @param
        *    s string buffer for File Tags
	* @return
	*    FeSuccess if succeed
	*/
```
```
#!c++
	FileError writeInfoSection(const std::string& s);//Write NXL File Info Section
	/**
	* @param
        *    s File Info Section for NXL file
	* @return
	*    FeSuccess if succeed
	*/
```
```
#!c++
	 FileError writePolicySection(const std::string& s);//Write NXL File Policy Section
	/**
	* @param
        *    s File Policy Section for NXL file
	* @return
	*    FeSuccess if succeed
	*/
```
```
#!c++
	 FileError writeTagSection(const std::string& s);//Write NXL File Tags
	/**
	* @param
        *    s File Tags for NXL file
	* @return
	*    FeSuccess if succeed
	*/
```