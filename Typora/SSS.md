![image-20240830124003715](./../img/image-20240830124003715.png)

```ABAP
*&---------------------------------------------------------------------*
*& Include          ZQUIZ_B02_06F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form set_layout
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM set_layout .

  LOOP AT gt_flights INTO gs_flight.
    IF gs_flight-seatsdif < 20.
      gs_scol-fname = 'SEATSDIF'.
      gs_scol-color-col = '6'.
      gs_scol-color-int = '1'.
      gs_scol-color-inv = '0'.

      APPEND gs_scol TO gs_flight-it_col.
    ENDIF.

    MODIFY gt_flights FROM gs_flight.
    CLEAR: gs_flight.
  ENDLOOP.

  gs_layout-ctab_fname = 'IT_COL'.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form set_field_catalog
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM set_field_catalog .
  gs_fcat-fieldname = 'SEATSDIF'.
  gs_fcat-coltext = 'SEATSDIF'.
  APPEND gs_fcat TO gt_fcat.
  CLEAR: gs_fcat.

  gs_fcat-fieldname = 'PRIVATE'.
  gs_fcat-coltext = 'PRIVATE'.
  APPEND gs_fcat TO gt_fcat.
  CLEAR: gs_fcat.

  gs_fcat-fieldname = 'BUSINESS'.
  gs_fcat-coltext = 'BUSINESS'.
  APPEND gs_fcat TO gt_fcat.
  CLEAR: gs_fcat.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form get_data
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM get_data .

  SELECT *
    INTO CORRESPONDING FIELDS OF TABLE gt_Scarr
    FROM scarr.

  SELECT *
    FROM sflight
    INTO CORRESPONDING FIELDS OF gs_sflight
    WHERE carrid IN so_Car
      AND connid IN so_con.

    MOVE-CORRESPONDING gs_sflight TO gs_flight.

    gs_flight-seatsmax = gs_sflight-seatsmax + gs_sflight-seatsmax_f
                         + gs_sflight-seatsmax_b.
    gs_flight-seatsocc = gs_sflight-seatsocc + gs_sflight-seatsocc_b
                         + gs_sflight-seatsocc_f.
    gs_flight-seatsdif = gs_flight-seatsmax - gs_flight-seatsocc.

    READ TABLE gt_scarr INTO gs_scarr
      WITH KEY carrid = gs_flight-carrid.
    IF sy-subrc = 0.
      gs_flight-carrname = gs_scarr-carrname.
    ENDIF.

    SELECT custtype
      FROM sbook
      INTO CORRESPONDING FIELDS OF gs_sbook
      WHERE cancelled <> 'X'
        AND carrid = gs_flight-carrid
        AND connid = gs_flight-connid
        AND fldate = gs_flight-fldate.

      IF gs_sbook-custtype = 'P'.
        gs_flight-private = gs_flight-private + 1.
      ELSEIF gs_sbook-custtype = 'B'.
        gs_flight-business = gs_flight-business + 1.
      ENDIF.
    ENDSELECT.

    APPEND gs_flight TO gt_flights.
    CLEAR: gs_flight.

  ENDSELECT.

ENDFORM.
```

![image-20240830132522867](./../img/image-20240830132522867.png)
SBOOK - CLASS 

![image-20240830132540748](./../img/image-20240830132540748.png)

```ABAP
  DATA: LS_WHERE(20),
        LT_WHERE LIKE TABLE OF LS_WHERE.

*   TODO : 빼내기!!!
   IF ZSSD1050-BPCODE IS NOT INITIAL.
      LS_WHERE = |BPCODE = '{ ZSSD1050-BPCODE }' |.
      APPEND LS_WHERE TO LT_WHERE.
  ENDIF.

  IF ZSSD1050-BPTCODE IS NOT INITIAL.
    IF LS_WHERE IS NOT INITIAL.
      LS_WHERE = 'AND'.
      APPEND LS_WHERE TO LT_WHERE.
    ENDIF.
    LS_WHERE = |BPTCODE = '{ ZSSD1050-BPTCODE }'|.
    APPEND LS_WHERE TO LT_WHERE.
  ENDIF.

  IF ZSSD1050-CTRYCODE IS NOT INITIAL.
     IF LS_WHERE IS NOT INITIAL.
      LS_WHERE = 'AND'.
      APPEND LS_WHERE TO LT_WHERE.
    ENDIF.
    LS_WHERE = |CTRYCODE = '{ ZSSD1050-CTRYCODE }'|.
    APPEND LS_WHERE TO LT_WHERE.
  ENDIF.
```

