## Create Window
```lua
local utility = {}
local UIS = game:GetService("UserInputService");
local RS = game:GetService("RunService");
local TS = game:GetService("TweenService");
local mouse = game:GetService('Players').LocalPlayer:GetMouse()

local Library = {}
local mainKeybind = "LeftControl"
local canDrag = true

function utility:ToRGB(color)  
	return color.R*255,color.G*255,color.B*255
end

local function CreateDrag(gui)
	local dragging
	local dragInput
	local dragStart
	local startPos

	local function update(input)
		local delta = input.Position - dragStart
		TS:Create(gui, TweenInfo.new(0.16, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)}):Play();
	end

	local lastEnd = 0
	local lastMoved = 0
	local con
	gui.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			if not canDrag then return end
			dragging = true
			dragStart = input.Position
			startPos = gui.Position

		end
	end)

	UIS.InputEnded:Connect(function(input)

		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = false
		end
	end)


	gui.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
			lastMoved = os.clock()
		end
	end)

	UIS.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			update(input)
		end
	end)
end

local tweenInfo = TweenInfo.new(.2, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut)
local tweenInfo2 = TweenInfo.new(.5, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut)
function Library:tween(object, goal, callback)
	local tween = TS:Create(object, tweenInfo, goal)
	tween.Completed:Connect(callback or function() end)
	tween:Play()
end

function Library:tween2(object, goal, callback)
	local tween = TS:Create(object, tweenInfo2, goal)
	tween.Completed:Connect(callback or function() end)
	tween:Play()
end

local ScreenGui = Instance.new('ScreenGui', gethui())

function Library:CreateWindow(options)
	local GUI = {
		CurrentTab = nil
	}
	

	local Main = Instance.new('Frame', ScreenGui)
	local Title = Instance.new('TextLabel', Main)
	local Divider = Instance.new('Frame', Main)
	local TabBar = Instance.new('ScrollingFrame', Main)
	local TabLayout = Instance.new('UIListLayout', TabBar)
	local TabBarPad = Instance.new('UIPadding', TabBar)
	local MainCorner = Instance.new('UICorner', Main)
	local MainGradient = Instance.new('UIGradient', Main)
	local Divider2 = Instance.new('Frame', Main)
	
	ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	Main.Name = "Main"
	Main.Position = UDim2.new(0.271,0,0.2845,0)
	Main.Size = UDim2.new(0,710,0,405)
	Main.BackgroundColor3 = Color3.new(1,1,1)
	Main.BorderSizePixel = 0
	Main.BorderColor3 = Color3.new(0,0,0)
	Main.ZIndex = 100
	Title.Name = "Title"
	Title.Position = UDim2.new(0.0254,0,0,0)
	Title.Size = UDim2.new(0,143,0,50)
	Title.BackgroundColor3 = Color3.new(1,1,1)
	Title.BackgroundTransparency = 1
	Title.BorderSizePixel = 0
	Title.BorderColor3 = Color3.new(0,0,0)
	Title.Text = options.Title
	Title.TextColor3 = Color3.new(0.7843,0.7843,0.7843)
	Title.Font = Enum.Font.Gotham
	Title.TextSize = 23
	Title.ZIndex = 101
	Title.TextXAlignment = Enum.TextXAlignment.Left
	Divider.Name = "Divider"
	Divider.Position = UDim2.new(0,0,0.121,0)
	Divider.Size = UDim2.new(0,710,0,1)
	Divider.BackgroundColor3 = Color3.new(0.7843,0.7843,0.7843)
	Divider.BorderSizePixel = 0
	Divider.BorderColor3 = Color3.new(0,0,0)
	Divider.ZIndex = 102
	TabBar.Name = "TabBar"
	TabBar.Position = UDim2.new(0,0,0.1235,0)
	TabBar.Size = UDim2.new(0,161,0,355)
	TabBar.BackgroundColor3 = Color3.new(1,1,1)
	TabBar.BackgroundTransparency = 1
	TabBar.BorderSizePixel = 0
	TabBar.BorderColor3 = Color3.new(0,0,0)
	TabBar.ZIndex = 103
	TabBar.ScrollingEnabled = false
	TabBar.ScrollBarThickness = 0
	TabBar.ScrollBarImageColor3 = Color3.new(0,0,0)
	TabLayout.Name = "TabLayout"
	TabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
	TabLayout.SortOrder = Enum.SortOrder.LayoutOrder
	TabBarPad.Name = "TabBarPad"
	TabBarPad.PaddingTop = UDim.new(0,5)
	Divider2.Name = "Divider2"
	Divider2.Position = UDim2.new(0.2246,0,0.121,0)
	Divider2.Size = UDim2.new(0,1,0,356)
	Divider2.BackgroundColor3 = Color3.new(0.6392,0.6392,0.6392)
	Divider2.BackgroundTransparency = 0.5
	Divider2.BorderSizePixel = 0
	Divider2.BorderColor3 = Color3.new(0,0,0)
	Divider2.ZIndex = 102
	MainCorner.CornerRadius = UDim.new(0,20)
	MainGradient.Name = "MainGradient"
	MainGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.new(0.04313725605607033, 0.019607843831181526, 0.15294118225574493)), ColorSequenceKeypoint.new(1.00,Color3.new(0.5098039507865906, 0.1882352977991104, 0.1568627506494522))}

	local MC = Instance.new('ScreenGui', gethui())
	local MobileCard = Instance.new('ImageButton', MC)
	local CardGradient = Instance.new('UIGradient', MobileCard)
	local CardText = Instance.new('TextLabel', MobileCard)
	local CardCorner = Instance.new('UICorner', MobileCard)

	MC.Name = "MC"
	MC.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	MobileCard.Name = "MobileCard"
	MobileCard.Position = UDim2.new(0.5, -20, 0, 10);
	MobileCard.Size = UDim2.new(0,40,0,40)
	MobileCard.BackgroundColor3 = Color3.new(1,1,1)
	MobileCard.BorderSizePixel = 0
	MobileCard.BorderColor3 = Color3.new(0,0,0)
	MobileCard.AutoButtonColor = false
	CardGradient.Name = "CardGradient"
	CardGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.new(0.04313725605607033, 0.019607843831181526, 0.15294118225574493)), ColorSequenceKeypoint.new(1.00,Color3.new(0.5098039507865906, 0.1882352977991104, 0.1568627506494522))}
	CardGradient.Rotation = -84
	CardText.Name = "CardText"
	CardText.Size = UDim2.new(0,40,0,40)
	CardText.BackgroundColor3 = Color3.new(1,1,1)
	CardText.BackgroundTransparency = 1
	CardText.BorderSizePixel = 0
	CardText.BorderColor3 = Color3.new(0,0,0)
	CardText.Text = "S"
	CardText.TextColor3 = Color3.new(0.7843,0.7843,0.7843)
	CardText.Font = Enum.Font.Gotham
	CardText.TextSize = 23
	CardText.ZIndex = 101

	MobileCard.MouseButton1Click:Connect(function()
		ScreenGui.Enabled = not ScreenGui.Enabled
	end)
	
	CreateDrag(MobileCard)
	CreateDrag(Main)

	function Library:Toggle()
		ScreenGui.Enabled = not ScreenGui.Enabled
	end

	UIS.InputBegan:Connect(function(key, gp)
		if gp then return end;

		if key.KeyCode == Enum.KeyCode[mainKeybind] then
			Library:Toggle()
		end
	end)

	function GUI:NewTab(options)
		
		local tab = {
			Active = false
		}
		
		local Canvas = Instance.new('ScrollingFrame', Main)
		local UIListLayout = Instance.new('UIListLayout', Canvas)
		local UIPadding = Instance.new('UIPadding', Canvas)
		local SelectedTab = Instance.new('Frame', TabBar)
		local Highlight = Instance.new('Frame', SelectedTab)
		local STCorner = Instance.new('UICorner', SelectedTab)
		local Tab = Instance.new('TextButton', SelectedTab)
		
		SelectedTab.Name = "SelectedTab"
		SelectedTab.Position = UDim2.new(88.03,0,0.6006,0)
		SelectedTab.Size = UDim2.new(0,118,0,34)
		SelectedTab.BackgroundColor3 = Color3.new(0,0,0)
		SelectedTab.BackgroundTransparency = 1
		SelectedTab.BorderSizePixel = 0
		SelectedTab.BorderColor3 = Color3.new(0,0,0)
		SelectedTab.ZIndex = 100
		Highlight.Name = "Highlight"
		Highlight.Position = UDim2.new(0.0508,0,0.2353,0)
		Highlight.Size = UDim2.new(0,2,0,18)
		Highlight.BackgroundColor3 = Color3.new(0.8353,0.8353,0.8353)
		Highlight.BorderSizePixel = 0
		Highlight.Transparency = 1
		Highlight.BorderColor3 = Color3.new(0,0,0)
		Highlight.ZIndex = 101
		STCorner.CornerRadius = UDim.new(0,6)
		Tab.Name = "Tab"
		Tab.Position = UDim2.new(0.0678,0,0,0)
		Tab.Size = UDim2.new(0,109,0,34)
		Tab.BackgroundColor3 = Color3.new(1,1,1)
		Tab.BackgroundTransparency = 1
		Tab.BorderSizePixel = 0
		Tab.BorderColor3 = Color3.new(0,0,0)
		Tab.Text = options.Name
		Tab.TextColor3 = Color3.new(0.5529,0.5529,0.5529)
		Tab.Font = Enum.Font.Gotham
		Tab.TextSize = 14
		Tab.ZIndex = 105
		Tab.AutoButtonColor = false		
		Canvas.Name = "Canvas"
		Canvas.Position = UDim2.new(0.2268,0,0.1235,0)
		Canvas.Size = UDim2.new(0,549,0,355)
		Canvas.BackgroundColor3 = Color3.new(1,1,1)
		Canvas.BackgroundTransparency = 1
		Canvas.BorderSizePixel = 0
		Canvas.BorderColor3 = Color3.new(0,0,0)
		Canvas.ZIndex = 107
		Canvas.Visible = false
		Canvas.AutomaticCanvasSize = Enum.AutomaticSize.Y;
		Canvas.ScrollBarThickness = 0
		Canvas.ScrollBarImageColor3 = Color3.new(0,0,0)
		UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0,5)
		UIPadding.PaddingTop = UDim.new(0,10)
		
		function tab:Activate()
			if not tab.Active then
				if GUI.CurrentTab ~= nil then
					GUI.CurrentTab:Deactivate()
				end
				tab.Active = true
				Library:tween(Tab, {TextColor3 = Color3.new(1,1,1)})
				Library:tween(SelectedTab, {BackgroundTransparency = 0.5})
				Library:tween(Highlight, {BackgroundTransparency = 0})
				Canvas.Visible = true
				GUI.CurrentTab = tab
			end
		end

		function tab:Deactivate()
			if tab.Active then
				tab.Active = false
				Library:tween(Tab, {TextColor3 =Color3.new(0.5529,0.5529,0.5529)})
				Library:tween(SelectedTab, {BackgroundTransparency = 1})
				Library:tween(Highlight, {BackgroundTransparency = 1})
				Canvas.Visible = false
			end
		end

		Tab.MouseButton1Click:Connect(function()
			tab:Activate()
		end)

		if GUI.CurrentTab == nil then
			tab.Activate()	
		end
		
		
		function tab:NewToggle(options)
			
			local toggle = {
				State = false
			}
			
			local Toggle = Instance.new('ImageButton', Canvas)
			local ToggleTitle = Instance.new('TextLabel', Toggle)
			local CheckBox = Instance.new('Frame', Toggle)
			local CheckBoxCorner = Instance.new('UICorner', CheckBox)
			local CheckMark = Instance.new('ImageButton', CheckBox)
			local ToggleCorner = Instance.new('UICorner', Toggle)
			


			Toggle.Name = "Toggle"
			Toggle.Position = UDim2.new(0.2606,0,0.5185,0)
			Toggle.Size = UDim2.new(0,499,0,34)
			Toggle.BackgroundColor3 = Color3.new(0,0,0)
			Toggle.BackgroundTransparency = 0.5
			Toggle.BorderSizePixel = 0
			Toggle.BorderColor3 = Color3.new(0,0,0)
			Toggle.ZIndex = 108
			Toggle.AutoButtonColor = false		
			ToggleTitle.Name = "ToggleTitle"
			ToggleTitle.Position = UDim2.new(0.0321,0,0,0)
			ToggleTitle.Size = UDim2.new(0,363,0,34)
			ToggleTitle.BackgroundColor3 = Color3.new(1,1,1)
			ToggleTitle.BackgroundTransparency = 1
			ToggleTitle.BorderSizePixel = 0
			ToggleTitle.BorderColor3 = Color3.new(0,0,0)
			ToggleTitle.Text = options.Name
			ToggleTitle.TextColor3 = Color3.new(0.851,0.851,0.851)
			ToggleTitle.Font = Enum.Font.Gotham
			ToggleTitle.TextSize = 14
			ToggleTitle.ZIndex = 109
			ToggleTitle.TextXAlignment = Enum.TextXAlignment.Left
			CheckBox.Name = "CheckBox"
			CheckBox.Position = UDim2.new(0.9359,0,0.1471,0)
			CheckBox.Size = UDim2.new(0,24,0,24)
			CheckBox.BackgroundColor3 = Color3.new(0.0706,0.0706,0.0706)
			CheckBox.BorderSizePixel = 0
			CheckBox.BorderColor3 = Color3.new(0,0,0)
			CheckBox.ZIndex = 107
			CheckBoxCorner.CornerRadius = UDim.new(0,5)
			CheckMark.Name = "CheckMark"
			CheckMark.Position = UDim2.new(0.0464,0,0.0417,0)
			CheckMark.Size = UDim2.new(0,22,0,22)
			CheckMark.BackgroundColor3 = Color3.new(0,0,0)
			CheckMark.BackgroundTransparency = 1
			CheckMark.BorderSizePixel = 0
			CheckMark.BorderColor3 = Color3.new(0,0,0)
			CheckMark.Image = "rbxassetid://6031094667"
			CheckMark.Visible = true
			CheckMark.AutoButtonColor = false
			CheckMark.ZIndex = 107
			ToggleCorner.CornerRadius = UDim.new(0,6)
			
			toggle.State = options.default

			options.callback(toggle.State)

			if toggle.State then
				Library:tween(CheckMark, {ImageTransparency = 0})
			else
				Library:tween(CheckMark, {ImageTransparency = 1})
			end

			function toggle:Toggle(boolean)
				if boolean == nil then
					toggle.State = not toggle.State
				else
					toggle.State = boolean
				end

				if toggle.State then
					print("a")
					Library:tween(CheckMark, {ImageTransparency = 0})
				else
					Library:tween(CheckMark, {ImageTransparency = 1})
				end

				options.callback(toggle.State)
			end

			Toggle.MouseButton1Down:Connect(function()
				toggle:Toggle()
			end)
			
			return toggle
		end
		
		function tab:NewSlider(options)
			local slider = {
				hover = false,
				MouseDown = false,
				connections = {}
			}
			
			local Slider = Instance.new('ImageButton', Canvas)
			local SliderTitle = Instance.new('TextLabel', Slider)
			local SliderBack = Instance.new('Frame', Slider)
			local SliderBackCorner = Instance.new('UICorner', SliderBack)
			local SliderMain = Instance.new('Frame', SliderBack)
			local SliderMainCorner = Instance.new('UICorner', SliderMain)
			local SliderCorner = Instance.new('UICorner', Slider)
			local SliderAmt = Instance.new('TextBox', Slider)
			

			Slider.Name = "Slider"
			Slider.Position = UDim2.new(0.2606,0,0.5185,0)
			Slider.Size = UDim2.new(0,499,0,34)
			Slider.BackgroundColor3 = Color3.new(0,0,0)
			Slider.BackgroundTransparency = 0.5
			Slider.BorderSizePixel = 0
			Slider.BorderColor3 = Color3.new(0,0,0)
			Slider.ZIndex = 108
			Slider.AutoButtonColor = false
			SliderTitle.Name = "SliderTitle"
			SliderTitle.Position = UDim2.new(0.0321,0,0,0)
			SliderTitle.Size = UDim2.new(0,211,0,34)
			SliderTitle.BackgroundColor3 = Color3.new(1,1,1)
			SliderTitle.BackgroundTransparency = 1
			SliderTitle.BorderSizePixel = 0
			SliderTitle.BorderColor3 = Color3.new(0,0,0)
			SliderTitle.Text = options.Name
			SliderTitle.TextColor3 = Color3.new(0.851,0.851,0.851)
			SliderTitle.Font = Enum.Font.Gotham
			SliderTitle.TextSize = 14
			SliderTitle.ZIndex = 109
			SliderTitle.TextXAlignment = Enum.TextXAlignment.Left
			SliderBack.Name = "SliderBack"
			SliderBack.Position = UDim2.new(0.5251,0,0.4118,0)
			SliderBack.Size = UDim2.new(0,229,0,6)
			SliderBack.BackgroundColor3 = Color3.new(0.0706,0.0706,0.0706)
			SliderBack.BorderSizePixel = 0
			SliderBack.BorderColor3 = Color3.new(0,0,0)
			SliderBack.ZIndex = 109
			SliderBackCorner.CornerRadius = UDim.new(0,5)
			SliderMain.Name = "SliderMain"
			SliderMain.Position = UDim2.new(-0,0,0,0)
			SliderMain.Size = UDim2.new(0,118,0,6)
			SliderMain.BackgroundColor3 = Color3.new(1,1,1)
			SliderMain.BorderSizePixel = 0
			SliderMain.BorderColor3 = Color3.new(0,0,0)
			SliderMain.ZIndex = 109
			SliderMainCorner.CornerRadius = UDim.new(0,5)
			SliderCorner.CornerRadius = UDim.new(0,6)
			SliderAmt.Name = "SliderAmt"
			SliderAmt.Position = UDim2.new(0.4569,0,0,0)
			SliderAmt.Size = UDim2.new(0,34,0,34)
			SliderAmt.BackgroundColor3 = Color3.new(1,1,1)
			SliderAmt.BackgroundTransparency = 1
			SliderAmt.BorderSizePixel = 0
			SliderAmt.BorderColor3 = Color3.new(0,0,0)
			SliderAmt.Text = "33"
			SliderAmt.TextColor3 = Color3.new(0.851,0.851,0.851)
			SliderAmt.Font = Enum.Font.Gotham
			SliderAmt.TextSize = 11
			SliderAmt.ZIndex = 109
			

			function slider:SetValue(v)
				if v == nil then
					local percentage = math.clamp((mouse.X - SliderBack.AbsolutePosition.X) / (SliderBack.AbsoluteSize.X), 0, 1)
					local value = ((options.max - options.min) * percentage) + options.min
					if value % 1 == 0 then
						SliderAmt.Text = string.format("%.0f", value)
					else
						SliderAmt.Text = string.format("%.2f", value)
					end
					SliderMain.Size = UDim2.fromScale(percentage, 1)
				else
					if v % 1 == 0 then
						SliderAmt.Text = string.format("%.0f", v)
					else
						SliderAmt.Text = tostring(v)
					end
					SliderMain.Size = UDim2.fromScale(((v - options.min) / (options.max - options.min)), 1)
				end
				options.callback(slider:GetValue())
			end


			function slider:GetValue()
				return tonumber(SliderAmt.Text)
			end

			slider:SetValue(options.default)

			SliderAmt.FocusLost:Connect(function()
				local toNum
				pcall(function()
					toNum = tonumber(SliderAmt.Text)
				end)
				if toNum then
					toNum = math.clamp(toNum, options.min, options.max)
					slider:SetValue(toNum)
				else
					SliderAmt.Text = "only number :<"
				end
			end)

			local Connection;
			table.insert(slider.connections, UIS.InputEnded:Connect(function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
					pcall(function()
						Connection:Disconnect();
						Connection = nil;
					end)
				end
			end))

			--LPH_NO_VIRTUALIZE(function()
			table.insert(slider.connections, Slider.MouseButton1Down:Connect(function()
				if(Connection) then
					Connection:Disconnect();
				end;

				Connection = RS.Heartbeat:Connect(function()
					--options.callback()

						slider:SetValue()

				end)
			end))
			--end)()

			return slider
		end
		
		function tab:NewDropDown(options)
			local dropdown = {}
			
			local Dropdown = Instance.new('Frame', Canvas)
			local DropdownTitle = Instance.new('TextLabel', Dropdown)
			local DropdownSelected = Instance.new('Frame', Dropdown)
			local SelectedOptionCorner = Instance.new('UICorner', DropdownSelected)
			local SelectedText = Instance.new('TextButton', DropdownSelected)
			local DropdownCorner = Instance.new('UICorner', Dropdown)
			
			Dropdown.Name = "Dropdown"
			Dropdown.Position = UDim2.new(0.2606,0,0.5185,0)
			Dropdown.Size = UDim2.new(0,499,0,34)
			Dropdown.BackgroundColor3 = Color3.new(0,0,0)
			Dropdown.BackgroundTransparency = 0.5
			Dropdown.BorderSizePixel = 0
			Dropdown.BorderColor3 = Color3.new(0,0,0)
			Dropdown.ZIndex = 108
			DropdownTitle.Name = "DropdownTitle"
			DropdownTitle.Position = UDim2.new(0.0321,0,0,0)
			DropdownTitle.Size = UDim2.new(0,312,0,34)
			DropdownTitle.BackgroundColor3 = Color3.new(1,1,1)
			DropdownTitle.BackgroundTransparency = 1
			DropdownTitle.BorderSizePixel = 0
			DropdownTitle.BorderColor3 = Color3.new(0,0,0)
			DropdownTitle.Text = options.Name
			DropdownTitle.TextColor3 = Color3.new(0.851,0.851,0.851)
			DropdownTitle.Font = Enum.Font.Gotham
			DropdownTitle.TextSize = 14
			DropdownTitle.ZIndex = 109
			DropdownTitle.TextXAlignment = Enum.TextXAlignment.Left
			DropdownSelected.Name = "DropdownSelected"
			DropdownSelected.Position = UDim2.new(0.6794,0,0.1471,0)
			DropdownSelected.Size = UDim2.new(0,152,0,24)
			DropdownSelected.BackgroundColor3 = Color3.new(0.0706,0.0706,0.0706)
			DropdownSelected.BorderSizePixel = 0
			DropdownSelected.BorderColor3 = Color3.new(0,0,0)
			DropdownSelected.ZIndex = 109
			SelectedOptionCorner.CornerRadius = UDim.new(0,5)
			SelectedText.Name = "SelectedText"
			SelectedText.Position = UDim2.new(0.0321,0,0,0)
			SelectedText.Size = UDim2.new(0,147,0,24)
			SelectedText.BackgroundColor3 = Color3.new(1,1,1)
			SelectedText.BackgroundTransparency = 1
			SelectedText.BorderSizePixel = 0
			SelectedText.BorderColor3 = Color3.new(0,0,0)
			SelectedText.AutoButtonColor = false
			SelectedText.Text = options.default
			SelectedText.TextColor3 = Color3.new(0.851,0.851,0.851)
			SelectedText.Font = Enum.Font.Gotham
			SelectedText.TextSize = 13
			SelectedText.ZIndex = 109
			DropdownCorner.CornerRadius = UDim.new(0,6)
			

			local DropDownOptions = Instance.new('Frame', Main)
			local Frame = Instance.new('Frame', DropDownOptions)
			local UIListLayout = Instance.new('UIListLayout', Frame)

			--Properties

			DropDownOptions.Name = "DropDownOptions"
			DropDownOptions.Position = UDim2.new(1.0211,0,0.1358,0)
			DropDownOptions.Size = UDim2.new(0,100,0,49)
			DropDownOptions.BackgroundColor3 = Color3.new(0,0,0)
			DropDownOptions.BackgroundTransparency = 0.25
			DropDownOptions.BorderSizePixel = 0
			DropDownOptions.BorderColor3 = Color3.new(0,0,0)
			DropDownOptions.Visible = false
			DropDownOptions.AutomaticSize = Enum.AutomaticSize.XY
			DropDownOptions.ZIndex = 110
			Frame.Size = UDim2.new(0,100,0,49)
			Frame.BackgroundColor3 = Color3.new(1,1,1)
			Frame.BackgroundTransparency = 1
			Frame.BorderSizePixel = 0
			Frame.BorderColor3 = Color3.new(0,0,0)
			Frame.AutomaticSize = Enum.AutomaticSize.XY
			Frame.ZIndex = 110
			UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
			UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
			
			for i, v in pairs(options.options) do
				local Option = Instance.new('TextButton', Frame)
				local Highlight = Instance.new('Frame', Option)
				Option.Name = "Option"
				Option.Position = UDim2.new(0.02,0,0,0)
				Option.Size = UDim2.new(0,98,0,27)
				Option.BackgroundColor3 = Color3.new(1,1,1)
				Option.BackgroundTransparency = 1
				Option.BorderSizePixel = 0
				Option.Text = v
				Option.BorderColor3 = Color3.new(0,0,0)
				Option.TextColor3 = Color3.new(0.8627,0.8627,0.8627)
				Option.Font = Enum.Font.SourceSans
				Option.TextSize = 14
				Option.ZIndex = 111
				Highlight.Name = "Highlight"
				Highlight.Position = UDim2.new(-0.0306,0,0,0)
				Highlight.Size = UDim2.new(0,2,0,27)
				Highlight.BackgroundColor3 = Color3.new(1,1,1)
				Highlight.BorderSizePixel = 0
				Highlight.BorderColor3 = Color3.new(0,0,0)
				Highlight.AutomaticSize = Enum.AutomaticSize.Y
				Highlight.ZIndex = 111
				
				Option.MouseButton1Down:Connect(function()
					SelectedText.Text = v
					DropDownOptions.Visible = false
					options.callback(v)
				end)
			end
			
			SelectedText.MouseButton1Down:Connect(function()
				DropDownOptions.Visible = not DropDownOptions.Visible
			end)
			
			options.callback(options.default)
			
			return dropdown
		end
		
		function tab:NewButton(options)
			local button = {}
			
			local Button = Instance.new('Frame', Canvas)
			local ButtonTitle = Instance.new('TextButton', Button)
			local ButtonCorner = Instance.new('UICorner', Button)

			--Properties

			Button.Name = "Button"
			Button.Position = UDim2.new(0.3338,0,0.6099,0)
			Button.Size = UDim2.new(0,499,0,34)
			Button.BackgroundColor3 = Color3.new(0,0,0)
			Button.BackgroundTransparency = 0.5
			Button.BorderSizePixel = 0
			Button.BorderColor3 = Color3.new(0,0,0)
			Button.ZIndex = 108
			ButtonTitle.Name = "ButtonTitle"
			ButtonTitle.Size = UDim2.new(0,498,0,34)
			ButtonTitle.BackgroundColor3 = Color3.new(1,1,1)
			ButtonTitle.AutoButtonColor = false
			ButtonTitle.BackgroundTransparency = 1
			ButtonTitle.BorderSizePixel = 0
			ButtonTitle.BorderColor3 = Color3.new(0,0,0)
			ButtonTitle.Text = options.Name
			ButtonTitle.TextColor3 = Color3.new(0.851,0.851,0.851)
			ButtonTitle.Font = Enum.Font.Gotham
			ButtonTitle.TextSize = 14
			ButtonTitle.ZIndex = 109
			ButtonCorner.CornerRadius = UDim.new(0,6)
			
			ButtonTitle.MouseButton1Down:Connect(function()
				Library:tween(Button, {BackgroundColor3 = Color3.new(0.756863, 0.756863, 0.756863)})
			end)
			
			ButtonTitle.MouseButton1Up:Connect(function()
				Library:tween(Button, {BackgroundColor3 = Color3.fromRGB(0, 0, 0)})
			end)
			
			ButtonTitle.MouseButton1Click:Connect(function()
				options.callback()
			end)
			
			return button
		end
		
		return tab
	end
	
	return GUI
end


--// services

local players = game:GetService("Players")
local userInputService = game:GetService("UserInputService")
local replicatedStorage = game:GetService("ReplicatedStorage")

--// variables

```
## Create Title
```lua
local lib = Library:CreateWindow({Title = "Saturn"})
```
## Create Tab
```lua
local tab1 = lib:NewTab({Name ="Catching"})
```
## Create Toggle
```lua
tab1:NewToggle({
	Name = "QB Aimbot Z TO CHANGE MODE",
	default = false,
	callback = function(v)
		
	end,
})
```
## Create Dropdown
```lua
tab1:NewDropDown({
    Name = "mag type",
    options = {
        "Blatant",
        "Regular",
        "Legit",
		"League"
    },
	
    default = "Normal",
    callback = function(v)

    end,
})
```
## Create Slider
```lua
tab1:NewSlider({
	Name = "swat reach range laggy",
	min = 1,
	max = 50,
	default = 0,
	callback = function(v)
	autoswatv = v
	
end})
```
## Create Button
```lua
tab1:NewButton({
    Name = "Click Me!",
    callback = function()
        print("Button clicked!")
    end
})
```
