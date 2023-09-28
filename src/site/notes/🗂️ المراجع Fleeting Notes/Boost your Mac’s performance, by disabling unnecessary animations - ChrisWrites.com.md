---
{"dg-publish":true,"permalink":"/almraje-fleeting-notes/boost-your-mac-s-performance-by-disabling-unnecessary-animations-chris-writes-com/"}
---

Is your Mac running more slowly than when it was shiny and new? Has it become prone to freezing? Or perhaps it seems to be taking *forever* to start up?

When it comes to speeding up an ailing Mac, there’s no shortage of advice out there, but in this article we’ll be covering one of the more *unusual* methods of boosting your Mac’s performance.

By the end of this article, you’ll know how to use Terminal commands plus a third party app, to disable all of macOS’ nice-to-have-but-far-from-essential animations, taking pressure off the processor and ultimately speeding up your Mac.

Disabling these little animated flourishes may not *seem* like it should make a huge difference, but all of these small tweaks can add up a noticeable performance boost. Plus, if your Mac is already struggling to perform an intensive task with the amount of processing power available, then that little animated flourish may be the thing that finally pushes your Mac over the edge, causing it to freeze up completely.

## Disabling animations with the Terminal

You can disable (and enable) a range of macOS animations, using the Terminal application. To access the Terminal:

-   Open a new “Finder” window.
-   Navigate to “Applications/Utilities” and launch the Terminal.

You can now toggle some of macOS’ most frequently-used animations, on and off:

1.  ### Window opening animations
    

To disable window opening animations, copy/paste the following command into the Terminal, and then press the “Enter” key on your keyboard:

defaults write NSGlobalDomain

If you change your mind and want to restore these animations at any point, then copy/paste the following command into the Terminal:

defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool true

Then, press the “Enter” key and the window opening animations will be restored.

### 2\. The resizing animation

This animation occurs when you resize a window, and may also occur when you open or save a file within an application. You can speed up the window resizing animation, creating something that’s slightly choppier, but puts less strain on your Mac’s processor.

To speed up this animation, run the following Terminal command:

defaults write NSGlobalDomain NSWindowResizeTime -float 0.001

If you miss the smooth resizing transition, then you can restore the animation’s default settings, with another Terminal command:

defaults write NSGlobalDomain NSWindowResizeTime -float 0.2

### 3\. The Quick Look window animation

By default, if you select any file or folder on your Mac and press the Space bar, the Quick Look window will expand smoothly across the screen, providing you with a preview of the selected item.

![](https://www.chriswrites.com/wp-content/uploads/removing-the-macOS-quick-look-window.png)

macOS opens the Quick Look window with a smooth animation, but you can remove this transition so that the window simply *appears* onscreen.

To disable the Quick Look animation, copy/paste the following command into the Terminal and then press the “Enter” key on your keyboard:

defaults write -g QLPanelAnimationDuration -float 0

If you change your mind at any point, then you can restore the Quick Look animation to its former glory:

defaults delete -g QLPanelAnimationDuration

Restart your Mac, and the Quick Look animation should be back in action.

### 4\. Launching an app from the Dock

The Dock provides easy access to all of your most frequently-used applications, but every time you launch an application from the Dock, it appears with a brief animation.

To suppress this animation, copy/paste the following command into the Terminal window:

defaults write com.apple.dock launchanim -bool false

To restore this animation, run:

defaults write com.apple.dock launchanim -bool true

## Access hidden system preferences, with TinkerTool

You can also disable animations using the free TinkerTool application, which grants you access to some of macOS’ hidden system settings:

-   Head over to the TinkerTool website and [download the correct version of TinkerTool](http://www.bresink.com/osx/TinkerToolOverview.html) for your version of macOS.
-   Once the file has downloaded, launch it and follow the onscreen instructions to install.
-   Read the warning, and if you’re happy to proceed then click “Understood.” This will launch the main TinkerTool interface.

![](https://www.chriswrites.com/wp-content/uploads/access-hidden-system-preferences-tinkertool.png)

You can then use TinkerTool to disable a range of animations:

-   **Finder animations.** Select the “General” tab and then disable the following: “Animation opening info panels and Desktop icons,” and “Animation selecting info panel categories.” To apply your changes, select the “Relaunch Finder” button.
-   **Dock animations.** Select the “Dock” tab and deselect the following: “Disable animation when hiding or showing Dock.” To apply your changes, select “Relaunch Dock.”
-   **Launchpad animations.** Select the “Launchpad” tab and deselect one, some or all of the following: “Disable fade-in effect when opening,” “Disable fade-out effect when closing,” and/or “Disable animation when switching between pages.” When you’re happy with your choices, select “Relaunch Dock.”
-   **Rubberband scrolling.** This is an overscrolling effect that can occur when you scroll past the window’s scrollable region. To remove this scrolling animation, select the “General” tab and then select the “Disable rubber band scrolling” checkbox. While you’re in the “General” tab, you may also want to disable the following animation effects: “Accelerate animation when rolling out sheets,” and “Animate opening windows.” To see your changes in action, log out of your user account and then log back in again.

If at any point you want to restore macOS’ default settings, then:

-   Select TinkerTool’s “Reset” tab.
-   Select either “Reset to pre-TinkerTool state,” or “Reset to defaults.”
-   Log out of your user account, and then log back in; your Mac’s original animations should have now been restored.

### Before you go

After spending over 20 years working with Macs, both old and new, theres a tool I think would be useful to every Mac owner who is experiencing performance issues.

[CleanMyMac](https://www.chriswrites.com/go/cleanmymac-x/) is highest rated all-round cleaning app for the Mac, it can quickly diagnose and solve a whole plethora of common (but sometimes tedious to fix) issues at the click of a button. It also just happens to resolve many of the issues covered in the speed up section of this site, so [Download CleanMyMac](https://www.chriswrites.com/go/cleanmymac-x/) to get your Mac back up to speed today.

![mac-pc](https://www.chriswrites.com/wp-content/uploads/testimg.jpg)

  

#### About the author

![](https://secure.gravatar.com/avatar/b99125f96641b98c416060552cb35d70?s=140&d=mm&r=g)

Jessica Thornsby is a technical writer based in Sheffield. She writes about Android, Java, Kotlin and all things Apple. She is the co-author of O'Reilly's "iWork: The Missing Manual," and the author of "Android UI Design," from Packt Publishing.