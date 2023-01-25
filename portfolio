--Change Table Name
--USE portfolio
--GO
--EXEC sp_rename 'dbo.customer', 'customers'

--Remove Column
--ALTER TABLE agents
--DROP COLUMN COUNTRY

--Orders Temp Table
DROP TABLE IF EXISTS #temp1

SELECT
	CUST_CODE,
	AGENT_CODE,
	COUNT(ORD_NUM) AS OrdersCount,
	MAX(ORD_DATE) AS LastOrdDate,
	SUM(ORD_AMOUNT) AS TotalOrdAmount,
	SUM(ADVANCE_AMOUNT) AS TotalAdvAmount,
	ORD_DESCRIPTION
INTO #temp1
FROM orders
GROUP BY
	CUST_CODE,
	AGENT_CODE,
	ORD_DESCRIPTION;

--SELECT * FROM #temp1

--Orders CTE
WITH temp_orders AS (
		SELECT
		CUST_CODE,
		AGENT_CODE,
		COUNT(ORD_NUM) AS OrdersCount,
		MAX(ORD_DATE) AS LastOrdDate,
		SUM(ORD_AMOUNT) AS TotalOrdAmount,
		SUM(ADVANCE_AMOUNT) AS TotalAdvAmount,
		ORD_DESCRIPTION
	FROM orders
	GROUP BY
		CUST_CODE,
		AGENT_CODE,
		ORD_DESCRIPTION
)

--Summarized Data
SELECT
	c.CUST_CODE,
	c.CUST_NAME,
	a.AGENT_CODE,
	a.AGENT_NAME,
	a.COMMISSION,
	c.CUST_CITY,
	c.WORKING_AREA,
	c.CUST_COUNTRY,
	o.OrdersCount,
	o.LastOrdDate,
	o.TotalOrdAmount,
	o.TotalAdvAmount,
	ORD_DESCRIPTION
FROM customers c
	LEFT JOIN temp_orders o ON c.CUST_CODE = o.CUST_CODE
	LEFT JOIN agents a ON c.AGENT_CODE = a.AGENT_CODE
ORDER BY
	o.OrdersCount DESC;
