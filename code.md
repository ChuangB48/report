# 程式碼
我這次用了四個我從來沒用過的語法:`GetAsyncKeyState`、`system("cls")`、`Sleep`和`thread`。

`GetAsyncKeyState`可以用來判斷使用者按下的按鈕，像我一開始就是判斷使用者按下enter鍵後跑下一步。

    while (true){
        if(GetAsyncKeyState(0x0D)&0x8000){
            system("cls");
            play();
        }
    }
*一直無限迴圈讓他跑，跑到偵測到使用者按下enter鍵*

`system("cls")`和`Sleep`一個是可以清除畫面上所有已經印出來的東西，另一個則是可以讓程式暫停一段時間。像我畫面更新就是先把畫面清掉，然後印上我要的，然後停一段時間。

    system("cls");
    cout << "health:" << health << '\n' << "score:" << score << '\n' << output;
    Sleep(150);
*清除後輸出，然後停150毫秒後繼續跑*

接下來是算字母位置，我用一個vector存，裡面有三個東西，字元、x軸和y軸。然後x軸不會動，y軸每次加一。

    vector <pair<char,pair<int,int>>> p;
*vector裡面有一個pair，pair的第一項有一個char用來存字母，第二項又是一個pair，裡面有兩個int用來存位置*

`thread`則是可以讓函式平行在跑，因為我遊戲介面有兩個無線迴圈，一個要更新畫面，一個要判斷使用者的動作。因為是無限迴圈，正常來說一定有一個跑不到。所以我就是用`thread`的`detach()`來讓他們一起跑。

    thread button(press);
    button.detach();
*設button為函式press()，然後button自己去旁邊跑，主程式繼續*

最後有分數系統和血量系統，反正兩個很像，不過血量到玲就停止遊戲。

[返回](lobby.md)