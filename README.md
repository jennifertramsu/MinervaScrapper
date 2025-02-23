# MinervaScraper

<p> Because it takes effort to log onto Minerva and navigate through the different webpages to see my grades only to realize that they haven't been uploaded yet. </p>

## Usage

### Requirements
<p> This program currently supports four browsers: <b> Chrome, Edge, Firefox, and Brave </b>. Your browser of interest should be indicated in the .env file. This script now supports webdriver-manager functionalities, and so the drivers' version is automatically checked and updated when the script is called. All drivers are saved in the folder Drivers.

<p> To download all required dependencies, navigate to Minerva's parent directory and pip install requirements.txt. </p>

        pip install -r requirements.txt

<h3> .env file </h3>
<p> Login credentials are retrieved from a .env file, stored in the same directory as the script. Create a .env file following the format below: </p>
<ul>
    <li> Set LOGIN=1 for ID login or LOGIN=0 for email login </li>
    <li> Set BROWSER to indicate your preferred browser </li>
</ul>
              
        # .env

        LOGIN={0, 1}

        BROWSER={CHROME, EDGE, FIREFOX, BRAVE}

        MCGILLID={insert ID here} # can exclude if LOGIN=0
        MINERVAPIN={insert PIN here} # can exclude if LOGIN=0

        MCGILLUSERNAME={insert McGill email here} # can exclude if LOGIN=1
        MCGILLPASSWORD={insert password here} # can exclude if LOGIN=1
        
        EMAIL={insert sender email here}
        PASS={insert sender email password here}

        MYEMAIL={insert recipient email here}
        
        NAME={Your name, so it feels a bit more personalized when email addresses you :D}

<p> For security reasons, it's recommended to create a throwaway email account and use its credentials for EMAIL and PASS. This script was tested using GMAIL. As Google no longer allows access from insecure sources (valid), an App Password must be generated under <a href=https://www.emailsupport.us/blog/gmail-smtp-not-working/> 2FA </a>. </p>

<h3> MinervaScrape </h3>

<p> To use from the command-line: </p>
<ul>
    <li> Navigate to the directory Minerva (assuming currently in MinervaScraper) </li>
</ul>
  
        cd Minerva

<ul>
    <li> Run the command python minervascraper.py with no arguments to scrape for all terms </li>
</ul>
              
        python minervascraper.py

<ul>
    <li> Run the command python minervascraper.py ARG1 ARG2 etc... to scrape for specified terms </li>
</ul>
              
        python minervascraper.py f2019 w2020 s2020 F2020

<p> Arguments are case-insensitive and can be passed in any order (time-independent). They take the form TERM + YEAR, where TERM is represented by a single letter, and YEAR has the form yyyy. </p>
<ul>
    <li> S/s --> Summer </li>
    <li> F/f --> Fall </li>
    <li> W/w --> Winter </li>
    <li> Example: </li>
    <ul>
        <li> f2019 and F2019 are equivalent for Fall term, 2019 </li>
    </ul>
</ul>
<p> Output is written to an output file named Scraped_Transcript_TERM1_TERM2.json if terms are specified, or to Scraped_Transcript_All_Terms.json if none are specified. </p>

<h3> GradeUpdate </h3>
<p> There are two ways to check for transcript updates. The only reason why two ways exist is because I was bored, so really, there's only one (useful) way. </p>

<b> (1) </b> Flag for a one-time update with minervascrape.py
              
    python minervascraper.py -u

    python minervascraper.py --update

<b> (2) </b> Periodically call gradeupdate.py
<p> By making use of external schedulers, gradeupdate.py will run the scraper at prescribed intervals and send an email when a change (grade, course average) is present on Minerva's unofficial transcript, excluding changes related to add/drop (because you probably don't care about that). The email will contain a formatted table that describes these changes. </p>
<ul>
    <li> MacOS, Linux </li>
    <ul>
        <li> Schedule through crontab </li>
    </ul>
    <li> Windows </li>
    <ul>
        <li> Windows task scheduler </li>
        <ul>
            <li> PROGRAM : path to python.exe </li>
            <li> ARGUMENTS : path to gradeupdate.py </li>
            <li> START IN : path to folder holding gradeupdate.py (Minerva) </li>
        </ul>
    </ul>
</ul>

<p> When the scraper is enabled on a schedule, it saves all output into a logfile ('minerva_log.txt'). </p>

## To-Do:
<ul>
    <li> ¯\_(ツ)_/¯ </li>
    <li> Find a better system to send periodic updates. </li>
</ul>
