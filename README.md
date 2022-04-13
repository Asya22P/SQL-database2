# SQL-database2
# решение задач
# 1) Найдите общую сумму, потраченную на полеты каждым пассажиром.Выведите имя и стоимость всех полетов.
# 2) Найдите среднее количество времени, потраченное в воздухе каждой возрастной группой. Выведите возрастную группу и кол-во времени в минутах (округленное до двух знаков после запятой.
# 3) Определите пассажиров с максимальным количеством полетов. Выведите имя и количество полетов
# 4) Определите самые популярные направления полетов. Направления с максимальным количеством прилетов.

1)
     
     create table table_12 as
       select 
         t1.name,
         t1.id,
         t2.flying_id
       from passengers t1
       inner join fly_mapping t2
       on t1.id = t2.passenger_id;
     
     
     
     create table table_23 as
       select 
         t1.flying_id,
         t2.price
       from fly_mapping t1
       inner join flying t2
       on t1.flying_id = t2.id;
     
     
     create table table_123 as
       select 
        t1.name,
        t1.id,
        t2.flying_id,
        t2.price
       from table_12 t1
       inner join table_23 t2
       on t1.flying_id = t2.flying_id; 
       
       
     select
       name,
       sum(price) as sum_price
     from table_123
     group by name;
     
     
     2)
     
     
     create table table_12 as
       select 
         t1.age_group,
         t1.id,
         t2.flying_id
       from passengers t1
       inner join fly_mapping t2
       on t1.id = t2.passenger_id;
     
     
     
     create table table_23 as
       select 
         t1.flying_id,
         
         t2.flight_time
       from fly_mapping t1
       inner join flying t2
       on t1.flying_id = t2.id;
     
     
     
     
     create table table_123 as
       select 
        t1.age_group,
        t1.id,
        t2.flying_id,
        t2.flight_time
       from table_12 t1
       inner join table_23 t2
       on t1.flying_id = t2.flying_id;
       
       
     select
       age_group,
       round(avg(flight_time),2) as avg_flight_time
     from table_123
     group by age_group;
     
     
     3)
     
     
     
     
     create table table_12 as
       select 
         t1.name,
         t1.id,
         t2.flying_id
       from passengers t1
       inner join fly_mapping t2
       on t1.id = t2.passenger_id;
     
     
     
     create table table_23 as
       select 
         t1.passenger_id,
         t1.flying_id
       from fly_mapping t1
       inner join flying t2
       on t1.flying_id = t2.id; 
     
     
     create table table_123 as
       select 
        t1.name,
        t1.id,
        t2.flying_id,
        t2.passenger_id
       from table_12 t1
       inner join table_23 t2
       on t1.id = t2.passenger_id;
       
     create table table_1234 as  
     select
       name,
       count(distinct flying_id) as count_flying_id
     from table_123
     group by name;
     
     select * from table_1234;
     
     
     select
       max(count_flying_id) as max_count_flying_id
     from table_1234;4)
     
     
     
     create table table_12 as
       select 
         t1.name,
         t1.id,
         t2.flying_id
       from passengers t1
       inner join fly_mapping t2
       on t1.id = t2.passenger_id;
     
     
     
     create table table_23 as
       select 
         t1.passenger_id,
         t1.flying_id
       from fly_mapping t1
       inner join flying t2
       on t1.flying_id = t2.id;  
     
     
     create table table_123 as
       select 
        t1.name,
        t1.id,
        t2.flying_id,
        t2.passenger_id
       from table_12 t1
       inner join table_23 t2
       on t1.id = t2.passenger_id;
      
     
     create table table_1234 as  
     select
       name,
       count( distinct flying_id) as count_flying_id
       
     from table_123
     group by name;
     
     create table table_12345 as
     select 
       avg(count_flying_id ) as avg_count_id
     from table_1234;
     
     select 
       t1.name,
       t1.count_flying_id
     from table_1234 t1
     inner join table_12345 t2
     on t1.count_flying_id > t2.avg_count_id;
     
     4)
     
     
     create table table_12 as
       select 
         t1.point_to,
         t1.id
         
       from flying t1
       inner join fly_mapping t2
       on t1.id = t2.flying_id;
     
     create table table_123 as
     select
       point_to,
       count( point_to) as count_point_to
       from table_12
       group by point_to;
     select * from table_123;
     select 
       max(count_point_to) as max_count_point_to
       from table_123;
