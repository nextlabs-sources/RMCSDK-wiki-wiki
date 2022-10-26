[RMCCore Library Home](Home)
#RMCCore Library Common Interfaces#

## [RestfulBase class definition](RestfulBase_Interface) ##
## [HTTPRequest class definition](HttpRequest_Interface) ##

## [Product class definition](Product_Interface) ##

## Result Interface for error code and message ##

### Result Interface ###

```
#!c++

class RetValue
{
public:    
    inline int32_t GetCode() 
    inline int32_t GetLine() 
    inline const char* GetFile() 
    inline const char* GetFunction() 
    
    inline operator bool () 
    inline operator int32_t () 
};
```

### Error Codes ###


```
#!c++

#define RMSDK_ERROR_SUCCESS                 0l
#define RMSDK_ERROR_NOT_ENOUGH_MEMORY       8l		//ERROR_NOT_ENOUGH_MEMORY
#define RMSDK_INVALID_JSON_FORMAT           11l		//ERROR_BAD_FORMAT
#define RMSDK_ERROR_INVALID_DATA            13l		//ERROR_INVALID_DATA
#define RMSDK_ERROR_NOTFOUND				1168l	//ERROR_NOT_FOUND

/************************************************************************/
/* RMS Error Code base starts from 0xF000                               */
/* for API return code from RMS, use the error code minus Error code    */
/*   base to get the result.                                            */
/*   For example, error code 61940 means 500 (61940-0xF000)             */
/************************************************************************/
#define RMSDK_RMS_ERRORCODE_BASE            0xF000
```