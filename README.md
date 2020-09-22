# utl-simple-proc-report-and-tabulate-n-and-percent-crosstab-ourput-datasets-
Simple proc report and tabulate n and percent crosstab ourput datasets 
    Simple proc report and tabulate n and percent crosstab output datasets                                                    
                                                                                                                              
    Unlike other solutions these algorithms produce output datasets                                                           
                                                                                                                              
         Two Solutions                                                                                                        
                                                                                                                              
              a. proc report                                                                                                  
              b. proc tabulate                                                                                                
                                                                                                                              
    GitHub                                                                                                                    
    https://tinyurl.com/y4nkh9zd                                                                                              
    https://github.com/rogerjdeangelis/utl-simple-proc-report-and-tabulate-n-and-percent-crosstab-ourput-datasets-            
                                                                                                                              
    macros                                                                                                                    
    https://tinyurl.com/y9nfugth                                                                                              
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                
                                                                                                                              
    github                                                                                                                    
    https://tinyurl.com/yafyt2jk                                                                                              
    https://github.com/rogerjdeangelis/utl-five-algorithms-for-a-simple-n-percent-crosstab                                    
                                                                                                                              
    related to (but different denominator)                                                                                    
    https://tinyurl.com/y4ulnoq8                                                                                              
    https://communities.sas.com/t5/SAS-Enterprise-Guide/How-to-add-percentage-columns-in-proc-report/td-p/331423              
                                                                                                                              
    /*                   _                                                                                                    
    (_)_ __  _ __  _   _| |_                                                                                                  
    | | `_ \| `_ \| | | | __|                                                                                                 
    | | | | | |_) | |_| | |_                                                                                                  
    |_|_| |_| .__/ \__,_|\__|                                                                                                 
            |_|                                                                                                               
    */                                                                                                                        
                                                                                                                              
    data have;                                                                                                                
    informat color $5.location $9.;                                                                                           
    input color$ location price;                                                                                              
    cards4;                                                                                                                   
    blue store 4.99                                                                                                           
    black warehouse 6.00                                                                                                      
    red warehouse 2.00                                                                                                        
    blue store 10.00                                                                                                          
    black store 7.50                                                                                                          
    red warehouse 10.00                                                                                                       
    blue store 5.00                                                                                                           
    black warehouse 3.00                                                                                                      
    red store 1.00                                                                                                            
    blue store 5.00                                                                                                           
    ;;;;                                                                                                                      
    run;quit;                                                                                                                 
                                                                                                                              
    /*           _               _                                                                                            
      ___  _   _| |_ _ __  _   _| |_                                                                                          
     / _ \| | | | __| `_ \| | | | __|                                                                                         
    | (_) | |_| | |_| |_) | |_| | |_                                                                                          
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                         
                    |_|                                                                                                       
    */                                                                                                                        
                                                                                                                              
    WORK.WANT_RPT total obs=4                                                                                                 
                                                                                                                              
                           STORE_    WAREHOUSE_    WAREHOUSE_                                                                 
       COLOR    STORE_N      PCT          N            PCT                                                                    
                                                                                                                              
       black       1        0.167         2            0.5                                                                    
       blue        4        0.667         0            0.0                                                                    
       red         1        0.167         2            0.5                                                                    
                                                                                                                              
                   6        1.000         4            1.0                                                                    
                                                                                                                              
    Variables                                                                                                                 
                                                                                                                              
    #    Variable         Type    Len                                                                                         
                                                                                                                              
    1    COLOR            Char      5                                                                                         
    2    STORE_N          Num       8                                                                                         
    3    STORE_PCT        Num       8                                                                                         
    4    WAREHOUSE_N      Num       8                                                                                         
    5    WAREHOUSE_PCT    Num       8                                                                                         
                                                                                                                              
    /*         _       _   _                                                                                                  
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                       
    / __|/ _ \| | | | | __| |/ _ \| `_ \                                                                                      
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                     
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                     
                                         _                                                                                    
      __ _     _ __ ___ _ __   ___  _ __| |_                                                                                  
     / _` |   | `__/ _ \ `_ \ / _ \| `__| __|                                                                                 
    | (_| |_  | | |  __/ |_) | (_) | |  | |_                                                                                  
     \__,_(_) |_|  \___| .__/ \___/|_|   \__|                                                                                 
                       |_|                                                                                                    
    */                                                                                                                        
    options missing='0';                                                                                                      
    %utl_odsrpt(setup);                                                                                                       
                                                                                                                              
    proc report data=have nowd missing out=want noheader formchar="|" box;                                                    
    title "|color|store_n|store_pct|warehouse_n|warehouse_pct|";                                                              
      column color location, (n pctn );                                                                                       
                                                                                                                              
      define color/group;                                                                                                     
      define location/across;                                                                                                 
      define n / 'Count';                                                                                                     
      define pctn / f=9.3;                                                                                                    
      rbreak after/summarize;                                                                                                 
                                                                                                                              
    run;quit;                                                                                                                 
                                                                                                                              
    %utl_odsrpt(outdsn=want_rpt);                                                                                             
                                                                                                                              
    options FORMCHAR='|----|+|---+=|-/\<>*';                                                                                  
    options missing='.';                                                                                                      
                                                                                                                              
    /*        _        _           _       _                                                                                  
    | |__    | |_ __ _| |__  _   _| | __ _| |_ ___                                                                            
    | `_ \   | __/ _` | `_ \| | | | |/ _` | __/ _ \                                                                           
    | |_) |  | || (_| | |_) | |_| | | (_| | ||  __/                                                                           
    |_.__(_)  \__\__,_|_.__/ \__,_|_|\__,_|\__\___|                                                                           
                                                                                                                              
    */                                                                                                                        
                                                                                                                              
    options missing='0';                                                                                                      
    %utl_odstab(setup);                                                                                                       
    proc tabulate data=have;                                                                                                  
    title "|color|store_n|store_pct|warehouse_n|warehouse_pct|";                                                              
    class color location;                                                                                                     
    table color='',location=''*(n colpctn) /box="color";                                                                      
    run;quit;                                                                                                                 
    %utl_odstab(outdsn=want_tab,datarow=2);                                                                                   
                                                                                                                              
    options FORMCHAR='|----|+|---+=|-/\<>*';                                                                                  
    options missing='.';                                                                                                      
                                                                                                                              
