[HOME](Home)
# RMCCore SDK RestfulBase Interface #

## RestfulBase Interface class definition ##
```
#!c++

namespace RMSDK {
    class RestfulBase
    {   
    public:
        virtual RetValue ImportFromString(std::string jsonstr) = 0;
        virtual RetValue ImportFromJson(JsonObject * value) = 0;
        
        virtual const std::string ExportToString(void) = 0;
        virtual JsonValue * ExportToJson(void) = 0;
        
        virtual RetValue ImportFromRMSResponse(JsonObject * root) = 0;
        virtual RetValue ImportFromRMSResponse(std::string jsonstr) = 0;
    };
    
}
```

## RestfulBase Interface Functions ##
```
#!c++
	RetValue ImportFromJson(JsonObject * value);/// Import class with JsonObject
	/**
	* @param
	*    value  JsonObject for Tenant class
        * @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
	*/
```

```
#!c++
	RetValue ImportFromString(std::string jsonstr);/// Import class from json string
	/**
	* @param
	*    jsonstr  json string saved class value
        * @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
        *    RMSDK_INVALID_JSON_FORMAT    if json string format is not valid
	*/
```

```
#!c++
	RetValue ImportFromRMSResponse(JsonObject * root);/// Import class with JsonObject returned from RMS tenant Restful API
	/**
	* @param
	*    root  RMS returned JsonObject
        * @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
	*/
```
```
#!c++
	RetValue ImportFromRMSResponse(std::string jsonstr);/// Import class with json string returned from RMS tenant Restful API
	/**
	* @param
	*    jsonstr  json string saved class value
        * @return
        *    RMSDK_ERROR_INVALID_DATA     if object is not valid
        *    RMSDK_INVALID_JSON_FORMAT    if json string format is not valid
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
	JsonValue * ExportToJson(void);/// export class data to JsonVaule
	/**
        * @return
        *    JsonVaule for class
	*/
```