````ABAP
*&---------------------------------------------------------------------*
*& Include          MZBSD1050F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form GET_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM GET_DATA .
*  BP MASTER READ 조회하기

  DATA: LT_BPCODE TYPE RANGE OF ZSSD1050-BPCODE,
        LS_BPCODE LIKE LINE OF LT_BPCODE,
        LT_BPTCODE TYPE RANGE OF ZSSD1050-BPTCODE,
        LS_BPTCODE LIKE LINE OF LT_BPTCODE,
        LT_CTRYCODE TYPE RANGE OF ZSSD1050-CTRYCODE,
        LS_CTRYCODE LIKE LINE OF LT_CTRYCODE.

  IF ZSSD1050-BPCODE IS NOT INITIAL.
    LS_BPCODE-SIGN = 'I'.
    LS_BPCODE-OPTION = 'EQ'.
    LS_BPCODE-LOW = ZSSD1050-BPCODE.
    APPEND LS_BPCODE TO LT_BPCODE.
  ENDIF.

  IF ZSSD1050-BPTCODE IS NOT INITIAL.
     LS_BPTCODE-SIGN = 'I'.
     LS_BPTCODE-OPTION = 'EQ'.
     LS_BPTCODE-LOW = ZSSD1050-BPTCODE.
     APPEND LS_BPTCODE TO LT_BPTCODE.
  ENDIF.

    IF ZSSD1050-CTRYCODE IS NOT INITIAL.
      LS_CTRYCODE-SIGN = 'I'.
      LS_CTRYCODE-OPTION = 'EQ'.
      LS_CTRYCODE-LOW = ZSSD1050-CTRYCODE.
      APPEND LS_CTRYCODE TO LT_CTRYCODE.
    ENDIF.

  DATA LV_DEL TYPE CHAR1 VALUE '%'.

  IF ZSSD1050-VALID = 'X'.
    LV_DEL = ''.
  ELSEIF ZSSD1050-DELETED = 'X'.
    LV_DEL = 'X'.
  ENDIF.


* BP코드를 내림차순으로 정렬 후 조회한다.
  SELECT A~BPCODE B~BPNAME A~BPTCODE A~DELFLG A~ACCNAME A~ACCNUM
         A~BANKCODE A~ZTERM A~CTRYCODE A~BUSTYPE A~BPTEL A~BPADNR
         A~STAMP_DATE_F A~STAMP_TIME_F A~STAMP_USER_F
         B~STAMP_DATE_L B~STAMP_TIME_L B~STAMP_USER_L
    FROM ZTBSD1050 AS A
    INNER JOIN ZTBSD1051 AS B ON A~BPCODE = B~BPCODE
    INTO CORRESPONDING FIELDS OF TABLE GT_BPDATA
    WHERE A~BPCODE IN LT_BPCODE AND
          A~BPTCODE IN LT_BPTCODE AND
          A~CTRYCODE IN LT_CTRYCODE AND
          A~DELFLG LIKE LV_DEL
    ORDER BY A~BPCODE DESCENDING.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form CREATE_BP
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*  BP코드 생성하기
*&---------------------------------------------------------------------*
FORM CREATE_BP.

  DATA: LT_DATA TYPE TABLE OF ZTBSD1050,
        LS_DATA LIKE LINE OF LT_DATA,
        LT_TEXT_DATA TYPE TABLE OF ZTBSD1051,
        LS_TEXT_DATA LIKE LINE OF LT_TEXT_DATA.

  DATA LV_NUM TYPE NUM03.

