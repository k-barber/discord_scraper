# K-Barber's Discord Scraper

### Table of Contents

- [K-Barber's Discord Scraper](#k-barber's-discord-scraper)
  - [Table of Contents](#table-of-contents)
  - [Download Link](#download-link)
  - [Using the Scraper](#using-the-scraper)
  - [FAQ](#faq)

-----

### Download Link

[Click Here to download](https://github.com/k-barber/discord_scraper/releases/download/V1.0/K-Barber_Discord_Scraper.zip)

-----

### Using the Scraper

This project is a simple stand-alone Discord channel image scraper. You start it up, enter the URL of the channel you want to scrape, and it pulls down every image that was posted to the channel.

To get started, first [download the program](https://github.com/k-barber/discord_scraper/releases/download/V1.0/K-Barber_Discord_Scraper.zip) and unzip it.

Once it's unzipped, you should see 2 files

- `geckodriver.exe` - a light-weight [Mozilla Firefox](https://github.com/mozilla/geckodriver) browser
- `main.exe` - the scraper itself

![1.jpg](https://raw.githubusercontent.com/k-barber/discord_scraper/main/readme_images/1.jpg)



To start up the scraper, simply open `main.exe`. You should see a Command Prompt window open up and ask you to enter a Discord channel URL. To get a channel's URL, open it up in the [Discord Web App](https://discord.com/app). The URL should look something like this: "https://discord.com/channels/561827776571768833/561830072265474078". Once you've got the link, simply paste it into the window and press `Enter`. 

![2.jpg](https://raw.githubusercontent.com/k-barber/discord_scraper/main/readme_images/2.jpg)

Once you've entered the link you should see a small web browser window pop up, showing the Discord log in screen. You will unfortunately need to enter your username and password each time you scrape a channel because I don't save it.

![3.jpg](https://raw.githubusercontent.com/k-barber/discord_scraper/main/readme_images/3.jpg)

If you look at the Command Prompt window, you'll see that it's waiting for you to finish logging in. When you've logged in, type "Y" to let it know.

![4.jpg](https://raw.githubusercontent.com/k-barber/discord_scraper/main/readme_images/4.jpg)

If the channel you want to scrape is NSFW you'll need to select "Continue" before indicating that you've finished logging in. If you don't, the scraper won't be able to find the channel's scroll bar and will crash.

![5.jpg](https://raw.githubusercontent.com/k-barber/discord_scraper/main/readme_images/5.jpg)

At this point, you can grab a coffee and let the scraper do it's job. When you get back you'll notice that the scraper has created a few more files and folders:

- `geckodriver.log` - the Firefox log file. If something goes wrong, you can upload it [here](https://github.com/k-barber/discord_scraper/issues) and I might take a look at it. Other than that, you can ignore it or delete it once the scraper's done.
- `images.txt` - a list of the image URLs found in the channel. Not really useful at the moment, but if the scraper fails to download the images, this file could (in a future update) be used to retry the download without needing to scroll through the whole channel again.
- `scraped` - a folder containing all the scraped images.

![6.jpg](https://raw.githubusercontent.com/k-barber/discord_scraper/main/readme_images/6.jpg)

If you look inside of the `scraped` folder, you should see all of the channel's images. It may take some time to download them all, depending on how far back the channel's history goes.

![7.jpg](https://raw.githubusercontent.com/k-barber/discord_scraper/main/readme_images/7.jpg)



**That's It!**

Thanks for checking out my program, I hope you enjoy it!



-----

### FAQ

- **Q: How long does it take to scrape a channel?**

  - A: It depends entirely on how long the channel's history is, how large the images are, and how fast your internet is. The scraper doesn't make any extraneous calls, so it should be pretty quick. I tested it by downloading 1,000 images totaling 3.86 GB. The scraper took just over 1.5 hours or 5.7 Mbps.

- **Q: Does the scraper get the thumbnails or the original images?**

  - A: The scraper downloads the original images.

- **Q: Can other users see me scraping the channel?**

  - A: No. Why would I do that to you?

- **Q: Somethings broken.**

  - A: There's really not much code in this application, so there's not much that can break. If something does break, or you think of a new feature, you can create an issue [here](https://github.com/k-barber/discord_scraper/issues)

- **Q: Why do I need to log in every time?**

  - A: There are two things I could do to get around this:

    1. Have the scraper ask you for your username and password
    2. Have you log in and then store the session cookies

    Number 1 would probably make some users nervous, so I don't do it. I'd also have to actually automate the log in process, which could get messy if discord ever asks for a captcha check. I tried number 2, but the cookies didn't last very long so it didn't prove useful.

- **Q: The browser says my connection is not secure, should I be worried about that?**

  - A: in short, no. The connection is not secure because the Firefox browser is being run through [Selenium Wire](https://pypi.org/project/selenium-wire/) which acts as a proxy server. This allows the scraper to see the network traffic between the Firefox scraper and Discord so that it can actually download the images.

- **Q: I don't trust you with my Discord login information.**

  - A: Good, you shouldn't. The scraper (aka my code) does not interact with your username or password at all. You enter your password in the Firefox browser and it encrypts it and sends it to Discord. In theory the scraper could search the network traffic for the password, but the source code is public, and as you can see in lines 66 - 68 of `main.py`, the only requests that the scraper actually looks at are those that have a URL matching an image in the channel.