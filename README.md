# Mac-Automator
Anti Afk For Roblox on Mac

Download Hammerspoon, open config and paste this:

local robloxAppName = "Roblox"
local interval = 1080 -- Time between keypresses in seconds (18 minutes)
local timeLeft = interval -- Initialize countdown timer

-- Function to send the "H" keypress to Roblox
local function sendHToRoblox()
    local robloxApp = hs.application.find(robloxAppName) -- Find Roblox app
    if robloxApp then
        local mainWindow = robloxApp:mainWindow() -- Get the main window of Roblox
        if mainWindow then
            -- Bring the Roblox window to focus
            mainWindow:focus()
            
            -- Send the "H" keypress
            hs.eventtap.keyStroke({}, "h", 0)
            
            print("Pressed H in Roblox")
        else
            print("Roblox is running, but no window found.")
        end
    else
        print("Roblox is not running.")
    end

    -- Reset the countdown
    timeLeft = interval
end

-- Countdown Timer Function
local function updateCountdown()
    if timeLeft > 0 then
        print("Time left until next keypress: " .. timeLeft .. " seconds")
        timeLeft = timeLeft - 1
    end
end

-- Set up the timer for keypress and countdown
hs.timer.doEvery(1, updateCountdown) -- Update countdown every second
hs.timer.doEvery(interval, sendHToRoblox) -- Send keypress every `interval` seconds

-- Notify that the script has loaded
hs.alert.show("Hammerspoon: Key H Automation with Countdown Loaded")