* NUMBER RANGE 완성
  CALL FUNCTION 'NUMBER_GET_NEXT'
  EXPORTING
    NR_RANGE_NR                   = '01'
    OBJECT                        = 'ZBSD_1050_'
 IMPORTING
   NUMBER                        = LV_NUM

 EXCEPTIONS
   INTERVAL_NOT_FOUND            = 1
   NUMBER_RANGE_NOT_INTERN       = 2
   OBJECT_NOT_FOUND              = 3
   QUANTITY_IS_0                 = 4
   QUANTITY_IS_NOT_1             = 5
   INTERVAL_OVERFLOW             = 6
   BUFFER_OVERFLOW               = 7
   OTHERS                        = 8.

  LS_TEXT_DATA-BPCODE = |V{ LV_NUM } |.
  LS_DATA-BPCODE = |V{ LV_NUM } |.

*   TEXT TABLE에 데이터 넣기
  LS_TEXT_DATA-BPNAME = ZTBSD1051-BPNAME.
  LS_TEXT_DATA-SPARS = SY-LANGU.

*   마스터 테이블에 데이터 넣기
  LS_DATA-BPTCODE = ZTBSD1050-BPTCODE.
  LS_DATA-BPNUM = ZTBSD1050-BPNUM.
  LS_DATA-BPADNR = ZTBSD1050-BPADNR.
  LS_DATA-BPTEL = ZTBSD1050-BPTEL.
  LS_DATA-BUSTYPE = ZTBSD1050-BUSTYPE.
  LS_DATA-CTRYCODE = ZTBSD1050-CTRYCODE.
  LS_DATA-ZTERM = ZTBSD1050-ZTERM.
  LS_DATA-BANKCODE = ZTBSD1050-BANKCODE.
  LS_DATA-ACCNUM = ZTBSD1050-ACCNUM.
  LS_DATA-ACCNAME = ZTBSD1050-ACCNAME.

*   TIMESTAMP 넣기
  LS_DATA-STAMP_DATE_F = SY-DATUM.
  LS_DATA-STAMP_TIME_F = SY-UZEIT.
  LS_DATA-STAMP_USER_F = SY-UNAME.
  LS_DATA-STAMP_DATE_L = SY-DATUM.
  LS_DATA-STAMP_TIME_L = SY-UZEIT.
  LS_DATA-STAMP_USER_L = SY-UNAME.

  LS_TEXT_DATA-STAMP_DATE_F = SY-DATUM.
  LS_TEXT_DATA-STAMP_TIME_F = SY-UZEIT.
  LS_TEXT_DATA-STAMP_USER_F = SY-UNAME.
  LS_TEXT_DATA-STAMP_DATE_L = SY-DATUM.
  LS_TEXT_DATA-STAMP_TIME_L = SY-UZEIT.
  LS_TEXT_DATA-STAMP_USER_L = SY-UNAME.

*  생성 하겠냐는 컨펌창 띄우기
  PERFORM CON_POPUP USING 'CREATE' CHANGING LV_ANSWER.

  IF LV_ANSWER = 2.
    RETURN.
  ENDIF.

* INSERT 시키기
  INSERT INTO ZTBSD1050 VALUES LS_DATA.
  INSERT INTO ZTBSD1051 VALUES LS_TEXT_DATA.
  PERFORM REFRESH.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form delete
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM DELETE .

  CALL METHOD GO_ALV->GET_SELECTED_ROWS
    IMPORTING
      ET_ROW_NO = GT_ROW.

* 만약 행을 선택하지 않고 삭제 버튼을 누른다면 경고창
  IF GT_ROW IS INITIAL.
    PERFORM POPUP_MSG USING 'ROW'.
    RETURN.
  ENDIF.

  READ TABLE GT_ROW INTO GS_ROW INDEX 1.
  READ TABLE GT_BPDATA INTO GS_BPDATA INDEX GS_ROW-ROW_ID.

