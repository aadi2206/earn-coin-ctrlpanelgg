# Installation Guide

Before deploying the CtrlPanel.GG Earn Coin System to your production server, it’s wise to download all the necessary files from this repository to your local computer. This will allow you to configure and customize the system as needed before going live. Follow these steps to get started:

## Step 1: Clone the Repository

1. Open your terminal or command prompt.

2. Navigate to the directory where you want to store the system files on your server using the `cd` command.
   [Recommended: First Download it on your Computer, Edit and then upload **OR** Do by copy-pasting in the commands given in the installation guide]
   
4. Clone the repository by running the following command:

   ```shell
   git clone https://github.com/aadi2206/earn-coin-ctrlpanelgg.git

   ```

## Step 2: Configuring The File For Linkvertise

1. Open up the EarnController.php which can be found in /var/www/ctrlpanel/app/Http/Controllers.

2. Use This for Direct Access:
```shell
nano /var/www/ctrlpanel/app/Http/Controllers/EarnController.php

```

4. Change `$dailyLimit` to the amount of daily how many links are generated per user.

5. Change `$timezone` to your timezone, you can find your timezone at https://en.wikipedia.org/wiki/Time_zone

6. Replace `Your_CtrlPanel_Domain` with the Domain of your CtrlPanel. !!!Do NOT ADD A / !!!

7. Replace `https://link-to.net/` with your Direct Ad Link, Generate it First.

8. Replace `Your_Publisher_ID` with your Linkvertise Publisher ID which you can find in the Full Script API Section. (Numerical Code in the HTML Code)

9. Change the Variable `$reward` to the Number of Coins you want to give a user for an ads session. The default is 30. `($reward = 30;)`

10. Save the File.

## Step 3: Configuring The File For Google Adsense

1. Open up the EarnController.php which can be found in /var/www/ctrlpanel/app/Http/Controllers.

2. Use This for Direct Access:
```shell
nano /var/www/ctrlpanel/app/Http/Controllers/EarnController.php

```

4. Change the Variable `$reward_a` to the Number of Coins you want to give a user for an ads session. The default is 5. `($reward_a = 5;)`

5. Save the File.

6. **Note:** Create a Folder Named Earn or paste this code:
```shell
mkdir /var/www/ctrlpanel/resources/views/earn/
```

8. Open up the adpage.blade.php which can be found in /var/www/ctrlpanel/resources/views/earn/.

9. Use This for Direct Access:
```shell
nano /var/www/ctrlpanel/resources/views/earn/adpage.blade.php
```

10. Replace every placeholder “xxxxxxx” with the variables you get from Adsense

11. Save the File.

## Step 4: Configuring The File For ClickCoins

1. Open up the EarnController.php which can be found in /app/Http/Controllers.

2. Use This for Direct Access:
```shell
nano /var/www/ctrlpanel/app/Http/Controllers/EarnController.php

```

4. Change the Variable `$clickcoinReward` to the Number of Coins you want to give a user for a click. The default is 1. `$clickcoinReward = 1`

5. Change the Variable `$minTimeBetweenClicks` to the Amount you want the second to wait after each Click. The default is 60. `$minTimeBetweenClicks = 60`

6. Replace $clickcoinLink = 'your direct ad link'; with your ads direct link.

7. Save the File.

## Step 5: Add the Routings and the Navigation and do the last steps.

1. Open up the web.php file which can be found in /var/www/ctrlpanel/routes/. (This is in your CtrlPanel Installation)

2. Use This for Direct Access:
```shell
nano /var/www/ctrlpanel/routes/web.php

```

4. Add this code to the Top of the Web.php:

   ```shell
   use App\Http\Controllers\EarnController;

   ```

5. Add this code under the Line
```shellRoute::post('/voucher/redeem', [VoucherController::class, 'redeem'])->middleware('throttle:5,1')->name('voucher.redeem');```

   ```shell
   Route::get('/earn', [EarnController::class, 'index'])->name('earn.index');
   Route::get('/earn/lv', [EarnController::class, 'start'])->name('earn.start');
   Route::get('/earn/ad', [EarnController::class, 'adsense'])->name('earn.adsense');
   Route::get('/earn/clickcoin', [EarnController::class, 'clickcoin'])->name('earn.clickcoin');
   Route::view('/adblocker-found', 'adblocker_found')->name('adblocker_found');

   Route::get('/earn/adpage', [EarnController::class, 'timerPage'])->name('earn.adpage');
   Route::get('/earn/return', [EarnController::class, 'redirectToEarnIndex'])->name('earn.return');
   Route::get('/redeem', [EarnController::class, 'redeem'])->name('earn.redeem');

   ```

6. Save the File.

7. Now Upload this all Files to ```/var/www/ctrlpanel```. (Only if you've done the changes of code in localhost not directly in Server's Folder)

8. Run these command's in the ctrlpanel directory.
   ```shell
   cd /var/www/ctrlpanel && php artisan view:clear && php artisan config:clear && chown -R www-data:www-data /var/www/ctrlpanel/*
   ```

## Hurray, Your System is Successfully Installed.

