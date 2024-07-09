# Manual-Audit-Modeling
# SQL code for building time / path models for Manual Audit process 

# code for setting up data base with required tables 
# Calendar Table:  MA2_DateDim
#     Contains date, US holidays (0 = holiday), WorkDay (1=workday, M-F).
#              Note US_Holiday_flag * Work_Day_Flag = Work Day
#     Other information on day, month, week, etc. derived from Snowflake functions
#     Note day_of_Calendar is not julian day, but days from 2000-01-01

# Data Pull view:  MA2_DataView6
#     View based on prior work at Avetta to get Manual Audit forms by various
#       attributes such as supplier information, Renewal Status, Work Flow node
#       and metrics related to entry into the workflow and time in workflow.

# Group Table:  MA2_Group
#     Table for metadata and data filters for each analytic created.  The Group
#       Table contains descriptors of the analytic, up to 10 unique dimensional 
#       attribute descritors, data qualifiers (date, size) and views to pull
#       data and perform the analytic.  
#     Example section contains sample code for populating this table.  

# Instance Table:  MA2_Instance
#      Table populated by the View For Dimensions (group table) containing 
#        metadata on each analytic data set (ADS), including the specific dimensional
#        attributes of the ADS, total number of atomic data elements and 
#        whether the group is ready for calculation

# Results (Analytic 1):  MA2_CTMODELRESULTS
#       Contains the individual histograms built for each qualified analytic Data Set
#         Key is the groupID and instance ID and results must be joined back to instance table 
#         to retrieve dimensional attributes.

# Results (Anatic 2):  MA2_PATHSPLITRESULTS
#        Constains the probability of each edge connecting the workflow nodes (if more 
#          than 2 exit edges).  Key is the groupID and instanceID and results must be 
#          joined back to instance table to retrieve dimensional attributes.

# 