*  삭제 하겠냐는 컨펌 팝업창 생성
  PERFORM CON_POPUP USING 'DELETE' CHANGING LV_ANSWER.

  IF LV_ANSWER = 2.
    RETURN.
  ENDIF.

  SELECT * FROM ZTBSD1030 INTO TABLE GT_ZTBSD1030.
  READ TABLE GT_ZTBSD1030 INTO GS_ZTBSD1030 WITH KEY LOGID = SY-UNAME.
  IF SY-SUBRC = 0.
  GS_BPDATA-STAMP_USER_L = GS_ZTBSD1030-EMPID.
  GS_BPDATA-STAMP_DATE_L = SY-DATUM.
  GS_BPDATA-STAMP_TIME_L = SY-UZEIT.

  GS_BPDATA-DELFLG = 'X'.

    MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1050.
    MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1051.
    UPDATE ZTBSD1050 FROM GS_ZTBSD1050.
    UPDATE ZTBSD1051 FROM GS_ZTBSD1051.
    MODIFY GT_BPDATA FROM GS_BPDATA INDEX GS_ROW-ROW_ID.
    PERFORM REFRESH.
  ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form ALV_REFRESH
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM ALV_REFRESH .
  CLEAR: GS_ROW.
  CALL METHOD GO_ALV->REFRESH_TABLE_DISPLAY
      EXCEPTIONS
        FINISHED = 1
        OTHERS   = 2.
    IF SY-SUBRC <> 0.
*     Implement suitable error handling here
    ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form UPDATE
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM UPDATE .
  CALL METHOD GO_ALV->GET_SELECTED_ROWS
    IMPORTING
      ET_ROW_NO = GT_ROW.

* 만약 행을 선택하지 않고 수정 버튼을 누른다면 경고창
  IF GT_ROW IS INITIAL.
    PERFORM POPUP_MSG USING 'ROW'.
    RETURN.
  ENDIF.

