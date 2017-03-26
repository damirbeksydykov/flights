# southwest-scraper
This Python script will allow you to find cheap roundtrips on Southwest, especially if you have flexible dates of travel (for example, you want to visit your long-distance significant other on any weekend in the next few months).  Since airlines change ticket prices throughout the week, leaving this running will allow you to wait until prices drop under a certain threshold.  Once a suitable flight is found, the script can send you a text message to notify you.  This program is different from others in that it considers multiple different airports and travel dates.

## Installation
### Setup
1. Clone this repository: `git clone https://github.com/n-patel/southwest-scraper`
2. Ensure that you have Python3 and `pip3` installed.
3. Install required modules with `pip3 install -r requirements.txt`
4. [Download](http://phantomjs.org/download.html) PhantomJS and put the executable in this root directory (`southwest-scraper`).
    * Alternatively, you can place the executable in `/usr/local/bin` folder (Mac/Linux) or in your Scripts folder (Windows).
5. Register for a free account on [Twilio](https://www.twilio.com) and get a phone number.

### Configuration
1. Open `config.ini`.  Input your Twilio details (from the [Twilio console](https://www.twilio.com/console)) into the top part of the file.
2. Depending on which option you chose for #3 above, input the appropriate Phantom options (**if you did not take the alternative option, set** `use_custom_phantom_path` **to true**).
3. Scroll to the very bottom of `app.py`.  Input your desired itineraries.

    ```python
    # scan() takes an array of Itineraries
    itins = [Itinerary(...), Itinerary(...)]
    scan(itins)

    # The format of an Itinerary:
    #   [src/dst airports] should look like ["OAK", "SFO"]
    #   [leave/return dates] should look like ["05/13", "05/14", "05/15"]
    #   budget is an integer
    Itinerary([src airports], [dst airports], [leave dates], [return dates], budget)

    # Note 0: If you're only interested in one-way trips, use an empty array [] for [return dates]
    # Note 1: This assumes that you want to return to the same airports you left from.
    ```

### Execution
1. Run `python3 app.py`.  Leave it running, and it will scrape according to the interval you configured and notify you via text for important events (start scraping, stop scraping, found a cheap flight).  You can also put this script on a remote server and leave it running.

## Contributions
Any contributions would be welcome!  Please try to follow the style conventions used throughout the rest of the script (though style changes are appreciated if appropriate -- just be sure to keep everything consistent).  If you find any bugs, please submit an issue and I'll take a look.

## Attributions
I used the Southwest.com scraping logic from [wcrasta's SWA-Scraper](https://github.com/wcrasta/SWA-Scraper).