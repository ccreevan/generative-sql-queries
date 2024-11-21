--Calendar table generation.
--Credit goes to Jeff Moden.
DECLARE @StartYear      DATETIME,
        @Years          INT,
        @Days           INT
;
 SELECT @StartYear = '2020',
        @Years     = 500,
        @Days      = DATEDIFF(dd,@StartYear,DATEADD(yy,@Years+1,@StartYear))
;
WITH --===== Itzik-Style CROSS JOIN counts from 1 to the number of days needed
      E1(N) AS (
                SELECT 1 UNION ALL SELECT 1 UNION ALL SELECT 1 UNION ALL 
                SELECT 1 UNION ALL SELECT 1 UNION ALL SELECT 1 UNION ALL 
                SELECT 1 UNION ALL SELECT 1 UNION ALL SELECT 1 UNION ALL SELECT 1
               ),                          -- 1*10^1 or 10 rows
      E2(N) AS (SELECT 1 FROM E1 a, E1 b), -- 1*10^2 or 100 rows
      E4(N) AS (SELECT 1 FROM E2 a, E2 b), -- 1*10^4 or 10,000 rows
      E8(N) AS (SELECT 1 FROM E4 a, E4 b), -- 1*10^8 or 100,000,000 rows
cteTally(N) AS (SELECT TOP (@Days) ROW_NUMBER() OVER (ORDER BY (SELECT NULL)) FROM E8)
 SELECT TOP 10000 WholeDate = DATEADD(dd,N-1,@StartYear)
   FROM cteTally
;