* 선택한 행에 맞는 데이터 들고와서 수정 팝업창에 띄우기
  READ TABLE GT_ROW INTO GS_ROW INDEX 1.
  READ TABLE GT_BPDATA INTO GS_BPDATA INDEX GS_ROW-ROW_ID.
  MOVE-CORRESPONDING GS_BPDATA TO ZSBSD50.
  CALL SCREEN 120
    STARTING AT 10 10.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form REFRESH
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM REFRESH .
  IF SY-SUBRC = 0.
     PERFORM GET_DATA.
     PERFORM ALV_REFRESH.
     MESSAGE 'Success, Data Save' TYPE 'S'.
    ELSE.
     MESSAGE 'Error, Data Save' TYPE 'E'.
  ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form RESET
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM RESET .
*  새로고침 버튼을 누르면 ALV 화면도 초기화 , 라디오 버튼 및 입력필드도 초기화 시킨다.
 CLEAR: GT_BPDATA, ZSSD1050.
 PERFORM RADIO_RESET.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form radio_reset
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM RADIO_RESET .
   IF ZSSD1050-VALID IS INITIAL AND ZSSD1050-ALL IS INITIAL AND
     ZSSD1050-DELETED IS INITIAL.
     ZSSD1050-VALID = 'X'.
   ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form popup_msg
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*&      --> ROW
*&---------------------------------------------------------------------*
FORM POPUP_MSG  USING  P_ROW.
  IF P_ROW = 'ROW'.
    MESSAGE ID 'ZCOMMON_MSG' TYPE 'S' NUMBER '008' DISPLAY LIKE 'E'.
  ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form CON_POPUP
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*&      --> P_
*&---------------------------------------------------------------------*
FORM CON_POPUP USING P_VALUE CHANGING LV_ANSWER.

  DATA : DOMAIN TYPE CHAR10 VALUE 'BP MASTER',
         CRUD_TYPE(2) TYPE C VALUE '수정'.

  IF P_VALUE = 'DELETE'.
    CRUD_TYPE = '삭제'.
  ELSEIF P_VALUE = 'CREATE'.
     CRUD_TYPE = '생성'.
  ENDIF.

  CALL FUNCTION 'POPUP_TO_CONFIRM'
  EXPORTING
    TITLEBAR       = | { DOMAIN } 데이터 { CRUD_TYPE } |
    TEXT_QUESTION  = | 해당 { DOMAIN } 데이터를 { CRUD_TYPE }하시겠습니까? |
    TEXT_BUTTON_1  = 'YES'
    TEXT_BUTTON_2  = 'NO'
    DISPLAY_CANCEL_BUTTON = ''
  IMPORTING
    ANSWER         = LV_ANSWER
  EXCEPTIONS
    TEXT_NOT_FOUND = 1
    OTHERS         = 2.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form UPDATE_BP
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM UPDATE_BP .
*  1. 해당 데이터를 수정할거냐?
  PERFORM CON_POPUP USING 'UPDATE' CHANGING LV_ANSWER.

  IF LV_ANSWER = 2.
    RETURN.
  ENDIF.

  SELECT * FROM ZTBSD1030 INTO TABLE GT_ZTBSD1030.
  READ TABLE GT_ZTBSD1030 INTO GS_ZTBSD1030 WITH KEY LOGID = SY-UNAME.
  ZSBSD50-STAMP_USER_L = GS_ZTBSD1030-EMPID.
  ZSBSD50-STAMP_DATE_L = SY-DATUM.
  ZSBSD50-STAMP_TIME_L = SY-UZEIT.

  IF SY-SUBRC = 0.
    MOVE-CORRESPONDING ZSBSD50 TO GS_BPDATA.
    MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1050.
    MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1051.

    UPDATE ZTBSD1050 FROM GS_ZTBSD1050.
    UPDATE ZTBSD1051 FROM GS_ZTBSD1051.
    MODIFY GT_BPDATA FROM GS_BPDATA INDEX GS_ROW-ROW_ID.
  ENDIF.
ENDFORM.
````

````ABAP
*&---------------------------------------------------------------------*
*& Include          MZBSD1050F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form GET_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM GET_DATA .
*  BP MASTER READ 조회하기

  DATA: LT_BPCODE TYPE RANGE OF ZSSD1050-BPCODE,
        LS_BPCODE LIKE LINE OF LT_BPCODE,
        LT_BPTCODE TYPE RANGE OF ZSSD1050-BPTCODE,
        LS_BPTCODE LIKE LINE OF LT_BPTCODE,
        LT_CTRYCODE TYPE RANGE OF ZSSD1050-CTRYCODE,
        LS_CTRYCODE LIKE LINE OF LT_CTRYCODE.

  IF ZSSD1050-BPCODE IS NOT INITIAL.
    LS_BPCODE-SIGN = 'I'.
    LS_BPCODE-OPTION = 'EQ'.
    LS_BPCODE-LOW = ZSSD1050-BPCODE.
    APPEND LS_BPCODE TO LT_BPCODE.
  ENDIF.

  IF ZSSD1050-BPTCODE IS NOT INITIAL.
     LS_BPTCODE-SIGN = 'I'.
     LS_BPTCODE-OPTION = 'EQ'.
     LS_BPTCODE-LOW = ZSSD1050-BPTCODE.
     APPEND LS_BPTCODE TO LT_BPTCODE.
  ENDIF.

    IF ZSSD1050-CTRYCODE IS NOT INITIAL.
      LS_CTRYCODE-SIGN = 'I'.
      LS_CTRYCODE-OPTION = 'EQ'.
      LS_CTRYCODE-LOW = ZSSD1050-CTRYCODE.
      APPEND LS_CTRYCODE TO LT_CTRYCODE.
    ENDIF.

  DATA LV_DEL TYPE CHAR1 VALUE '%'.

  IF ZSSD1050-VALID = 'X'.
    LV_DEL = ''.
  ELSEIF ZSSD1050-DELETED = 'X'.
    LV_DEL = 'X'.
  ENDIF.


