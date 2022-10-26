[HOME](Home)
# RMCCore SDK FileBase Interface #

## FileBase Interface class definition ##
```
#!c++
namespace RMSDK {
    class FileBase
    {
    public:
        FileBase(const std::string& path);
	virtual ~FileBase() {};
        virtual bool IsOpened();
        virtual bool Open() = 0;
        virtual void Close() = 0;
        bool IsNXL();

        RetValue GetLastError();
    public:
        virtual uint32_t read(uint64_t offset, uint8_t* buf, uint32_t bytesToRead) = 0;
    public:
        std::string     m_filepath;
        std::wstring    m_wfilepath;
    };
```

## FileBase Interface Functions ##
```
#!c++
	FileBase(const std::string& path);/// constructor
	/**
	* @param
	*    path  full path of file
	*/
```

```
#!c++
	virtual bool IsOpened();/// Is file opened
	/**
        * @return
        *    bool     true if opened. otherwise call function GetLastError() for error information
	*/
```

```
#!c++
	virtual bool Open() = 0;/// open file
	/**
	* @param
	*    none
        * @return
        *    true if open file succeed. otherwise call function GetLastError for error information
	*/
```

```
#!c++
	const std::string ExportToString(void);/// export class data to Json string
	/**
        * @return
        *    json string with class values
	*/
```

```
#!c++
	virtual void Close() = 0;///close file
	/**
        * @return
        *    none
	*/
```

```
#!c++
	bool IsNXL();/// is the file NXL format
	/**
        * @return
        *    true if the file is nxl format
	*/
```
```
#!c++
	RetValue GetLastError();/// Get last error code of file operation
	/**
        * @return
        *    last error code and message
	*/
```
```
#!c++
	virtual uint32_t read(uint64_t offset, uint8_t* buf, uint32_t bytesToRead);
        /// Read file
	/**
	* @param
	*    offset  the offset of file 
	*    buf     the return buffer pointer
	*    bytesToRead  the buffer size for return data
        * @return
        *    read bytes
	*/
```