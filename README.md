# Windows Terminal Default Tabs

Here's how one can go about opening multiple default tabs with different staring locations in *Windows Terminal*.

![Demo](https://raw.githubusercontent.com/btebbens/windows-terminal-default-tabs/main/demo.png)

## Configure Profiles

A *Windows Terminal Profile* must be configured for each _unique_ tab. In my case, I needed 3 profiles; one for each repo I was working in. A profile may be used in more than one tab/pane.

1) Open `Settings` and click *Add a new profile*
2) Select a profile to duplicate (Usually `PowerShell`) and click *Duplicate*
3) Change the `Name`, `Starting directory`, `Icon`, and/or other settings as desired and click *Save*
4) Repeat for additional _unique_ tabs

## Configure Startup

*Windows Terminal* has a `startupActions` property that is configured in `settings.json`. This takes a list of semicolon-separated arguments for *Windows Terminal* (Run `wt.exe --help` if curious).

1) Define your desired workflow
2) Open `Settings` and click *Open JSON file*
3) Add `"startupActions": ""` to the root json object
4) Add commands to `startupActions`

In my case, I wanted 3 tabs with the last tab containing 3 panes, so my `startupActions` looked like this:

`"new-tab -p \"PowerShell App1-Profile\" ; new-tab -p \"PowerShell App2-Profile\"; new-tab -p \"PowerShell App3-Profile\" ; split-pane -p \"PowerShell  App3-Profile\" ; split-pane -v -p \"PowerShell  App3-Profile\""`

Broken down is this list of commands:
- `new-tab -p \"App1 Profile\"` opens the first tab to my `App1-Profile` 
- `new-tab -p \"App2 Profile\"` opens the second tab to `App2-Profile`
- `new-tab -p \"App3 Profile\"` opens the third tab to `App3-Profile`
- `split-pane -p \"App3 Profile\"` creates a pane in the right 50% on the third tab
- `split-pane -v -p \"App3 Profile\"` creates a pane int the bottom 50% of the right side on the third tab
