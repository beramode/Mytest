```mermaid
flowchart TD
   A[Disconnect happen] --> B[Copy timestamp/result.dzf]
   B --> C[Search the copied string on Nebula Server.log]
   C -->|Found| D[Check the file queue count]
   C -->|Not Found| E[Goto Tool FW]

