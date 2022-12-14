[HOME](Home)
# Result Interface for error code and message #

## Result Interface ##

SDWLResult: This class shows the function return status - success or failed with error code and message.

```
#!c++

class SDWLResult
{
	int GetCode(); //Get Error codes
	const std::string& GetMsg(); //Get error message related to the code
//following function are for debugging purpose
	const char* GetFile();//Get filename which return the error
	const char* GetFunction();//Get function within which return the error
	int GetLine(); //Get code line which return the error
}
```


## Error Codes ##

The error code is the same as Windows error code - winerror.h.

```
#!c++

#define SDWL_SUCCESS						ERROR_SUCCESS
#define SDWL_PATH_NOT_FOUND					ERROR_PATH_NOT_FOUND
#define SDWL_INVALID_JSON_FORMAT			ERROR_BAD_FORMAT
#define SDWL_INVALID_DATA					ERROR_INVALID_DATA
#define SDWL_CERT_NOT_READY					ERROR_NOT_READY
#define SDWL_NOT_ENOUGH_MEMORY				ERROR_NOT_ENOUGH_MEMORY
#define SDWL_NOT_FOUND						ERROR_NOT_FOUND
#define SDWL_INTERNAL_ERROR					ERROR_EXTENDED_ERROR
#define SDWL_LOGIN_REQUIRED					ERROR_INVALID_ACCESS
#define SDWL_ACCESS_DENIED					ERROR_ACCESS_DENIED
#define SDWL_BUSY							ERROR_BUSY
#define SDWL_ALREADY_EXISTS					ERROR_ALREADY_EXISTS

/************************************************************************/
/* RMS Error Code base starts from 0xF000                               */
/* for API return code from RMS, use the error code minus Error code    */
/*   base to get the result.                                            */
/*   For example, error code 61940 means 500 (61940-0xF000)             */
/************************************************************************/
#define SDWL_RMS_ERRORCODE_BASE				0xF000
```