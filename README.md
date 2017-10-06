# utl_optlen
SAS reduce or shrink the size of numeric and character SAS variables to the max observed in the data
optimum lengths for SAS variables

    ```  Reduce the size of numeric and character variables to the max observed in the data              ```
    ```                                                                                                          ```
    ```  see                                                                                                     ```
    ```  https://goo.gl/UnvAvf                                                                                   ```
    ```  https://communities.sas.com/t5/General-SAS-Programming/output-from-iteration/m-p/377253                 ```
    ```                                                                                                          ```
    ```  associated code                                                                                         ```
    ```                                                                                                          ```
    ```    WORKING CODE                                                                                          ```
    ```    ============                                                                                          ```
    ```         SAS                                                                                              ```
    ```                                                                                                          ```
    ```         %utl_optlen(inp=class,out=class);                                                                ```
    ```                                                                                                          ```
    ```         Details                                                                                          ```
    ```         Rick Langston  (numeric length reduction)                                                        ```
    ```                                                                                                          ```
    ```         * NUMERIC;                                                                                       ```
    ```         if missing(num[i]) then len=3;                                                                   ```
    ```         else do;                                                                                         ```
    ```           if num[i] ne trunc( num[i], 7 ) then len = 8 ; else                                            ```
    ```           if num[i] ne trunc( num[i], 6 ) then len = 7 ; else                                            ```
    ```           if num[i] ne trunc( num[i], 5 ) then len = 6 ; else                                            ```
    ```           if num[i] ne trunc( num[i], 4 ) then len = 5 ; else                                            ```
    ```           if num[i] ne trunc( num[i], 3 ) then len = 4 ; else len=3;                                     ```
    ```         end;                                                                                             ```
    ```         if len > lennum[i] then lennum[i]=len;                                                           ```
    ```                                                                                                          ```
    ```         * CHARACTER;                                                                                     ```
    ```         array chr[&chr] _character_;                                                                     ```
    ```         array lenchr[&chr] _temporary_;                                                                  ```
    ```                                                                                                          ```
    ```         do __i=1 to dim(chr);                                                                            ```
    ```            if lengthn(chr[__i]) > lenchr[__i] then lenchr[__i]=length(chr[__i]);                         ```
    ```         end;                                                                                             ```
    ```                                                                                                          ```
    ```  HAVE                                                                                                    ```
    ```  ====                                                                                                    ```
    ```                                                                                                          ```
    ```  Up to 40 obs WORK.CLASS total obs=19                                                                    ```
    ```                                                                                                          ```
    ```  Obs    SEX    NAME       AGE    HEIGHT    WEIGHT                                                        ```
    ```                                                                                                          ```
    ```    1     M     Alfred      14      45        101                                                         ```
    ```    2     F     Alice       13      53        121                                                         ```
    ```    3     F     Barbara     13      23        119                                                         ```
    ```    4     F     Carol       14      55        110                                                         ```
    ```    5     M     Henry       14      28        120                                                         ```
    ```    6     M     James       12      43        132                                                         ```
    ```    7     F     Jane        12      46        106                                                         ```
    ```   ...                                                                                                    ```
    ```                                                                                                          ```
    ```   Middle Observation(9 ) of CLASS - Total Obs 19                                                         ```
    ```                                                                                                          ```
    ```                              SAMPLE                                                                      ```
    ```    -- CHARACTER --  LENGTH   VALUE                                                                       ```
    ```                     ======   =====                                                                       ```
    ```   SEX         C      5       M                   SEX                                                     ```
    ```   NAME        C      16      Jeffrey             NAME                                                    ```
    ```                                                                                                          ```
    ```                                                                                                          ```
    ```    -- NUMERIC --                                                                                         ```
    ```   AGE         N      8       13                  AGE                                                     ```
    ```   HEIGHT      N      8       20                  HEIGHT                                                  ```
    ```   WEIGHT      N      8       140                 WEIGHT                                                  ```
    ```                                                                                                          ```
    ```                                                                                                          ```
    ```  WANT                                                                                                    ```
    ```  ====                                                                                                    ```
    ```                                                                                                          ```
    ```  Up to 40 obs WORK.CLASS total obs=19                                                                    ```
    ```                                                                                                          ```
    ```  Obs    SEX    NAME       AGE    HEIGHT    WEIGHT                                                        ```
    ```                                                                                                          ```
    ```    1     M     Alfred      14      45        101                                                         ```
    ```    2     F     Alice       13      53        121                                                         ```
    ```    3     F     Barbara     13      23        119                                                         ```
    ```    4     F     Carol       14      55        110                                                         ```
    ```    5     M     Henry       14      28        120                                                         ```
    ```    6     M     James       12      43        132                                                         ```
    ```    7     F     Jane        12      46        106                                                         ```
    ```  ..                                                                                                      ```
    ```                                                                                                          ```
    ```                                                                                                          ```
    ```                                SAMPLE                                                                    ```
    ```    -- CHARACTER --  LENGTH     VALUE                                                                     ```
    ```                     ======     =====                                                                     ```
    ```                                                                                                          ```
    ```   -- CHARACTER --                                                                                        ```
    ```  SEX              C    1       M                                                                         ```
    ```  NAME             C    7       Jeffrey                                                                   ```
    ```                                                                                                          ```
    ```                                                                                                          ```
    ```   -- NUMERIC --                                                                                          ```
    ```  AGE              N    3       13                                                                        ```
    ```  HEIGHT           N    3       20                                                                        ```
    ```                                                                                                          ```
    ```  DETAILS                                                                                                 ```
    ```  =======                                                                                                 ```
    ```                 OLD      NEW                                                                             ```
    ```                 LENGTH   LENGTH                                                                          ```
    ```                                                                                                          ```
    ```  SEX       C     5        1                                                                              ```
    ```  NAME      C    16        7                                                                              ```
    ```  AGE       N     8        3                                                                              ```
    ```  HEIGHT    N     8        3                                                                              ```
    ```                 ==       ==                                                                              ```
    ```                 37       14                                                                              ```
    ```                                                                                                          ```
    ```                                                                                                          ```
    ```  *                _              _       _                                                               ```
    ```   _ __ ___   __ _| | _____    __| | __ _| |_ __ _                                                        ```
    ```  | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |                                                       ```
    ```  | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |                                                       ```
    ```  |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|                                                       ```
    ```  ;                                                                                                       ```
    ```                                                                                                          ```
    ```  data class;                                                                                             ```
    ```    length sex $5 name $16.;                                                                              ```
    ```    set sashelp.class;                                                                                    ```
    ```      weight=int(50*uniform(5531)) +100;                                                                  ```
    ```      height=int(45*uniform(5531)) + 20;                                                                  ```
    ```  run;quit;                                                                                               ```
    ```                                                                                                          ```
