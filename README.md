# utl-compute-the-date-and-time-of-peak-full-moons-for-any-year-python-package-ephem
Compute the date and time for full moons for any year python package ephem
    %let pgm=utl-compute-the-date-and-time-of-peak-full-moons-for-any-year-python-package-ephem;

    %stop_submission;

    Compute the date and time for full moons for any year python package ephem

    TWO SOLUTIONS  (2 python imterfaces)

          1 utl_submit_py64_310
          2 utl_pybeginx & utl_py
          3 should be possible to run the python using sas FCMP and a Python package
            I could not get it to work.

    Theree are some sophisticated astronomical packages in python?

    INPUT
    =====

    %let yr=2025;

    OUTPUT
    ======

      peak datetime_full_moons (about each 30 days?)

    0   2025-01-13 15:26:51
    1   2025-02-12 06:53:19
    2   2025-03-13 23:54:35
    3   2025-04-12 17:22:12
    4   2025-05-12 09:55:52
    5   2025-06-11 00:43:45
    6   2025-07-10 13:36:42
    7   2025-08-09 00:54:58
    8   2025-09-07 11:08:49
    9   2025-10-06 20:47:33
    10  2025-11-05 06:19:15
    11  2025-12-04 16:14:00

    github
    https://tinyurl.com/42me2x5u
    https://github.com/rogerjdeangelis/utl-compute-the-date-and-time-of-peak-full-moons-for-any-year-python-package-ephem

    stackoverflow r
    https://tinyurl.com/m6u9r7rd
    https://stackoverflow.com/questions/79715775/how-to-calculate-full-moon-dates-with-lubridate-in-r

    /**************************************************************************************************************************/
    /* INPUT           | PROCESS                                                               |  OUTPUT                      */
    /* =====           | =======                                                               |  ======                      */
    /* %let yr=2025;   | 1 MACRO %UTL_SUBMIT_PY64_310                                          |                              */
    /*                 | =============================                                         |                              */
    /*                 |                                                                       |                              */
    /*                 | proc datasets lib=sd1 nolist nodetails;                               |  PYTHON                      */
    /*                 |  delete pywant;                                                       |       datetime_full_moon     */
    /*                 | run;quit;                                                             |  0   2025-01-13 15:26:51     */
    /*                 |                                                                       |  1   2025-02-12 06:53:19     */
    /*                 | %utl_submit_py64_310('                                                |  2   2025-03-13 23:54:35     */
    /*                 | import ephem;                                                         |  3   2025-04-12 17:22:12     */
    /*                 | import datetime;                                                      |  4   2025-05-12 09:55:52     */
    /*                 | import pandas as pd;                                                  |  5   2025-06-11 00:43:45     */
    /*                 | exec(open("c:/oto/fn_pythonx.py").read());                            |  6   2025-07-10 13:36:42     */
    /*                 | have,meta = ps.read_sas7bdat("d:/sd1/have.sas7bdat");                 |  7   2025-08-09 00:54:58     */
    /*                 | def get_full_moons_in_year(year):;                                    |  8   2025-09-07 11:08:49     */
    /*                 | .   moons = [];                                                       |  9   2025-10-06 20:47:33     */
    /*                 | .   # Start from the last day of the previous year;                   |  10  2025-11-05 06:19:15     */
    /*                 | .   date = ephem.Date(datetime.date(year - 1, 12, 31));               |  11  2025-12-04 16:14:00     */
    /*                 | .   end_date = ephem.Date(datetime.date(year + 1, 1, 1));             |                              */
    /*                 | .   while date <= end_date:;                                          |  SAS                         */
    /*                 | .       date = ephem.next_full_moon(date);                            |                              */
    /*                 | .       local_date = ephem.localtime(date);                           |  Obs  DATETIME_FULL_MOON     */
    /*                 | .       if local_date.year == year:;                                  |                              */
    /*                 | .           moons.append(local_date.strftime("%Y-%m-%d %H:%M:%S"));   |   1   2025-01-13 15:26:51    */
    /*                 | .   return moons;                                                     |   2   2025-02-12 06:53:19    */
    /*                 | full_moons = get_full_moons_in_year(&yr);                             |   3   2025-03-13 23:54:35    */
    /*                 | print(full_moons);                                                    |   4   2025-04-12 17:22:12    */
    /*                 | df = pd.DataFrame(full_moons, columns=["datetime_full_moon"]);        |   5   2025-05-12 09:55:52    */
    /*                 | print(df);                                                            |   6   2025-06-11 00:43:45    */
    /*                 | fn_tosas9x(df,outlib="d:/sd1/",outdsn="pywant",timeest=3);            |   7   2025-07-10 13:36:42    */
    /*                 | ');                                                                   |   8   2025-08-09 00:54:58    */
    /*                 |                                                                       |   9   2025-09-07 11:08:49    */
    /*                 | libname sd1 "d:/sd1";                                                 |  10   2025-10-06 20:47:33    */
    /*                 | proc print data=sd1.pywant;                                           |  11   2025-11-05 06:19:15    */
    /*                 | run;quit;                                                             |  12   2025-12-04 16:14:00    */
    /*                 |                                                                       |                              */
    /*                 |                                                                       |                              */
    /*------------------------------------------------------------------------------------------------------------------------*/
    /*                 |                                                                       |                              */
    /* * clipboard;    | 2 MACROS UTL_PYBEGINX AND UTL_PYENDX                                  |  PYTHON                      */
    /* filename clp    | ====================================                                  |       datetime_full_moon     */
    /*   clipbrd;      |                                                                       |  0   2025-01-13 15:26:51     */
    /* data _null_;    | proc datasets lib=sd1 nolist nodetails;                               |  1   2025-02-12 06:53:19     */
    /*  file clp;      |  delete pywant;                                                       |  2   2025-03-13 23:54:35     */
    /*  yr=2025;       | run;quit;                                                             |  3   2025-04-12 17:22:12     */
    /*  put yr;        |                                                                       |  4   2025-05-12 09:55:52     */
    /* run;quit;       | %utl_pybeginx;                                                        |  5   2025-06-11 00:43:45     */
    /*                 | parmcards4;                                                           |  6   2025-07-10 13:36:42     */
    /*                 | import ephem                                                          |  7   2025-08-09 00:54:58     */
    /*                 | import datetime                                                       |  8   2025-09-07 11:08:49     */
    /*                 | import pandas as pd                                                   |  9   2025-10-06 20:47:33     */
    /*                 | import pyperclip                                                      |  10  2025-11-05 06:19:15     */
    /*                 | exec(open('c:/oto/fn_pythonx.py').read())                             |  11  2025-12-04 16:14:00     */
    /*                 | have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat')                  |                              */
    /*                 | txt = pyperclip.paste()                                               |  SAS                         */
    /*                 | print(txt)                                                            |                              */
    /*                 | yr=int(txt.strip())                                                   |  Obs  DATETIME_FULL_MOON     */
    /*                 | print(yr);                                                            |                              */
    /*                 | def get_full_moons_in_year(year):                                     |   1   2025-01-13 15:26:51    */
    /*                 |     moons = []                                                        |   2   2025-02-12 06:53:19    */
    /*                 |     # Start from the last day of the previous year                    |   3   2025-03-13 23:54:35    */
    /*                 |     date = ephem.Date(datetime.date(year - 1, 12, 31))                |   4   2025-04-12 17:22:12    */
    /*                 |     end_date = ephem.Date(datetime.date(year + 1, 1, 1))              |   5   2025-05-12 09:55:52    */
    /*                 |     while date <= end_date:                                           |   6   2025-06-11 00:43:45    */
    /*                 |         date = ephem.next_full_moon(date)                             |   7   2025-07-10 13:36:42    */
    /*                 |         local_date = ephem.localtime(date)                            |   8   2025-08-09 00:54:58    */
    /*                 |         if local_date.year == year:                                   |   9   2025-09-07 11:08:49    */
    /*                 |             moons.append(local_date.strftime("%Y-%m-%d %H:%M:%S"))    |  10   2025-10-06 20:47:33    */
    /*                 |     return moons                                                      |  11   2025-11-05 06:19:15    */
    /*                 | full_moons = get_full_moons_in_year(yr)                               |  12   2025-12-04 16:14:00    */
    /*                 | print(full_moons)                                                     |                              */
    /*                 | df = pd.DataFrame(full_moons, columns=['datetime_full_moon'])         |                              */
    /*                 | print(df)                                                             |                              */
    /*                 | fn_tosas9x(df,outlib='d:/sd1/',outdsn='pywant',timeest=3);            |                              */
    /*                 | ;;;;                                                                  |                              */
    /*                 | %utl_pyendx;                                                          |                              */
    /*                 |                                                                       |                              */
    /*                 | libname sd1 "d:/sd1";                                                 |                              */
    /*                 | proc print data=sd1.pywant;                                           |                              */
    /*                 | run;quit;                                                             |                              */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

     %let yr=2025;


    /**************************************************************************************************************************/
    /*  %let yr=2025;                                                                                                         */
    /**************************************************************************************************************************/

    /*         _   _             _               _ _                  __   _  _    _____ _  ___
    / |  _   _| |_| |  ___ _   _| |__  _ __ ___ (_) |_   _ __  _   _ / /_ | || |  |___ // |/ _ \
    | | | | | | __| | / __| | | | `_ \| `_ ` _ \| | __| | `_ \| | | | `_ \| || |_   |_ \| | | | |
    | | | |_| | |_| | \__ \ |_| | |_) | | | | | | | |_  | |_) | |_| | (_) |__   _| ___) | | |_| |
    |_|  \__,_|\__|_|_|___/\__,_|_.__/|_| |_| |_|_|\__|_| .__/ \__, |\___/   |_| _|____/|_|\___/
                   |___|                             |__|_|    |___/            |__|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_submit_py64_310('
    import ephem;
    import datetime;
    import pandas as pd;
    exec(open("c:/oto/fn_pythonx.py").read());
    have,meta = ps.read_sas7bdat("d:/sd1/have.sas7bdat");
    def get_full_moons_in_year(year):;
    .   moons = [];
    .   # Start from the last day of the previous year;
    .   date = ephem.Date(datetime.date(year - 1, 12, 31));
    .   end_date = ephem.Date(datetime.date(year + 1, 1, 1));
    .   while date <= end_date:;
    .       date = ephem.next_full_moon(date);
    .       local_date = ephem.localtime(date);
    .       if local_date.year == year:;
    .           moons.append(local_date.strftime("%Y-%m-%d %H:%M:%S"));
    .   return moons;
    full_moons = get_full_moons_in_year(&yr);
    print(full_moons);
    df = pd.DataFrame(full_moons, columns=["datetime_full_moon"]);
    print(df);
    fn_tosas9x(df,outlib="d:/sd1/",outdsn="pywant",timeest=3);
    ');

    libname sd1 "d:/sd1";
    proc print data=sd1.pywant;
    run;quit;

    /**************************************************************************************************************************/
    /*  PYTHON                                                                                                                */
    /*       datetime_full_moon                                                                                               */
    /*  0   2025-01-13 15:26:51                                                                                               */
    /*  1   2025-02-12 06:53:19                                                                                               */
    /*  2   2025-03-13 23:54:35                                                                                               */
    /*  3   2025-04-12 17:22:12                                                                                               */
    /*  4   2025-05-12 09:55:52                                                                                               */
    /*  5   2025-06-11 00:43:45                                                                                               */
    /*  6   2025-07-10 13:36:42                                                                                               */
    /*  7   2025-08-09 00:54:58                                                                                               */
    /*  8   2025-09-07 11:08:49                                                                                               */
    /*  9   2025-10-06 20:47:33                                                                                               */
    /*  10  2025-11-05 06:19:15                                                                                               */
    /*  11  2025-12-04 16:14:00                                                                                               */
    /*                                                                                                                        */
    /*  SAS                                                                                                                   */
    /*                                                                                                                        */
    /*  Obs  DATETIME_FULL_MOON                                                                                               */
    /*                                                                                                                        */
    /*   1   2025-01-13 15:26:51                                                                                              */
    /*   2   2025-02-12 06:53:19                                                                                              */
    /*   3   2025-03-13 23:54:35                                                                                              */
    /*   4   2025-04-12 17:22:12                                                                                              */
    /*   5   2025-05-12 09:55:52                                                                                              */
    /*   6   2025-0 -11 00:43:45                                                                                              */
    /*   7   2025-07-10 13:36:42                                                                                              */
    /*   8   2025-08-09 00:54:58                                                                                              */
    /*   9   2025-09-07 11:08:49                                                                                              */
    /*  10   2025-10-06 20:47:33                                                                                              */
    /*  11   2025-11-05 06:19:15                                                                                              */
    /*  12   2025-12-04 16:14:00                                                                                              */
    /**************************************************************************************************************************/

    /*___          _   _               _                _               ___           _   _
    |___ \   _   _| |_| |  _ __  _   _| |__   ___  __ _(_)_ __ __  __  ( _ )    _   _| |_| |  _ __  _   _
      __) | | | | | __| | | `_ \| | | | `_ \ / _ \/ _` | | `_ \\ \/ /  / _ \/\ | | | | __| | | `_ \| | | |
     / __/  | |_| | |_| | | |_) | |_| | |_) |  __/ (_| | | | | |>  <  | (_>  < | |_| | |_| | | |_) | |_| |
    |_____|  \__,_|\__|_|_| .__/ \__, |_.__/ \___|\__, |_|_| |_/_/\_\  \___/\/  \__,_|\__|_|_| .__/ \__, |
                       |__|_|    |___/            |___/                                   |__|_|    |___/
     _                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    * clipboard;
    filename clp
      clipbrd;
    data _null_;
     file clp;
     yr=2025;
     put yr;
    run;quit;

    /**************************************************************************************************************************/
    /*  2025 in the windows clipboard as text                                                                                 */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    import ephem
    import datetime
    import pandas as pd
    import pyperclip
    exec(open('c:/oto/fn_pythonx.py').read())
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat')
    txt = pyperclip.paste()
    print(txt)
    yr=int(txt.strip())
    print(yr);
    def get_full_moons_in_year(year):
        moons = []
        # Start from the last day of the previous year
        date = ephem.Date(datetime.date(year - 1, 12, 31))
        end_date = ephem.Date(datetime.date(year + 1, 1, 1))
        while date <= end_date:
            date = ephem.next_full_moon(date)
            local_date = ephem.localtime(date)
            if local_date.year == year:
                moons.append(local_date.strftime("%Y-%m-%d %H:%M:%S"))
        return moons
    full_moons = get_full_moons_in_year(yr)
    print(full_moons)
    df = pd.DataFrame(full_moons, columns=['datetime_full_moon'])
    print(df)
    fn_tosas9x(df,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    libname sd1 "d:/sd1";
    proc print data=sd1.pywant;
    run;quit;

    /**************************************************************************************************************************/
    /*  PYTHON                                                                                                                */
    /*       datetime_full_moon                                                                                               */
    /*  0   2025-01-13 15:26:51                                                                                               */
    /*  1   2025-02-12 06:53:19                                                                                               */
    /*  2   2025-03-13 23:54:35                                                                                               */
    /*  3   2025-04-12 17:22:12                                                                                               */
    /*  4   2025-05-12 09:55:52                                                                                               */
    /*  5   2025-06-11 00:43:45                                                                                               */
    /*  6   2025-07-10 13:36:42                                                                                               */
    /*  7   2025-08-09 00:54:58                                                                                               */
    /*  8   2025-09-07 11:08:49                                                                                               */
    /*  9   2025-10-06 20:47:33                                                                                               */
    /*  10  2025-11-05 06:19:15                                                                                               */
    /*  11  2025-12-04 16:14:00                                                                                               */
    /*                                                                                                                        */
    /*  SAS                                                                                                                   */
    /*                                                                                                                        */
    /*  Obs  DATETIME_FULL_MOON                                                                                               */
    /*                                                                                                                        */
    /*   1   2025-01-13 15:26:51                                                                                              */
    /*   2   2025-02-12 06:53:19                                                                                              */
    /*   3   2025-03-13 23:54:35                                                                                              */
    /*   4   2025-04-12 17:22:12                                                                                              */
    /*   5   2025-05-12 09:55:52                                                                                              */
    /*   6   2025-0 -11 00:43:45                                                                                              */
    /*   7   2025-07-10 13:36:42                                                                                              */
    /*   8   2025-08-09 00:54:58                                                                                              */
    /*   9   2025-09-07 11:08:49                                                                                              */
    /*  10   2025-10-06 20:47:33                                                                                              */
    /*  11   2025-11-05 06:19:15                                                                                              */
    /*  12   2025-12-04 16:14:00                                                                                              */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
