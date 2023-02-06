# SasLogSearch

## 400起點DB
* DB:
    LIBRARY.FBLSTUS
* KEY: 
    FSTUS_SCR_NO
    FSTUS_TXN_KEY
    FSTUS_UPDATE_NO

## 400MQDB
* DB:
    REMOTE.FVAMQSND
* KEY: 
    FSTUS_SCR_NO = substr(VAS_MSG_BODY,1,4)
    FSTUS_TXN_KEY LIKE substr(VAS_MSG_BODY, 7, 70)
    FSTUS_UPDATE_NO = substr(VAS_MSG_BODY,77, 10)

## SWALLOW
* DB:
    SIT:MEGA_OBSWDBT.dbo.SWHNMSG
* IP:
    SIT:192.168.x.x
* KEY:
    MESG_APPLI_MAIN_REFNO = FSTUS_SCR_NO-FSTUS_TXN_KEY-FSTUS_UPDATE_NO


## Sas
* DB:
    SIT:AMLHK0.NCSC.NAME_CHECK_RECORD_MAIN
* IP
    SIT:192.168.x.x
* KEY:
    REFERENCE_NUMBER = FSTUS_SCR_NO-FSTUS_TXN_KEY-FSTUS_UPDATE_NO

