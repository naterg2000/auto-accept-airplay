# auto-accept-airplay 
This AppleScript can detect AirPlay notifications and click the Accept button so you don't have to. 

You can customize this script to work with other Mac notifications! You just have to:\

1. change `notificationPhrase` to some text that is in the notification you'd like to interact with\
2. configure the UI Element path in the `try` statement to your notification's UI groups\

These links were very helpful:\
[List UI Elements with AppleScript](https://stackoverflow.com/questions/42231133/use-applescript-to-list-the-names-of-all-ui-elements-in-a-window-gui-scripting)\
[List all UI elements in a window](https://discussions.apple.com/thread/4390028?sortBy=best)

`set notificationPhrase to "would like to AirPlay to this Mac" -- DON'T CHANGE THIS

repeat
	checkNotification(notificationPhrase) -- check for a notification
	delay 1
end repeat

-- check notifications for notificationPhrase
on checkNotification(phrase)
	
	-- fetch static text from a notification banner 
	tell application "System Events"
		set notificationText to the value of (static text ¬
			of group 1 ¬
			of UI element 1 ¬
			of scroll area 1 ¬
			of group 1 ¬
			of window ¬
			of process "NotificationCenter") as text
		
		-- if notificationPhrase is in notificationText, 
		-- interact with notification banner
		if notificationText contains phrase then
			try
				click button 2 of ¬
					group 1 of ¬
					UI element 1 of ¬
					scroll area 1 of ¬
					group 1 of ¬
					window "Notification Center" of ¬
					application process "NotificationCenter" of ¬
					application "System Events"
			end try
		end if
	end tell
end checkNotification`
