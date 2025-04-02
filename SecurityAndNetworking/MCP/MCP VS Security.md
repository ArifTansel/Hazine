
Mcp 
- secure
- strandardized
- flexible 

LLM  ve client arasında bir veri alışverişi sağlar(yukarıdakilere uyan). 

MCP client-server mimarisine sahiptir. MCP client ile LLM based uygulama arasındak bağlantıyı kolaylaştırır.  Bu yapı  LLM in sadece gerekli veriye erişebildiğinden emin olur. 

[[server-filesystem(MCP)]] i ele alalım 
- Read/write files
- Create/list/delete directories
- Move files/directories
- Search files
- Get file metadata

server Configuration 
```json
{  
	"mcpServers": {  
		"filesystem": {  
			"command": "npx",  
			"args": [  
			"-y",  
			"@modelcontextprotocol/server-filesystem",  
			"/Users/user/Desktop",  
			"/Users/user/"  
			]  
		} 
	}  
}
```