* BP코드를 내림차순으로 정렬 후 조회한다.
  SELECT A~BPCODE B~BPNAME A~BPTCODE A~DELFLG A~ACCNAME A~ACCNUM
         A~BANKCODE A~ZTERM A~CTRYCODE A~BUSTYPE A~BPTEL A~BPADNR
         A~STAMP_DATE_F A~STAMP_TIME_F A~STAMP_USER_F
         B~STAMP_DATE_L B~STAMP_TIME_L B~STAMP_USER_L
    FROM ZTBSD1050 AS A
    INNER JOIN ZTBSD1051 AS B ON A~BPCODE = B~BPCODE
    INTO CORRESPONDING FIELDS OF TABLE GT_BPDATA
    WHERE A~BPCODE IN LT_BPCODE AND
          A~BPTCODE IN LT_BPTCODE AND
          A~CTRYCODE IN LT_CTRYCODE AND
          A~DELFLG LIKE LV_DEL
    ORDER BY A~BPCODE DESCENDING.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form CREATE_BP
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*  BP코드 생성하기
*&---------------------------------------------------------------------*
FORM CREATE_BP.

  DATA: LT_DATA TYPE TABLE OF ZTBSD1050,
        LS_DATA LIKE LINE OF LT_DATA,
        LT_TEXT_DATA TYPE TABLE OF ZTBSD1051,
        LS_TEXT_DATA LIKE LINE OF LT_TEXT_DATA.

  DATA LV_NUM TYPE NUM03.

* NUMBER RANGE 완성
  CALL FUNCTION 'NUMBER_GET_NEXT'
  EXPORTING
    NR_RANGE_NR                   = '01'
    OBJECT                        = 'ZBSD_1050_'
 IMPORTING
   NUMBER                        = LV_NUM

 EXCEPTIONS
   INTERVAL_NOT_FOUND            = 1
   NUMBER_RANGE_NOT_INTERN       = 2
   OBJECT_NOT_FOUND              = 3
   QUANTITY_IS_0                 = 4
   QUANTITY_IS_NOT_1             = 5
   INTERVAL_OVERFLOW             = 6
   BUFFER_OVERFLOW               = 7
   OTHERS                        = 8.

*  PERFORM ADD_USERID.
*
*  MOVE-CORRESPONDING ZSBSD50 TO GS_BPDATA.
*  MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1050.
*  MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1051.
*  GS_ZTBSD1051-SPARS = SY-LANGU.
*
*  UPDATE ZTBSD1050 FROM GS_ZTBSD1050.
*  UPDATE ZTBSD1051 FROM GS_ZTBSD1051.
*  MODIFY GT_BPDATA FROM GS_BPDATA INDEX GS_ROW-ROW_ID.


  LS_TEXT_DATA-BPCODE = |V{ LV_NUM } |.
  LS_DATA-BPCODE = |V{ LV_NUM } |.

*   TEXT TABLE에 데이터 넣기
  LS_TEXT_DATA-BPNAME = ZTBSD1051-BPNAME.
  LS_TEXT_DATA-SPARS = SY-LANGU.

*   마스터 테이블에 데이터 넣기
  LS_DATA-BPTCODE = ZTBSD1050-BPTCODE.
  LS_DATA-BPNUM = ZTBSD1050-BPNUM.
  LS_DATA-BPADNR = ZTBSD1050-BPADNR.
  LS_DATA-BPTEL = ZTBSD1050-BPTEL.
  LS_DATA-BUSTYPE = ZTBSD1050-BUSTYPE.
  LS_DATA-CTRYCODE = ZTBSD1050-CTRYCODE.
  LS_DATA-ZTERM = ZTBSD1050-ZTERM.
  LS_DATA-BANKCODE = ZTBSD1050-BANKCODE.
  LS_DATA-ACCNUM = ZTBSD1050-ACCNUM.
  LS_DATA-ACCNAME = ZTBSD1050-ACCNAME.

