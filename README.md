# utl_calculating_the_area_between_a_curve_and_a_straight_line
Calculating the area between a curve and a straight line. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Calculating the area between a curve and a straight line

    see github
    https://goo.gl/fcYkcs
    https://github.com/rogerjdeangelis/utl_calculating_the_area_between_a_curve_and_a_straight_line

    StackOverflow R
    https://goo.gl/kctkT8
    https://stackoverflow.com/questions/48752035/calculating-the-area-between-a-curve-and-a-straight-line-without-finding-the-fun

    G5w profile
    https://stackoverflow.com/users/4752675/g5w

    There are two other shorter solutions.
    INPUT
    =====

      y=sqrt(x)
      y=x


        Y |
     1.00 +  Area between y=sqrt(x) and y=x = 1/6           ++++
          |                                             ++++/
          |                                         ++++  /
          |                                     +++     /
          |                                 +++      /
     0.75 +                Y=sqrt(x)    +++        /
          |                         +++         /
          |                      +++          /  y=x
          |                   +++ Area     /
          |                +++ 2/3-1/2   /
     0.50 +              ++  =1/6     /
          |            ++ 0.16667   /
          |          ++          /
          |        ++          /
          |      ++         /    Area under y=x = 1/2
     0.25 +     ++        /      Area under y=sqrt(x) = 2/3
          |    ++      /         I(x) = integral(sqrt(x)) = 2/3 * x **(3/2) =I(1)-I(0) =2/3
          |   ++     /
          |   +   /              Area in between = 2/3 - 1/3 = 1/6
          |  .  /
     0.00 +  +/
          |
          ---+---------+---------+---------+---------+---------+--
            0.0       0.2       0.4       0.6       0.8       1.0

                                      X

    PROCESS
    =======

        %utl_submit_wps64('
        libname sd1 "d:/sd1";
        options set=R_HOME "C:/Program Files/R/R-3.3.1";
        libname wrk "%sysfunc(pathname(work))";
        proc r;
        submit;
        source("C:/Program Files/R/R-3.3.1/etc/Rprofile.site", echo=T);
        library(haven);
        have<-read_sas("d:/sd1/have.sas7bdat");
        head(have);
        attach(have);
        m <- 1;
        b <- 0;
        F1 = approxfun(X,Y);
        F2 = function(X) { m*X+b };
        area<-integrate(F1, X[1], X[100])$value - integrate(F2, X[1], X[100])$value;
        endsubmit;
        import r=area data=wrk.want;
        run;quit;
        ');


    OUTPUT
    ======

     WORK.WANT total obs=1

        AREA

      0.16601

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      do x=.01 to 1 by .01;
        y=sqrt(x);
        y1=x;
        output;
      end;
    run;quit;

    options ls=64 ps=32;
    proc plot data=sd1.have;
    plot y*x="+" y1*x="."/overlay;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_wps64('
    libname sd1 "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.1";
    libname wrk "%sysfunc(pathname(work))";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.1/etc/Rprofile.site", echo=T);
    library(haven);
    have<-read_sas("d:/sd1/have.sas7bdat");
    head(have);
    attach(have);
    m <- 1;
    b <- 0;
    F1 = approxfun(X,Y);
    F2 = function(X) { m*X+b };
    area<-integrate(F1, X[1], X[100])$value - integrate(F2, X[1], X[100])$value;
    endsubmit;
    import r=area data=wrk.want;
    run;quit;
    ');

