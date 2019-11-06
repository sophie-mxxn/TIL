**1267 : Illegal mix of collations**

------

> mysql collate ; 데이터 정렬 

​	테이블 혹은 WHERE 절의 데이터 정렬 



**collation 확인**

$ mysql > SHOW VARIABLES LIKE 'collation%'; 

$ mysql > show full columns from hr_cc_normalised_data_date_v; (테이블 확인)



> error 내용
>
> Illegal mix of collations (latin1_general_cs,IMPLICIT) and (latin1_general_ci,IMPLICIT) for operation '='
>
> 동일하지 않은 두 개의 데이터의 비교에 대한 오류



[solutions]

1. 테이블의 데이터 정렬 변경 

   ```mysql
   ALTER TABLE {table_name} DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
   ```

2. binary 연산자 사용

   ```mysql
   WHERE binary table1.column1 = binary table2.column1
   ```