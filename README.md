# utl-fit-a-beta-pdf-using-sas-nlmixed-and-r-fitdistplus-package
Fit a beta density pdf using sas nlmixed and r fitdistplus package 
    %let pgm=utl-fit-a-beta-density-pdf-using-sas-nlmixed-and-r-fitdistplus-package;

    %stop_submission;

    Fit a beta density pdf using sas nlmixed and r fitdistplus package

    hi res plot
    https://tinyurl.com/3r8xxtz6
    https://github.com/rogerjdeangelis/utl-fit-a-beta-pdf-using-sas-nlmixed-and-r-fitdistplus-package/blob/main/fit.png

    github
    https://tinyurl.com/2s46zxha
    https://github.com/rogerjdeangelis/utl-fit-a-beta-pdf-using-sas-nlmixed-and-r-fitdistplus-package

    sas communities
    https://tinyurl.com/mrxw4jye
    https://communities.sas.com/t5/Statistical-Procedures/Log-Likelihood-for-BETA-distribution-in-Proc-NLMIXED/m-p/851965#M42170

       Two Solution
           1 sas nlmixed
           2 r fitdistrplus package
             no need to take the log
           3 related repos
    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */
                        Beta Random Variable(XBETA)

            0.0       0.2       0.4       0.6       0.8       1.0
          ---+---------+---------+---------+---------+---------+----
          | PLOT https://tinyurl.com/3r8xxtz6  FIT A=5 and B=5     |
          |                                                        |
      2.5 +  O beta(5,5)              OO       G(a+b)  a-1    b-1  + 2.5
          |  | observed             OO OOO-->  ------ x   (1-x)    |
          |                        O ___ OO   G(a)G(B)             |
          | fit beta(5,5) to    s O  |||  OO|                      |
          |                      O   |||  |O|      OR              |
      2.0 + INPUT DATA          |O|  |||  ||O           4      4   + 2.0
          | ==========          O||  |||  ||OO   252 * x *(1-x)    |
          |   XBETA            O|||  |||  |||O                     |
    D     |     __             O|||  |||  ||| O __R FIT ESTIMATES  |     D
    E     |  0.46954       |||O |||  |||  ||| O|||                 |     E
    N 1.5 +  0.63700       |||O |||  |||  |||  O||  alpha: 4.5691  + 1.5 N
    S     |  0.45208       ||O  |||  |||  |||  O||  beta:  4.6189  |     S
    I     |  0.66118       ||O  |||  |||  |||  |O|                 |     I
    T     |  0.75778       |O|  |||  |||  |||  |O|                 |     T
    Y     |  ...           |O|  |||  |||  |||  ||O                 |     Y
      1.0 +                O||  |||  |||  |||  ||OO                + 1.0
          |               O|||  |||  |||  |||  |||O                |
          |           ___ O|||  |||  |||  |||  ||| O___            |
          |           |||O |||  |||  |||  |||  ||| O|||            |
          |           |||O |||  |||  |||  |||  |||  O||            |
      0.5 +           ||O  |||  |||  |||  |||  |||  OO|            + 0.5
          |           |O|  |||  |||  |||  |||  |||  |OO            |
          |           O||  |||  |||  |||  |||  |||  ||O            |
          |          OO||  |||  |||  |||  |||  |||  |||OO          |
          |        OO |||  |||  |||  |||  |||  |||  ||| OOO        |
        0 +  OOOOOO|| |||  |||  |||  |||  |||  |||  ||| |||OOOOO   +   0
          ---+---------+----+----+---------+---------+---------+----
            0.0       0.2       0.4       0.6       0.8       1.0
                    Beta Random Variable(XBETA)



    /**************************************************************************************************************************/
    /*        INPUT                   |       PROCESS                                |       OUTPUT                           */
    /*                                |                                              |                                        */
    /*    Obs   XBETA                 |  1 SAS NLMIXED                               | PARAMETER    ESTIMATE                  */
    /*                                |                                              |                                        */
    /*      1  0.46954                |                                              |    a          4.5689                   */
    /*      2  0.63700                |  ods output ParameterEstimates=fit;          |    b          4.6188                   */
    /*      3  0.45208                |  proc nlmixed data=sd1.have;                 |                                        */
    /*      4  0.66118                |    parms a=4 b=5.5;                          |                                        */
    /*      5  0.75778                |    ll=                                       |                                        */
    /*    ...                         |      logpdf("Beta", xbeta, a, b);;           |                                        */
    /*    996  0.24497                |    model xbeta~general(ll);                  |                                        */
    /*    997  0.79708                |  run;                                        |                                        */
    /*    998  0.63692                |                                              |                                        */
    /*    999  0.54632                |  proc print data=fit(keep=                   |                                        */
    /*                                |    parameter estimate);                      |                                        */
    /*   1000  0.55149                |  run;quit;                                   |                                        */
    /*                                |                                              |                                        */
    /*   options                      |                                              |                                        */
    /*     validvarname=upcase;       |                                              |                                        */
    /*   libname sd1 "d:/sd1";        |                                              |                                        */
    /*   data sd1.have;               |                                              |                                        */
    /*   call streaminit(54321);      |                                              |                                        */
    /*   do i = 1 to 1000;            |                                              |                                        */
    /*      xbeta =                   |                                              |                                        */
    /*       rand("Beta", 5, 5);      |                                              |                                        */
    /*      output;                   |                                              |                                        */
    /*   end;                         |                                              |                                        */
    /*   run;quit;                    |                                              |                                        */
    /*                                |---------------------------------------------------------------------------------------*/
    /*                                |                                              |                                        */
    /*                                | 2 R FITDISTRPLUS PACKAGE                     |  ROWNAMES      PARAMETERS              */
    /*                                |                                              |                                        */
    /*                                |                                              | alpha.shape1      4.56905              */
    /*                                | %utlfkil(d:/png/fit.png)                     | beta.shape2       4.61892              */
    /*                                |                                              |                                        */
    /*                                | proc datasets lib=sd1 nolist nodetails;      |                                        */
    /*                                |  delete want;                                |                                        */
    /*                                | run;quit;                                    |                                        */
    /*                                |                                              |                                        */
    /*                                | %utl_rbeginx;                                |                                        */
    /*                                | parmcards4;                                  |                                        */
    /*                                | library(haven)                               |                                        */
    /*                                | library(fitdistrplus)                        |                                        */
    /*                                | source("c:/oto/fn_tosas9x.R")                |                                        */
    /*                                | have<-read_sas("d:/sd1/have.sas7bdat")       |                                        */
    /*                                | have<-as.numeric(t(have$XBETA))              |                                        */
    /*                                | fit <- fitdist(have, "beta")                 |                                        */
    /*                                | want<-data.frame(c(                          |                                        */
    /*                                |     alpha=fit$estimate[1]                    |                                        */
    /*                                |    ,beta =fit$estimate[2]))                  |                                        */
    /*                                | colnames(want)<-c("Parameters")              |                                        */
    /*                                | png("d:/png/fit.png")                        |                                        */
    /*                                | x <- seq(0, 1, length.out = 100)             |                                        */
    /*                                | hist(have, freq = FALSE,                     |                                        */
    /*                                |    main = "Beta Distribution Fit"            |                                        */
    /*                                |   ,xlab = "x"                                |                                        */
    /*                                |   ,ylim = c(0, 3)                            |                                        */
    /*                                |   ,xlim = c(0,1))                            |                                        */
    /*                                | lines(x, dbeta(x                             |                                        */
    /*                                |   ,shape1 = fit$estimate[1]                  |                                        */
    /*                                |   ,shape2 = fit$estimate[2])                 |                                        */
    /*                                |   ,col = "red", lwd = 2)                     |                                        */
    /*                                | legend("topright"                            |                                        */
    /*                                |   ,legend = c("Fitted Beta PDF")             |                                        */
    /*                                |   ,col = "red", lwd = 2)                     |                                        */
    /*                                | dev.off()                                    |                                        */
    /*                                | fn_tosas9x(                                  |                                        */
    /*                                |       inp    = want                          |                                        */
    /*                                |      ,outlib ="d:/sd1/"                      |                                        */
    /*                                |      ,outdsn ="want"                         |                                        */
    /*                                |      )                                       |                                        */
    /*                                | ;;;;                                         |                                        */
    /*                                | %utl_rendx;                                  |                                        */
    /*                                |                                              |                                        */
    /*                                | proc print data=sd1.want;                    |                                        */
    /*                                | run;quit;                                    |                                        */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options
      validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
    call streaminit(54321);
    do i = 1 to 1000;
       xbeta =
        rand("Beta", 5, 5);
       output;
    end;
    run;quit;


    /**************************************************************************************************************************/
    /*  Obs   XBETA                                                                                                           */
    /*                                                                                                                        */
    /*    1  0.46954                                                                                                          */
    /*    2  0.63700                                                                                                          */
    /*    3  0.45208                                                                                                          */
    /*    4  0.66118                                                                                                          */
    /*    5  0.75778                                                                                                          */
    /*  ...                                                                                                                   */
    /*  996  0.24497                                                                                                          */
    /*  997  0.79708                                                                                                          */
    /*  998  0.63692                                                                                                          */
    /*  999  0.54632                                                                                                          */
    /* 1000  0.55149                                                                                                          */
    /**************************************************************************************************************************/

    /*___            __ _ _      _ _     _         _
    |___ \   _ __   / _(_) |_ __| (_)___| |_ _ __ | |_   _ ___
      __) | | `__| | |_| | __/ _` | / __| __| `_ \| | | | / __|
     / __/  | |    |  _| | || (_| | \__ \ |_| |_) | | |_| \__ \
    |_____| |_|    |_| |_|\__\__,_|_|___/\__| .__/|_|\__,_|___/
                                            |_|
    */

    %utlfkil(d:/png/fit.png)

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(fitdistrplus)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    have<-as.numeric(t(have$XBETA))
    fit <- fitdist(have, "beta")
    want<-data.frame(c(
        alpha=fit$estimate[1]
       ,beta =fit$estimate[2]))
    colnames(want)<-c("Parameters")
    png("d:/png/fit.png")
    x <- seq(0, 1, length.out = 100)
    hist(have, freq = FALSE,
       main = "Beta Distribution Fit"
      ,xlab = "x"
      ,ylim = c(0, 3)
      ,xlim = c(0,1))
    lines(x, dbeta(x
      ,shape1 = fit$estimate[1]
      ,shape2 = fit$estimate[2])
      ,col = "red", lwd = 2)
    legend("topright"
      ,legend = c("Fitted Beta PDF")
      ,col = "red", lwd = 2)
    dev.off()
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /* Obs      ROWNAMES      PARAMETERS                                                                                      */
    /*                                                                                                                        */
    /*  1     alpha.shape1      4.56905                                                                                       */
    /*  2     beta.shape2       4.61892                                                                                       */
    /**************************************************************************************************************************/

    /*____            _       _           _
    |___ /   _ __ ___| | __ _| |_ ___  __| |  _ __ ___ _ __   ___  ___
      |_ \  | `__/ _ \ |/ _` | __/ _ \/ _` | | `__/ _ \ `_ \ / _ \/ __|
     ___) | | | |  __/ | (_| | ||  __/ (_| | | | |  __/ |_) | (_) \__ \
    |____/  |_|  \___|_|\__,_|\__\___|\__,_| |_|  \___| .__/ \___/|___/
                                                      |_|
    */

    REPO
    ------------------------------------------------------------------------------------------------------------------------------------
    https://github.com/rogerjdeangelis/utl-betas-for-rolling-regressions
    https://github.com/rogerjdeangelis/utl-better-fit-with-two-paramater-beta-then-four-than-four-polynomial-on-unit-square
    https://github.com/rogerjdeangelis/utl-has-your-stock-out-performed-standard-and-poors500-calulating-the-beta-slope
    https://github.com/rogerjdeangelis/utl-piecewise-linear-fit-compared-to-unit-square-beta-cdf-non-linear-fit-two-vs-four-parameters
    https://github.com/rogerjdeangelis/utl-using-beta-cdf-and-pdf-unitsquare-to-fit-non-linear-equations-and-simple-polynomials
    https://github.com/rogerjdeangelis/utl-using-the-unitsquare-framework-and-cumulative-beta-to-fit-a-non-linear-equation
    https://github.com/rogerjdeangelis/utl_estimate_parameters_of_beta_distribution_with_known_percentiles
    https://github.com/rogerjdeangelis/utl_symbolic_determination_of_moments_of_a_beta_like_distribution

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
