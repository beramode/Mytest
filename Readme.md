```mermaid
sequenceDiagram
    participant User
    participant Config as HMIConfigKlarf
    participant Service as WaferMapSnapshotService
    participant Table as HMIDataTable
    participant Pane as HMIWaferMapPane
    participant Ctrl as WaferMapCtrl
    participant Draw as DrawSetting

    Note over User,Draw: Case 2: With DieColorSettingList (Use Custom Colors)
    
    User->>Config: Load Config (before button click)
    activate Config
    Config->>Config: Load XML Config
    Note over Config: <DieColorSettings>
    Config->>Config: WaferMapSnapshotDieColorSettingList.Load(childNode)
    Config-->>User: Config Loaded
    deactivate Config
    
    Note over User: Later...
    
    User->>Service: Click Generate KLARF Button
    activate Service
    
    Service->>Table: new HMIDataTable(result)
    Service->>Table: DieColorSettingList = waferMapSnapshotDieColorSettingList
    
    Service->>Ctrl: IsCustomizeDieColor = true
    Service->>Pane: Init(table)
    Pane->>Ctrl: Init(table)
    
    Ctrl->>Draw: new DrawSetting()
    Ctrl->>Draw: SetColor(dieColorSetting, true)
    
    Draw->>Draw: Colors = colorSetting.ColorTable[i].Color
    Draw->>Draw: ValueRange = [BeginValue, EndValue]
    Draw->>Draw: NumOfLevels = colorSetting.Intervals
    Note over Draw: Use custom color settings<br/>Directly from ColorTable

