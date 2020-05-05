# utl-normalizing-the-proc-corr-output-correlation-matrix
Normalizing the proc corr output correlation matrix
    Normalizing the proc corr output correlation matrix

    github
    https://tinyurl.com/yct87n2f
    https://github.com/rogerjdeangelis/utl-normalizing-the-proc-corr-output-correlation-matrix


    utl_gather macro by Alea Iacta
    https://github.com/clindocu

    I don't think this can be done with one 'proc transpose'.
    The utl_untranspose macro may work (untested)

    SAS Forum
    https://tinyurl.com/yb5rqbzu
    https://communities.sas.com/t5/Statistical-Procedures/Filtering-Correlation-Matrix/m-p/645358

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    proc corr data=sashelp.cars outp=have(where=(_type_='CORR')) noprint;
    run;


     WORK.HAVE total obs=10

                                                                                                              MPG_
      _TYPE_    _NAME_           MSRP       INVOICE    ENGINESIZE    CYLINDERS    HORSEPOWER    MPG_CITY     HIGHWAY     WEIGHT     WHEELBASE     LENGTH

       CORR     MSRP            1.00000     0.99913      0.57175       0.64974      0.82695     -0.47502    -0.43962     0.44843      0.15200     0.17204
       CORR     INVOICE         0.99913     1.00000      0.56450       0.64523      0.82375     -0.47044    -0.43459     0.44233      0.14833     0.16659
       CORR     ENGINESIZE      0.57175     0.56450      1.00000       0.90800      0.78743     -0.70947    -0.71730     0.80787      0.63652     0.63745
       CORR     CYLINDERS       0.64974     0.64523      0.90800       1.00000      0.81034     -0.68440    -0.67610     0.74221      0.54673     0.54778
       CORR     HORSEPOWER      0.82695     0.82375      0.78743       0.81034      1.00000     -0.67670    -0.64720     0.63080      0.38740     0.38155
       CORR     MPG_CITY       -0.47502    -0.47044     -0.70947      -0.68440     -0.67670      1.00000     0.94102    -0.73797     -0.50728    -0.50153
       CORR     MPG_HIGHWAY    -0.43962    -0.43459     -0.71730      -0.67610     -0.64720      0.94102     1.00000    -0.79099     -0.52466    -0.46609
       CORR     WEIGHT          0.44843     0.44233      0.80787       0.74221      0.63080     -0.73797    -0.79099     1.00000      0.76070     0.69002
       CORR     WHEELBASE       0.15200     0.14833      0.63652       0.54673      0.38740     -0.50728    -0.52466     0.76070      1.00000     0.88919
       CORR     LENGTH          0.17204     0.16659      0.63745       0.54778      0.38155     -0.50153    -0.46609     0.69002      0.88919     1.00000

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    Up to 40 obs WORK.WANTGTH total obs=100

    Obs    _TYPE_    _NAME_        VAR                V

      1     CORR     MSRP          MSRP            1.00000
      2     CORR     MSRP          INVOICE         0.99913
      3     CORR     MSRP          ENGINESIZE      0.57175
      4     CORR     MSRP          CYLINDERS       0.64974
      5     CORR     MSRP          HORSEPOWER      0.82695
      6     CORR     MSRP          MPG_CITY       -0.47502
      7     CORR     MSRP          MPG_HIGHWAY    -0.43962
      8     CORR     MSRP          WEIGHT          0.44843
      9     CORR     MSRP          WHEELBASE       0.15200
     10     CORR     MSRP          LENGTH          0.17204
     11     CORR     INVOICE       MSRP            0.99913
     12     CORR     INVOICE       INVOICE         1.00000
     13     CORR     INVOICE       ENGINESIZE      0.56450
     14     CORR     INVOICE       CYLINDERS       0.64523
     15     CORR     INVOICE       HORSEPOWER      0.82375
     16     CORR     INVOICE       MPG_CITY       -0.47044
     17     CORR     INVOICE       MPG_HIGHWAY    -0.43459
     18     CORR     INVOICE       WEIGHT          0.44233
     19     CORR     INVOICE       WHEELBASE       0.14833
     20     CORR     INVOICE       LENGTH          0.16659
    ...

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    %utl_gather(have,var,corr,_name_ _type_,want(where=(corr>.5)),valformat=8.3);


