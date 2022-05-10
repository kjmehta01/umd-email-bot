# Meet the UMD email bot, designed for The Diamondback :robot:

## About the bot
For my final project in JOUR328O, I set out to build a reporting tool that could instantly notify The Diamondback newsroom’s Slack when a new campus message – or email from the president’s office – was dispatched.

The app can help the newsroom break news quickly, but its need comes in large part from the university’s switch to only sending these messages to university email addresses.

Many students – and Diamondback reporters – aren’t checking those emails nearly as frequently as they might check other emails. Plus, the emails don’t come at the same time for each email address. Thus, it was necessary to find a way to pull each email by bypassing the inconsistent email system that often goes unchecked.

Scraping the campus messages from the university website allows The Diamondback to see each message as soon as it starts to exist on the page of the university’s website. When the Slack bot identifies a new message, it scrapes the data from the website, pulling the email title, link, date and description. The bot then delivers an alert to Slack with a link to the full email, the title and date of the email. In a thread, the bot replies to the alert message with the beginning of the email so reporters and editors alike can get a sense of the email just from Slack itself.

The bot also links to a csv in GitHub that holds the recent data and source of the data, so users can explore these elements quickly and instantly. These links, especially the csv of breaking news could be useful at a time when we’re seeing a series of breaking news announcements. For example, this would have been useful amid rapid changes in COVID-19 restrictions.

The link to the full email appears multiple times to accommodate different types of users. In both cases, the users are reporters or editors on The Diamondback staff. But the message might come to users while they are in different positions. Some users, who might be on their laptops, might choose to read the entire email immediately. This user will click to view the full email immediately in the first message. But there are other users, who might be walking to class and experiencing spotty wifi while on mobile. In this scenario, these users will just want to read the details of the thread. This user might grow curious and become interested in reading the complete email, but with a spotty connection – it could take a lot of loading power to navigate in and out of the thread.

From a visual perspective, the bot includes an envelope icon and The Diamondback logo sitting inside of the envelope. The app icon – covered in “Diamondback red”, black and white – mimics the appearance of another Slack bot, aptly named “Diamondbot,” who lives in The Diamondback Slack. The two are intentionally similar, but not too similar so that the user can distinguish messages from Diamondbot and this UMD email bot.

## The journey (and all of the roadblocks)

Over the course of creating this project, I ran into an expanse of problems. First, I had trouble figuring out the relationship between the yml file and Python. At a point, I remember seeing more than 90 GitHub Actions failed messages fill my inbox. I tried to do too much with the yml file, but I later moved the actions I tried to do in the yml file into Python. Specifically, in Python, I added code that would only send Slack messages if there was new data, rather than turning to the yml file to try to do this.

Another major hiccup in the same vein was ensuring that I loaded in all of my libraries in the yml file. Since this class was the first time I began exploring yml files, I did not realize that I would need to load every single library that I was using Python in my yml file. Once I loaded in each library, the scrape was able to run error-free.

I also initially struggled to connect to Slack. In an old repository for my first Slack bot, I was able to get the same bot to run, but I struggled to get the email bot to run in Slack. Once I indicated the channel in the yml and pulled the correct token from Slack, I was able to begin sending messages in Slack from my new email bot repository.

I used BeautifulSoup to scrape the data, which came to me pretty easily. However, one day, when I sat down to make progress on the app, I found that all of the lists I had created were empty. I could not figure out why, at first, but when I double-checked what I had against the web page’s source code, I found that the HTML backing the message page on the university website had changed. It took some time, but I was able to adjust all of the code to the newly named sections, among other HTML elements.

In extracting the data into a data frame, I used Pandas. But I ran into a problem where I was listing all of the column names as numbers and all of the row labels as numbers. I knew I wanted to include labels for the columns, but I spent hours searching for a way to do this. Once I finally sorted that out, I wondered how I couldn’t figure it out earlier. It was as easy as “df.columns = [‘column’, ‘names]. Adding in the labels made it a lot easier to parse the data and read my code.

Throughout the project, I sought to revamp it in some ways. And I’m still thinking about ways that I could do that. One thing that I sought to do was use natural language processing to scan each email for names. Unfortunately, the recognition wasn’t impressive. You can see that code, and other attempts that didn’t make it into the final, on a spare file called “tries.py.” Another file, try.py, illustrated an attempt to simplify the code and reduce the creation of csvs by relying on dictionaries instead. I ultimately stuck with the csv option since it was easiest for me to test with, but in a later iteration, I am interested in continuing to work on this.

I also considered the value of integrating more of a database than the linked csv on GitHub. Here’s a [Datasette app](https://troubled-silken-tyrannosaurus.glitch.me/) that demonstrates what that database could look like. Right now, the bot holds a small amount of recent data and delivers it to [data.csv](https://github.com/rinatorch/umd-email-bot/blob/main/Code/data.csv) in this repository.

## Reflecting and moving forward

Looking ahead, I worry that changes to the HTML might surface again and render the bot useless. However, I am confident that I could figure out how to change the scrape to meet any changes in the HTML. But if the HTML remains the same, there should never be a need to sunset it, but folks should keep an eye on HTML changes and link changes when maintaining this bot.

On a personal level, this app feels like a culmination of the Python skills I’ve learned and picked up along the way. It’s wild just how much dictionaries, lists, for loops, Pandas and BeautifulSoup can do when you bring them all together. I’ve got a ways to go when it comes to building apps for efficiency and am planning to keep working at that. But in the meantime, I’m eager to deploy this bot to The Diamondback newsroom. I am confident it will be a useful tool that can outlive my time at the publication.
