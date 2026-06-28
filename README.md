-- SCRIPT TELEPORT CLICK CHO DELTA MOBILE (RUN ONCE)
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local CoreGui = game:GetService("CoreGui")

-- Biến kiểm tra trạng thái bật/tắt
local teleportEnabled = false

-- ==========================================
-- TẠO GIAO DIỆN (GUI) TRÊN ĐIỆN THOẠI
-- ==========================================
local ScreenGui = Instance.new("ScreenGui")
local ToggleButton = Instance.new("TextButton")
local UICorner = Instance.new("UICorner")

-- Cấu hình vị trí và tên cho ScreenGui để không bị lỗi xóa khi chết
ScreenGui.Name = "DeltaTeleportGui"
ScreenGui.Parent = CoreGui
ScreenGui.ResetOnSpawn = false

-- Cấu hình Nút Bấm (Button)
ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = ScreenGui
ToggleButton.Size = UDim2.new(0, 100, 0, 45)
ToggleButton.Position = UDim2.new(0.05, 0, 0.2, 0) -- Nằm ở góc trên bên trái màn hình
ToggleButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50) -- Màu đỏ (Đang tắt)
ToggleButton.Text = "TP: OFF"
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.TextSize = 16
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.Active = true
ToggleButton.Draggable = true -- Bạn có thể giữ và kéo nút này đi chỗ khác nếu vướng

-- Bo góc nút bấm cho đẹp
UICorner.CornerRadius = UDim.new(0, 8)
UICorner.Parent = ToggleButton

-- ==========================================
-- XỬ LÝ LOGIC BẬT/TẮT VÀ DỊCH CHUYỂN
-- ==========================================
-- Bật tắt chế độ khi chạm vào nút trên màn hình
ToggleButton.MouseButton1Click:Connect(function()
    teleportEnabled = not teleportEnabled
    if teleportEnabled then
        ToggleButton.BackgroundColor3 = Color3.fromRGB(50, 180, 50) -- Màu xanh (Đang bật)
        ToggleButton.Text = "TP: ON"
    else
        ToggleButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50) -- Màu đỏ (Đang tắt)
        ToggleButton.Text = "TP: OFF"
    end
end)

-- Xử lý khi chạm vào màn hình game để bay
Mouse.Button1Down:Connect(function()
    if teleportEnabled then
        local character = LocalPlayer.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            -- Lấy vị trí ngón tay chạm vào trong thế giới 3D
            local targetPos = Mouse.Hit.Position
            
            -- Dịch chuyển và cộng thêm 3.5 block chiều cao để tránh bị kẹt xuống đất/sàn nhà
            character.HumanoidRootPart.CFrame = CFrame.new(targetPos + Vector3.new(0, 3.5, 0))
        end
    end
end)

print("[Delta Mobile]: Script Teleport bằng cách chạm màn hình đã sẵn sàng!")
