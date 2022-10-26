[HOME](Home)

# SDWL Types Interface #

## Type Definitions ##
The definition is used to communicate between application and sdk library.

```
#!c++

typedef enum _USERIDPTYPE {
	SKYDRM = 0,
	SAML,
	GOOGLE,
	FACEBOOK,
	YAHOO
} USER_IDPTYPE;


typedef struct _SDR_FILE_ACTIVITY_INFO {
	std::string duid;
	std::string email;
	std::string operation;
	std::string deviceType;
	std::string deviceId;
	std::string accessResult;
	uint64_t accessTime;
} SDR_FILE_ACTIVITY_INFO;

typedef struct _SDR_PROJECT_INFO {
	uint32_t      projid;
	std::string   name;
	std::string   displayname;
	std::string   description;
	bool          bowner;
	uint64_t	  totalfiles;
} SDR_PROJECT_INFO;

typedef enum _WATERMARK_ROTATION {
	NOROTATION = 0,
	CLOCKWISE,
	ANTICLOCKWISE
} WATERMARK_ROTATION;

typedef struct _SDR_WATERMARK_INFO {
	std::string   text;
	std::string   fontName;
	std::string   fontColor;
	int           fontSize;
	int           transparency;
	WATERMARK_ROTATION           rotation;
	bool          repeat;
} SDR_WATERMARK_INFO;

typedef struct _SDR_OBLIGATION_INFO {
	std::wstring                                        name;
	std::vector<std::pair<std::wstring, std::wstring>>  options;
} SDR_OBLIGATION_INFO;

typedef enum  {
	ALL = 0,
	OWNEDBYME,
	OWNEDBYOTHER
} PROJECT_FILTER;

enum IExpiryType {
	NEVEREXPIRE = 0,
	RELATIVEEXPIRE,
	ABSOLUTEEXPIRE,
	RANGEEXPIRE
};

struct SDR_Expiration {
	IExpiryType   type;
	uint64_t start;
	uint64_t end;

	SDR_Expiration() {
		type = IExpiryType::NEVEREXPIRE;
		start = 0;
		end = 0;
	}
};

typedef enum {
	RLOProtect = 1,
	RLOShare,
	RLORemoveUser,
	RLOView,
	RLOPrint,
	RLODownload,
	RLOEdit,
	RLORevoke,
	RLODecrypt,
	RLOCopyContent,
	RLOCaptureScreen,
	RLOClassify,
	RLOReshare,
	RLODelete
} SRMActivityLogOperation;

typedef struct {
	std::string   name;
	bool          allow;
} SDR_CLASSIFICATION_LABELS;

typedef struct {
	std::string   name;
	bool          multiSelect;
	bool          mandatory;
	std::vector<SDR_CLASSIFICATION_LABELS> labels;
} SDR_CLASSIFICATION_CAT;

```