*   TIMESTAMP 넣기
  LS_DATA-STAMP_DATE_F = SY-DATUM.
  LS_DATA-STAMP_TIME_F = SY-UZEIT.
  LS_DATA-STAMP_USER_F = SY-UNAME.
  LS_DATA-STAMP_DATE_L = SY-DATUM.
  LS_DATA-STAMP_TIME_L = SY-UZEIT.
  LS_DATA-STAMP_USER_L = SY-UNAME.

  LS_TEXT_DATA-STAMP_DATE_F = SY-DATUM.
  LS_TEXT_DATA-STAMP_TIME_F = SY-UZEIT.
  LS_TEXT_DATA-STAMP_USER_F = SY-UNAME.
  LS_TEXT_DATA-STAMP_DATE_L = SY-DATUM.
  LS_TEXT_DATA-STAMP_TIME_L = SY-UZEIT.
  LS_TEXT_DATA-STAMP_USER_L = SY-UNAME.

*  생성 하겠냐는 컨펌창 띄우기
  PERFORM CON_POPUP USING 'CREATE' CHANGING LV_ANSWER.

  IF LV_ANSWER = 2.
    RETURN.
  ENDIF.

* INSERT 시키기
  INSERT INTO ZTBSD1050 VALUES LS_DATA.
  INSERT INTO ZTBSD1051 VALUES LS_TEXT_DATA.
  PERFORM REFRESH.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form ALV_REFRESH
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM ALV_REFRESH .
  CLEAR: GS_ROW.
  CALL METHOD GO_ALV->REFRESH_TABLE_DISPLAY
      EXCEPTIONS
        FINISHED = 1
        OTHERS   = 2.
    IF SY-SUBRC <> 0.
*     Implement suitable error handling here
    ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form UPDATE
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM UPDATE .
  CALL METHOD GO_ALV->GET_SELECTED_ROWS
    IMPORTING
      ET_ROW_NO = GT_ROW.

* 만약 행을 선택하지 않고 수정 버튼을 누른다면 경고창
  IF GT_ROW IS INITIAL.
    PERFORM POPUP_MSG USING 'ROW'.
    RETURN.
  ENDIF.

* 선택한 행에 맞는 데이터 들고와서 수정 팝업창에 띄우기
  READ TABLE GT_ROW INTO GS_ROW INDEX 1.
  READ TABLE GT_BPDATA INTO GS_BPDATA INDEX GS_ROW-ROW_ID.
  MOVE-CORRESPONDING GS_BPDATA TO ZSBSD50.
  CALL SCREEN 120
    STARTING AT 10 10.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form REFRESH
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM REFRESH .
  IF SY-SUBRC = 0.
     PERFORM GET_DATA.
     PERFORM ALV_REFRESH.
     MESSAGE 'Success, Data Save' TYPE 'S'.
    ELSE.
     MESSAGE 'Error, Data Save' TYPE 'E'.
  ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form RESET
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM RESET .
*  새로고침 버튼을 누르면 ALV 화면도 초기화 , 라디오 버튼 및 입력필드도 초기화 시킨다.
 CLEAR: GT_BPDATA, ZSSD1050.
 PERFORM RADIO_RESET.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form radio_reset
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM RADIO_RESET .
   IF ZSSD1050-VALID IS INITIAL AND ZSSD1050-ALL IS INITIAL AND
     ZSSD1050-DELETED IS INITIAL.
     ZSSD1050-VALID = 'X'.
   ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form popup_msg
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*&      --> ROW
*&---------------------------------------------------------------------*
FORM POPUP_MSG  USING  P_ROW.
  IF P_ROW = 'ROW'.
    MESSAGE ID 'ZCOMMON_MSG' TYPE 'S' NUMBER '008' DISPLAY LIKE 'E'.
  ENDIF.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form CON_POPUP
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*&      --> P_
*&---------------------------------------------------------------------*
FORM CON_POPUP USING P_VALUE CHANGING LV_ANSWER.

  DATA : DOMAIN TYPE CHAR10 VALUE 'BP MASTER',
         CRUD_TYPE(2) TYPE C VALUE '수정'.

  IF P_VALUE = 'DELETE'.
    CRUD_TYPE = '삭제'.
  ELSEIF P_VALUE = 'CREATE'.
     CRUD_TYPE = '생성'.
  ENDIF.

  CALL FUNCTION 'POPUP_TO_CONFIRM'
  EXPORTING
    TITLEBAR       = | { DOMAIN } 데이터 { CRUD_TYPE } |
    TEXT_QUESTION  = | 해당 { DOMAIN } 데이터를 { CRUD_TYPE }하시겠습니까? |
    TEXT_BUTTON_1  = 'YES'
    TEXT_BUTTON_2  = 'NO'
    DISPLAY_CANCEL_BUTTON = ''
  IMPORTING
    ANSWER         = LV_ANSWER
  EXCEPTIONS
    TEXT_NOT_FOUND = 1
    OTHERS         = 2.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form delete
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM DELETE .

  CALL METHOD GO_ALV->GET_SELECTED_ROWS
    IMPORTING
      ET_ROW_NO = GT_ROW.

