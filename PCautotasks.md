Windows is capable of calling and running batch files automatically based on a schedule a user defines.

# Introduction #

Once we have the [FTP data downloading from pH1000s](PCbyethernet.md) and optional [emailing of files to a different location](PCemail.md) figured out it is useful to automatically call the tasks.
In order for this feature to work, the computer must remain on during the time frame that it is expected to be pulling records from the pH1000.

# Details #

By adding **Scheduled Tasks** in Windows the batch scrips can be called automatically.
  1. Open Scheduled Tasks in Windows XP from Start -> Program Files -> Accessories -> System Tools
  1. Add Scheduled Task following the wizard to select the pH1000\_ftp.bat file
  1. Follow the remainder of the wizard, it doesn't matter what options you select for timing.  That will be changed when you get to Open advanced settings when I click finish.
  1. In the advanced features, under schedule set it to run daily and have a start time in the morning.
  1. Then click advanced, and set the task to repeat once every 10 minutes until the end of the working day.  This should be often enough to pull the 100 records from the pH1000 before the memory fills up during high throughput reading of bags.
  1. In settings, click wake computer to run this task.

Add a second task in a similar fashion to do the option emailing feature
  1. Add Scheduled Task following the wizard to select the pH1000\_email.bat file
  1. Follow the remainder of the wizard and for frequency maybe once a week is a good choice.
  1. Again you'll probably want to set the computer to wake up in the advanced settings feature.