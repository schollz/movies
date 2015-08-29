# IMDB/RT Scraper

The purpose of this program is to download the most recent data from IMDB (which is freely available) and RottenTomatoes.com (which needs to be scraped).

These scripts are simple to use.

First make sure you have no ```movies.db``` file, to begin with.

Then run:

```python dumpIMDB.py```

This script will download the latest ratings archive via FTP, unzip them, process them (to remove TV shows and non-English titles) and then add the relevant information into the database under the ```imdb``` table. This script also generates a list of all the movies it found ```imdb_movies.list``` which is now going to be used to seed the search for movies on the RT website.

Then configure ```rt_server.py``` to use the computers you need, and then run.

## Depreciated

Once the IMDB dump is complete, you can start the RT scrape. The basic command is:

```python dumpRT.py START_INDEX NUM_THREADS THREAD_NUM```

where ```START_INDEX``` is what line in the ```imdb_movies.list``` file you want to start from, ```NUM_THREADS``` defines the number that you want to skip, and ```THREAD_NUM``` is the modulus (should be between 0 and ```NUM_THREADS-1```). The most useful way to run this program is to run several processes at once, such as:

```(nohup python dumpRT.py 0 8 0 &) && (nohup python dumpRT.py 0 8 1 &) && (nohup python dumpRT.py 0 8 2 &) && (nohup python dumpRT.py 0 8 3 &) && (nohup python dumpRT.py 0 8 4 &) && (nohup python dumpRT.py 0 8 5 &) && (nohup python dumpRT.py 0 8 6 &) && (nohup python dumpRT.py 0 8 7 &)```

Any errors will be written to the log files generated. Check those errors - if they are very frequent then it is possible that RT changed its HTML layout and you may have to go into the code to fix those things.

Once that script is done, then you can open Matlab to generate the relevant information and plots by running ```matlab_analysis.m```.

That's it!

## NOTE

The IMDB and RT is **not** free to use. IMDB specifies that their data may be used as long as it is not posted on a forum and only used for academic purposes. Likely RT has similar stipulations.
