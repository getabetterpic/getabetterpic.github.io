---
layout: post
title: An Order Form in 2 Weeks
date: '2012-08-22T21:08:00.000-04:00'
author: Daniel Smith
tags:
- VBA
- COM
- VB
- order form
- Oracle
- credit card
- VSTO
- Excel
- DES
- add-in
- Visual Basic
- credit card validation
- Quoting
- encryption
- Visual Studio
modified_time: '2012-08-22T21:08:19.840-04:00'
blogger_id: tag:blogger.com,1999:blog-358950712929443967.post-3338480259833870090
blogger_orig_url: http://www.getabetterpic.com/2012/08/an-order-form-in-2-weeks.html
---

One day the CFO walks by my cube, stops, and comes back to me. "Do you think you could learn .NET in 48 hours?" he asks. "Um, sure," I reply. Little did I know this would start a crazy two weeks for me. Thankfully I had 2 weeks and not 48 hours.<br /><br />Up until this point, our dealers would log onto an externally-facing Oracle website and enter equipment orders through Oracle Quoting. But we were paying a good bit of money every year to maintain support on Quoting in case anything should go wrong. About a month before the support agreement was to come due, the higher-ups decided not to renew, so we needed to come up with an alternative where the dealers could enter equipment orders, and we needed to come up with it quick. So I got to work.

I quickly designed a simple order form in an Excel spreadsheet. I realized it wasn't the best possible way to go about it, but it was the quickest I knew of. I made the order form as full-featured as I could, including drop downs for part numbers, look-ups based off of related accessories, and automatically-populating prices based off a separate, hidden worksheet. Then came the fun part.

How do you enter credit card information in an Excel spreadsheet without exposing the information to prying eyes? My first thought was to encrypt the information into the spreadsheet using a VBA function. However, to encrypt/decrypt, you need a password. And although VBA projects can be locked, they are infamous for the ease by which the project lock can be picked. So that was ruled out.

My second, "brilliant" idea was to encrypt the information using an add-in. Add-ins have the benefit of being more secure than VBA, yet offering a lot of the same functionality. So I got to work. My first attempt at creating an add-in was to use a Visual Studio Tools for Office (VSTO) add-in. So I got to work coding, Googling, and generally trying to figure out how to get it to work. After about a week of coding and troubleshooting, I had a working product. So we began the deployment phase.

Unfortunately, I had overlooked one small detail. The VSTO add-in only worked in Excel 2007, and a lot of our dealers only had Excel 2003. Also, I felt the VSTO add-in was cumbersome in how it installed, and the Excel workbook had to be tied directly to the add-in. So I decided to redesign the add-in as a basic COM add-in instead. The idea was to have a dead-simple install process, and the ability to send out fresh Excel workbooks with updated information without the need to constantly update the add-in associated with it. So the add-in itself only contained the program necessary to encrypt the credit card information. All other functions (such as where to place the encrypted information, the input information to encrypt, etc.) were housed in the workbook through VBA functions and calls.

Side note: I also coded a credit card validation method in VBA to avoid fat-fingered credit card numbers from being treated as valid.

Keep in mind I had never used Visual Studio before, I had never coded a COM add-in (or any other add-in for that matter), I was trying to figure out how to get the code signed through the company's IT department, and, oh yeah, I was studying for the Georgia bar exam at the same time. Having that many learning curves going made for a miserable couple of weeks for my wife.

The good news is, after another week I was able to roll out a COM add-in that had been signed by the IT department and deployed it to the dealers. There were a few bugs that came up we had to fix, mostly dealing with what dependencies we included in the installer and where, but now things seem to be smooth sailing, at least for the time being.

Moral of this story: If the CFO asks if you can learn something in 48 hours, be prepared to dig in and knowledge up.</div>