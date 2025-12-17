# Nebula Troubleshooting Flowchart
這份文件展示了 **18 個步驟的流程圖**，用於工具斷線後的排查流程。  
流程圖使用 **Mermaid 語法**，GitHub 會自動渲染。
---
## 🔄 流程圖
```mermaid
flowchart TD
   A[Disconnect happen] --> B[Copy timestamp/result.dzf]
   B --> C[Search the copied string on Nebula Server.log]
   C -->|Found| D[Check the file queue count]
   C -->|Not Found| E[Goto Tool FW]
   D --> F{Queue count ≤ 100?}
   F -->|Yes| G[Wait for a while (End)]
   F -->|No| H[Check all filter rules]
   H --> I{Filter rule normal?}
   I -->|Yes| J[Network throughput issue (End)]
   I -->|No| K[Update filter rule]
   K --> L[Restart Result Server (End)]
   E --> M[Search Server.log with result string]
   M --> N{Result string found?}
   N -->|No| O[Check Loader setting like watched result folder (End)]
   N -->|Yes| P[Search Server.log with “IsAdded” in 10 minutes]
   P --> Q{IsAdded found?}
   Q -->|Yes| R[Prepare logs and contact RD (End)]
   Q -->|No| S[Check server setting like Server IP on Nebula ResultServerManager]
   S --> T[Goto Result Transfer Manager]
   T --> U[Reconnect the tool]
   U --> V[Stop and start download (End)]
