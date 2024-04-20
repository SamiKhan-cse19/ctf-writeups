# Banyan Wisdom - 200 points
This problem asks you to find a banyan tree outside Dhaka with very little clue and information.
```
I recently visited a very old Banyan tree (botgach) outside Dhaka. Can you also visit the place and bring me the flag?

N.B. You will know when you see the flag.
```
There is also a hint that unlocks for 50 points, which says:
```
Can you have Wisdom without "knowledge"?
```

## Solution Approach:
The problem asks to visit the place which indicates locating it in Google Maps. Now, there are a limited number of banyan trees in Bangladesh and it is possible to bruteforce search each and every location matching "botgach" and look for the flag. 

But a more practical approach would be to google first to see the locations of the famous banyan trees. Searching "banyan tree bangladesh" shows a bunch of articles about different banyan trees along with their location. Going through this list and searching for the locations in Google Maps will not take much time as the correct article appears within the first page.

![Search Result for "banyan tree bangladesh"](Banyan_Wisdom/Screenshot_2024-04-20_03-04-21.png "Search Result for \"banyan tree bangladesh\"")

**With Hint:**

If you check the hint, you will see that the word "knowledge" has been introduced. Adding this word to the search query further narrows down the results and the blog will appear within the first two or three results.

![Search Result for "banyan tree bangladesh knowledge"](Banyan_Wisdom/Screenshot_2024-04-20_04-21-08.png "Search Result for \"banyan tree bangladesh knowledge\"")

**Going to the Location:**

If you have the location, which is Debhata, Satkhira, you can now go to Maps and search "botgach debhata" and it will take you "Bonbibir Botgach". Now you can simply sort the reviews by newest or search for "iutctf" in the reviews, you will find the flag.

![Maps Search Result](Banyan_Wisdom/Screenshot_2024-04-20_04-12-20.png)
![Reviews](Banyan_Wisdom/Screenshot_2024-04-20_04-14-18.png)

**Flag:** `iutctf{7W45_N07_H4rD_70_F1ND_4F73r_411}`
