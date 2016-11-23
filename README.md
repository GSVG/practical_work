# practical_work
practice

CREATE OR REPLACE FUNCTION func_mfr(v_price IN PRODUCTS.PRICE%TYPE) 
        RETURN VARCHAR2 AS
                    
    CURSOR cur_mfr_disc 
      IS SELECT DISTINCT m.MFR
    FROM  PRODUCTS p INNER JOIN MANUFACTURERS m ON p.mfr_id = m.MFR_ID
      WHERE p.price > v_price
      ORDER BY m.MFR;
  
     rec_cur cur_mfr_disc%ROWTYPE;
     srt_manf VARCHAR2(4000) := '';
                 
      BEGIN
        FOR rec_cur IN cur_mfr_disc 
          LOOP
            srt_manf := srt_manf||', '|| rec_cur.mfr;
          END LOOP;    
             
          RETURN srt_manf;
          
        COMMIT WORK;
         
      END func_mfr;
