# Mac-Automator
Anti Afk For Roblox on Mac

Here’s a clear, step-by-step guide to set up your Hammerspoon script on macOS. It includes all the necessary links and instructions to get started.

---

### **How to Set Up Hammerspoon Script on macOS**

#### Step 1: **Download and Install Hammerspoon**
1. Visit the official Hammerspoon website: [https://www.hammerspoon.org/](https://www.hammerspoon.org/).
2. Click **Download Hammerspoon** to download the `.dmg` installer.
3. Open the downloaded `.dmg` file and drag the Hammerspoon app into your **Applications** folder.
4. Open Hammerspoon from your **Applications** folder.

---

#### Step 2: **Grant Accessibility Permissions**
1. When you open Hammerspoon for the first time, it will ask for **Accessibility permissions**.
2. Go to **System Settings > Privacy & Security > Accessibility**.
3. Click the **+** button and add the **Hammerspoon app** to the list.
4. Enable the checkbox next to Hammerspoon to grant it the necessary permissions.

---

#### Step 3: **Find and Open the Configuration File**
1. Click the Hammerspoon icon in the top menu bar (near the clock) and select **Open Config**.
2. This will open a file named `init.lua` in your default text editor (e.g., TextEdit, VSCode, or Sublime Text).

---

#### Step 4: **Add Your Script**
1. Copy and paste the following script into `init.lua`:

   ```lua
   local robloxAppName = "Roblox"
   local delayInSeconds = 1080 -- Delay between keypresses (18 minutes)
   local timeLeft = delayInSeconds -- Initialize countdown timer

   -- Function to send the "H" keypress to Roblox
   local function sendKeyToRoblox()
       local robloxApp = hs.application.find(robloxAppName) -- Find Roblox app
       if robloxApp then
           local mainWindow = robloxApp:mainWindow() -- Get the main window of Roblox
           if mainWindow then
               -- Bring the Roblox window to focus
               mainWindow:focus()
               
               -- Send the "H" keypress
               hs.eventtap.keyStroke({}, "h", 0)
               
               print("Pressed 'H' in Roblox")
           else
               print("Roblox is running, but no window found.")
           end
       else
           print("Roblox is not running.")
       end
       timeLeft = delayInSeconds -- Reset the countdown after sending the key
   end

   -- Countdown timer to display remaining time in the console
   local function showCountdown()
       if timeLeft > 0 then
           print("Time left until next keypress: " .. timeLeft .. " seconds")
           timeLeft = timeLeft - 10
       elseif timeLeft < 0 then
           -- Reset the timer just in case it went below zero
           timeLeft = 0
       end
   end

   -- Timer to send the keypress
   hs.timer.doEvery(delayInSeconds, sendKeyToRoblox)

   -- Timer to update the countdown every 10 seconds
   hs.timer.doEvery(10, showCountdown)

   -- Notify that the script has loaded
   hs.alert.show("Hammerspoon: Key Automation with Countdown Loaded")
   ```

2. Save the file and close your text editor.

---

#### Step 5: **Reload the Script**
1. Go back to the Hammerspoon menu bar icon.
2. Select **Reload Config** or press `Cmd + Shift + R`.
3. You should see a notification: **Hammerspoon: Key Automation with Countdown Loaded**.

---

#### Step 6: **Test the Script**
1. Make sure Roblox is running.
2. Watch the **Hammerspoon Console** (`Cmd + Shift + C`) for logs, such as:
   - `"Pressed 'H' in Roblox"`
   - `"Time left until next keypress: X seconds"`

---

#### Step 7: **Running the Script**
- As long as Hammerspoon is open, the script will run automatically.
- If you quit Hammerspoon, the script will stop.
- To start it again, reopen Hammerspoon, and it will reload your saved `init.lua` configuration.

---

### Additional Notes
- **To Change the Key or Timing**:
  - Replace `"h"` with any other key you want to send.
  - Change `1080` in `local delayInSeconds` to your desired interval in seconds.

- **To Stop the Script**:
  - Quit Hammerspoon from the menu bar: **Hammerspoon > Quit Hammerspoon**.

- **To Add This Guide to GitHub**:
  - Include this text in your repository’s README file for easy reference.
  - Add your `init.lua` file to the repository as an example.

---

Let me know if you'd like help formatting this guide for GitHub or need further clarification! 🚀