* 만약 행을 선택하지 않고 삭제 버튼을 누른다면 경고창
  IF GT_ROW IS INITIAL.
    PERFORM POPUP_MSG USING 'ROW'.
    RETURN.
  ENDIF.

  READ TABLE GT_ROW INTO GS_ROW INDEX 1.
  READ TABLE GT_BPDATA INTO GS_BPDATA INDEX GS_ROW-ROW_ID.
  MOVE-CORRESPONDING GS_BPDATA TO ZSBSD50.

*  삭제 하겠냐는 컨펌 팝업창 생성
  PERFORM CON_POPUP USING 'DELETE' CHANGING LV_ANSWER.

  IF LV_ANSWER = 2.
    RETURN.
  ENDIF.

  PERFORM UPDATE_DATA USING 'DELETE'.
  PERFORM REFRESH.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form UPDATE_BP
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM UPDATE_BP .
*  1. 해당 데이터를 수정할거냐?
  PERFORM CON_POPUP USING 'UPDATE' CHANGING LV_ANSWER.

*  컨펌 팝업에서 NO를 누를경우 RETURN
  IF LV_ANSWER = 2.
    RETURN.
  ENDIF.

  PERFORM UPDATE_DATA USING 'UPDATE'.
  PERFORM ALV_REFRESH.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form UPDATE_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*&      --> P_
*&---------------------------------------------------------------------*
FORM UPDATE_DATA  USING P_TYPE.
*  USER ID 가져오기
  PERFORM ADD_USERID.

  IF P_TYPE = 'DELETE'.
    ZSBSD50-DELFLG = 'X'.
  ENDIF.

  MOVE-CORRESPONDING ZSBSD50 TO GS_BPDATA.
  MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1050.
  MOVE-CORRESPONDING GS_BPDATA TO GS_ZTBSD1051.
  GS_ZTBSD1051-SPARS = SY-LANGU.

  UPDATE ZTBSD1050 FROM GS_ZTBSD1050.
  UPDATE ZTBSD1051 FROM GS_ZTBSD1051.
  MODIFY GT_BPDATA FROM GS_BPDATA INDEX GS_ROW-ROW_ID.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form ADD_USERID
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM ADD_USERID .
  SELECT * FROM ZTBSD1030 INTO TABLE GT_ZTBSD1030.
  READ TABLE GT_ZTBSD1030 INTO GS_ZTBSD1030 WITH KEY LOGID = SY-UNAME.
  ZSBSD50-STAMP_USER_L = GS_ZTBSD1030-EMPID.
  ZSBSD50-STAMP_DATE_L = SY-DATUM.
  ZSBSD50-STAMP_TIME_L = SY-UZEIT.
ENDFORM.
````

