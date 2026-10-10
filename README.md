# 128bitUI

> Roblox Lua UI Library สำหรับ script executor  
> โดย **128B!t** — ดีไซน์ clean, floating button สี่เหลี่ยมมน, ธีมหลายสี, config auto-save

---

## โหลด Library

```lua
local BitUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/4rise-Dev/128B-t-UI/refs/heads/main/128bitUI.lua"))()
```

> แทน URL ด้วย raw link จาก GitHub ของแก

---

## เริ่มต้นใช้งาน

### สร้าง Window

```lua
local Window = BitUI:CreateWindow({
    Title         = "My Hub",
    SubTitle      = "v1.0",
    LogoId        = "rbxassetid://10709819149",   -- logo หลักบน window
    Size          = UDim2.new(0, 720, 0, 485),
    ToggleKey     = Enum.KeyCode.RightControl,    -- ปุ่มเปิด/ปิด
    DefaultTheme  = "NeverloseCrimson",           -- ธีมเริ่มต้น
})
```

### ธีมที่มี

| ชื่อ | สี |
|---|---|
| `NeverloseCrimson` | แดง |
| `StarHubGold` | ทอง |
| `CyberCyan` | ฟ้าไซเบอร์ |
| `MatrixEmerald` | เขียว |
| `ObsidianViolet` | ม่วง |
| `SakuraBlossom` | ชมพู |
| `GlacierIce` | น้ำเงินน้ำแข็ง |
| `SunsetFlame` | ส้มพระอาทิตย์ตก |
| `ElectricLime` | เขียวสะท้อน |
| `MidnightStealth` | เทา |

---

## Floating Toggle Button

ปุ่มลอยสี่เหลี่ยมมนข้างจอ กด = เปิด/ปิด window

```lua
-- ตั้งค่าผ่าน Settings ก่อน CreateWindow
BitUI.Settings.ShowFloatingToggle = true        -- แสดง/ซ่อน
BitUI.Settings.FloatIconId = "rbxassetid://XXX" -- icon บน floating button
BitUI.Settings.FloatSize   = 52                 -- ขนาด (px)
```

หรือจะตั้งผ่าน Settings tab ใน UI ก็ได้ (auto-save)

---

## สร้าง Tab

```lua
Window:AddNavHeader("SECTION NAME", 1)  -- หัวข้อ separator (LayoutOrder ต้องน้อยกว่า tab)

local MyTab = Window:CreateTab({
    Title       = "Main",
    IconId      = "rbxassetid://10709791882",
    LayoutOrder = 2,
})
```

---

## สร้าง GroupBox

```lua
-- side = "Left" หรือ "Right"
local Box = MyTab:CreateGroupBox("Left", "TITLE", "BADGE", "rbxassetid://ICON")
```

---

## Elements

### Toggle

```lua
local myToggle = Box:AddToggle(
    "Toggle Name",           -- title
    "Description text",      -- คำอธิบาย (nil ได้)
    false,                   -- ค่าเริ่มต้น
    function(value)
        print("Toggle:", value)  -- true/false
    end
)

-- ควบคุมด้วย code
myToggle.Set(true)
local current = myToggle.Get()  -- boolean
```

### Slider

```lua
local mySlider = Box:AddSlider(
    "Speed",    -- title
    0,          -- min
    100,        -- max
    50,         -- default
    "u/s",      -- suffix (หน่วย)
    function(value)
        print("Slider:", value)
    end
)
```

### Dropdown

```lua
local myDropdown = Box:AddDropdown(
    "Mode",
    {"Option A", "Option B", "Option C"},
    "Option A",   -- default
    function(selected)
        print("Selected:", selected)
    end
)
```

### Text Input

```lua
Box:AddInput(
    "Player Name",
    "Enter username...",  -- placeholder
    "",                   -- default
    function(text)
        print("Input:", text)
    end
)
```

### Action Row (ปุ่มคลิกได้)

```lua
Box:AddActionRow(
    "Reset",
    "คืนค่าทุกอย่างกลับ default",
    "rbxassetid://10734933222",   -- icon
    function()
        print("Clicked!")
    end
)
```

---

## Notification

```lua
BitUI:Notify({
    Title      = "TITLE",
    Content    = "เนื้อหา notification",
    Icon       = "rbxassetid://10709752996",        -- optional
    Badge      = "NEW",                             -- optional
    BadgeColor = Color3.fromRGB(34, 197, 94),       -- optional
    Duration   = 4,                                 -- วินาที (default 4)
})
```

---

## Settings Tab (built-in)

```lua
Window:AddNavHeader("SETTINGS", 6)
local SettingsTab = Window:CreateTab({
    Title       = "Settings",
    IconId      = BitUI.Icons.Settings,
    LayoutOrder = 7,
})
Window:CreateDualColumnSettings(SettingsTab)
```

สร้าง settings page สำเร็จรูป — ธีม, เสียง, วอลล์เปเปอร์, transparency, floating toggle

---

## Icons ที่มีใน library

```lua
BitUI.Icons.Logo      -- rbxassetid://10709819149
BitUI.Icons.Settings  -- rbxassetid://10734950309
BitUI.Icons.Zap       -- rbxassetid://10709791882
BitUI.Icons.Combat    -- rbxassetid://10709818534
BitUI.Icons.Refresh   -- rbxassetid://10734933222
BitUI.Icons.Dashboard -- rbxassetid://10709752035
BitUI.Icons.Teleport  -- rbxassetid://10723404337
BitUI.Icons.Check     -- rbxassetid://10709790644
BitUI.Icons.Copy      -- rbxassetid://10709812159
-- ... ดูทั้งหมดใน BitUI.Icons
```

---

## ตัวอย่างสมบูรณ์

```lua
local BitUI = loadstring(game:HttpGet("RAW_URL"))()

BitUI.Settings.FloatIconId = "rbxassetid://10709819149"

local Window = BitUI:CreateWindow({
    Title    = "128B!t Hub",
    SubTitle = "Movement",
    Size     = UDim2.new(0, 720, 0, 485),
    ToggleKey = Enum.KeyCode.RightControl,
})

Window:AddNavHeader("MODULES", 1)

local Tab = Window:CreateTab({
    Title       = "Movement",
    IconId      = BitUI.Icons.Zap,
    LayoutOrder = 2,
})

local Box = Tab:CreateGroupBox("Left", "SPEED", nil, BitUI.Icons.Zap)

local speedToggle = Box:AddToggle("Enable Speed", nil, false, function(v)
    game:GetService("Players").LocalPlayer.Character
        and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Humanoid")
        and (game:GetService("Players").LocalPlayer.Character.Humanoid.WalkSpeed = v and 100 or 16)
end)

Box:AddSlider("WalkSpeed", 16, 300, 16, "SPD", function(v)
    local hum = game:GetService("Players").LocalPlayer.Character
        and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Humanoid")
    if hum and speedToggle.Get() then hum.WalkSpeed = v end
end)

BitUI:Notify({ Title = "LOADED", Content = "128B!t Hub ready", Badge = "OK" })
```

---

## License

MIT — ใช้ได้ฟรี แก้ได้ แจกได้  
Credit: **128B!t**
